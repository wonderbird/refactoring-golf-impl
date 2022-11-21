# Starter Template for new Java Projects

This repository provides a starter template for new Java projects.

## Thanks

Many thanks to [JetBrains](https://www.jetbrains.com/?from=dotnet-starter) who provide
an [Open Source License](https://www.jetbrains.com/community/opensource/) for this project ❤️.

## Development

### What is Inside?

This project provides a simple gradle based Java project template. The sources are kept in the `app/src` folder.

### Creating a New Project From this Template

After having forked this starter project, you'll need to adapt the project names in the configuration files and some
text files:

1. Change the LICENSE to your needs

2. Renaming from `javastarter` to ...
  - rename the package directory `javastarter` to your desired package name
  - adapt the package of the main class in `app/build.gradle`
  - change the root project name in `settings.gradle`
  - rename the classes `App` and `AppTest` to your desired class names

## Build, Test, Run

### Prerequisites

To compile, test and run this project java 17 is required on your machine. For calculating code
metrics I recommend [metrix++](https://github.com/metrixplusplus/metrixplusplus). This requires
python.

### Build the Solution and Run the Tests

```sh
./gradlew clean build test
```

## Before Creating a Pull Request

### Check Code Metrics

... check code metrics using [metrix++](https://github.com/metrixplusplus/metrixplusplus)

- Configure the location of the cloned metrix++ scripts
  ```sh
  export METRIXPP=/path/to/metrixplusplus
  ```

- Collect metrics
  ```sh
  python "$METRIXPP/metrix++.py" collect --std.code.complexity.cyclomatic --std.code.lines.code --std.code.todo.comments --std.code.maintindex.simple -- .
  ```

- Get an overview
  ```sh
  python "$METRIXPP/metrix++.py" view --db-file=./metrixpp.db
  ```

- Apply thresholds
  ```sh
  python "$METRIXPP/metrix++.py" limit --db-file=./metrixpp.db --max-limit=std.code.complexity:cyclomatic:5 --max-limit=std.code.lines:code:25:function --max-limit=std.code.todo:comments:0 --max-limit=std.code.mi:simple:1
  ```

At the time of writing, I want to stay below the following thresholds:

```
--max-limit=std.code.complexity:cyclomatic:5
--max-limit=std.code.lines:code:25:function
--max-limit=std.code.todo:comments:0
--max-limit=std.code.mi:simple:1
```

Finally, remove all code duplication. The next section describes how to detect code duplication.

### Remove Code Duplication Where Appropriate

To detect duplicates I use the [CPD Copy Paste Detector](https://pmd.github.io/latest/pmd_userdocs_cpd.html)
tool from the [PMD Source Code Analyzer Project](https://pmd.github.io/latest/index.html).

If you have installed PMD by download & unzip, replace `pmd` by `./run.sh`.
The [homebrew pmd formula](https://formulae.brew.sh/formula/pmd) makes the `pmd` command globally available.

```sh
pmd cpd --minimum-tokens 50 --files src
```

## References

- [Gradle Build Init Plugin](https://docs.gradle.org/current/userguide/build_init_plugin.html) - This project has been created using `gradle init --type java-application`.
