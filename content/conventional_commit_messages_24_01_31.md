---
title: Conventional commit messages
date: 2024-01-31 08:06
tags: ["coding", "git"]
draft: false
---
I recently tried out using [conventional commit messages](https://www.conventionalcommits.org/) for git.

The basic structure of a commit message should be

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

For the type only feat and fix are hard definitions. Other types with definitions include

- feat – a new feature is introduced with the changes
- fix – a bug fix has occurred
- chore – changes that do not relate to a fix or feature and don't modify src or test files (for example updating dependencies)
- refactor – refactored code that neither fixes a bug nor adds a feature
- docs – updates to documentation such as a the README or other markdown files
- style – changes that do not affect the meaning of the code, likely related to code formatting such as white-space, missing semi-colons, and so on.
- test – including new or correcting previous tests
- perf – performance improvements
- ci – continuous integration related
- build – changes that affect the build system or external dependencies
- revert – reverts a previous commit

There are some conventions if you use an automatic versioning tool:

- adding a `BREAKING_CHANGE` or appending a `!` after the type/scope bumps the `MAJOR` version.
- any `feat` commit increases the `MINOR` version
- any other commit type only the `PATCH` number.
