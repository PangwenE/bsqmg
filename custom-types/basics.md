# Basics

To create a custom type, create a header file for your type. In this example, we'll make a Custom Type called `Counter`
that extends `MonoBehavior`.

In your header file, include Custom Types - types are declared using macros, similarly to hooking.

```cpp
#pragma once

#include "custom-types/shared/macros.hpp"
```

Since our `Counter` Custom Type will be extending `MonoBehaviour`, we will include this too.

```cpp
#include "UnityEngine/MonoBehaviour.hpp"
```

## Declaring the type.

Now we have included the necessary macros - we can now declare our `Counter` type.

```cpp
// General format is (Namespace, ClassName, any classes to extend from, contents)
DECLARE_CLASS_CODEGEN(MyNamespace, Counter, UnityEngine::MonoBehaviour,
    public:
        // DECLARE_INSTANCE_METHOD can override any inherited methods and create il2cpp methods.
        DECLARE_INSTANCE_METHOD(void, Update);
        
        // DECLARE_INSTANCE_FIELD can create fields.
        DECLARE_INSTANCE_FIELD(int, counts);
        
        DECLARE_CTOR(ctor);
        DECLARE_SIMPLE_DTOR();
)
```

In C#, this would translate to the following:

```csharp
namespace MyNamespace 
{
    public class Counter : MonoBehaviour 
    {
        public int counts;
        
        public void Update() 
        {
            
        }
    }
}
```

## Defining the type.

Create a new source file - name it accordingly - and include your Custom Type header.

To define the type, use the `DEFINE_TYPE(Namespace, Class)` macro.

For our `Counter` type, this will look like so:

```cpp
#include "Counter.hpp"

DEFINE_TYPE(MyNamespace, Counter);
```

We can now implement methods defined in the declaration.

- `OnUpdate` - OnUpdate Method, override from `MonoBehaviour` - Declared by `DECLARE_INSTANCE_METHOD(void, Update);`
- `ctor` - Constructor - Declared by `DECLARE_CTOR(ctor);`

Our `Counter.cpp` file now looks like this:

```cpp
#include "Counter.hpp"

DEFINE_TYPE(MyNamespace, Counter);

void MyNamespace::Counter::ctor() {
  // This invokes the Il2CPP constructor - it initializes any fields, such as the "counts" integer field we declared using "DECLARE_INSTANCE_FIELD(int, counts);" 
  INVOKE_CTOR();
}

void MyNamespace::Counter::OnUpdate() {
    // Update method.
    counter = counter + 5;
    // Add 5 to the counter field.
}
```

## Registering the type.

You can register all the Custom Types you have created using the `custom_types::Register::AutoRegister()` method.

This method should be put in your `load()` like so:

```cpp
extern "C" void load() {
    // ... stuff like hooks above this
    custom_types::Register::AutoRegister();
}
```

## Using the type.

Types can be used as normal - for our `Counter` type, we can add it to a GameObject as it is a MonoBehaviour derivative.

```cpp
#include "UnityEngine/GameObject.hpp"
#include "Counter.hpp"

UnityEngine::GameObject* gameObject = UnityEngine::GameObject::New_ctor("CounterObject");
gameObject->AddComponent<MyNamespace::Counter *>();
```
