# BSQ Modding Guide

This guide is aimed for beginners and experienced modders. It goes into most of the concepts you will need or could
potentially need for modding.

The guide contains tutorials on:

- Hooking
- Configuration using `config-utils` (and alternative manual configuration)
- UI using `questui` and **or** `QUC`

## Explore

Checkout the [Getting Started](/getting-started/) guide if you want to learn how to make mods.

The sidebar contains all the guides you can follow. Introduction pages contain infomation on prerequisites and other
useful information.

## Contributing

Contributing is easy, fork, write and pull request - there are few checklists you should follow to make sure the content
you want to add is suitable and is correctly formatted.

#### General rules:

- Make sure it is grammatically correct.
- Links are only allowed to be to the following websites (exceptions can be made on request):
    - GitHub
    - Discord (if related to the page)
    - GitLab
    - Wikipedia
    - Microsoft C++ Documentation
    - Android Documentation
    - Any BMBF website (git.bmbf.dev, bmbf.dev ect.)

#### If you're adding a tutorial/guide on how to use a community library:

- Is the library kept up-to-date relatively quickly with new supported modding versions?
- Is it a library that is worth documenting? (For example, is it actually useful for multiple mods or is it a one-use
  case.)
- If the library is not a mod based library, eg: `fmt` or `fruit`, the PR will be closed. These libraries already have
  their own documentation.

## Contributors

These people have contributed to the guide:

<a href="https://github.com/cal117/bsqmg/graphs/contributors">
  <img id="contributors-im" src="https://contrib.rocks/image?repo=cal117/bsqmg" alt="contributors"/>
</a>

<script>
    const num = Math.round(Math.random() * 10000000);
    document.getElementById("contributors-im").src += `&${num}`;
</script>


