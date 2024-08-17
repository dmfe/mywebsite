---
tags:
    - gradle
    - build tool
    - cli
---

# Command-Line Interface Basics

CLI is the primary method of **inrecacting with Gradle**.
Executing Gradle on the command line conforms to the following structure:
```bash
gradle [taskName...] [--option-name...]
```

Options are allowed _before_ and _after_ task names:
```bash
gradle [--option-name...] [taskName...]
```

Multiple tasks should be separated by space:
```bash
gradle [taskName1 taskName2...] [--option-name...]
```

Options that enable behavior have long-form options with inverses specified with `--no-`:
```bash
gradle [...] --build-cache
gradle [...] --no-build-cache
```

Some long-form options have short-options equivalents:
```bash
gradle --help
gradle -h
```

## Command-Line usage

### Executing tasks

To execute a task called `taskName` on the root project:
```bash
$ gradle :taskName
```
This will run the single task `taskName` and all of its dependencies.

### Specify options for tasks

To pass an option to a task, prefix the option with `--` after the task name:
```bash
$ gradle taskName --exampleOption=exampleValue
```

