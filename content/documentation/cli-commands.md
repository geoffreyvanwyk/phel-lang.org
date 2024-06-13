+++
title = "CLI Commands"
weight = 21
+++

Phel includes a series of commands out-of-the-box.

```bash
# To see an overview of all commands.
vendor/bin/phel list
```

## Build the Project

```bash
vendor/bin/phel build
# Usage:
#   build [options]
#
# Options:
#       --cache|--no-cache            Enable cache
#       --source-map|--no-source-map  Enable source maps
```

Build the current project into the main PHP path. This means that the Phel code will be transpiled into PHP code that will be saved into that directory, with the file `out/index.php` being the entry point. You can run the PHP code directly using the PHP interpreter. This will improve the runtime performance, because there won't be a need to compile the code again.

[Configuration](/documentation/configuration/#buildconfig) in `phel-config.php`:

```php
<?php
return (new \Phel\Config\PhelConfig())
    ->setBuildConfig((new \Phel\Config\PhelBuildConfig())
        ->setMainPhelNamespace('your-ns\index')
        ->setMainPhpPath('out/index.php'));
```

## Export Definitions

Export all definitions with the metadata `{:export true}` as PHP classes.

It generates PHP classes at namespace level and a method for each exported definition. This allows you to use the exported Phel functions from your PHP code.

```bash
vendor/bin/phel export
```

[Configuration](/documentation/configuration/#export-definitions) in `phel-config.php`:

```php
<?php
return (new \Phel\Config\PhelConfig())
    ->setExportConfig((new \Phel\Config\PhelExportConfig())
        ->setFromDirectories(['src'])
        ->setNamespacePrefix('PhelGenerated')
        ->setTargetDirectory('src/PhelGenerated'));
```

## Format Phel Files

Formats the given files. You can pass relative or absolute paths.

```bash
vendor/bin/phel format
# Usage:
#   format <paths>...
#
# Arguments:
#   paths                 The file paths that you want to format.
```

[Configuration](/documentation/configuration/) in `phel-config.php`:

```php
<?php
return (new PhelConfig())
    ->setFormatDirs(['src', 'tests']);
```

## Read-Eval-Print Loop

Start a REPL. This is and interactive prompt (stands for Read-Eval-Print Loop). It is very helpful to test out small tasks or to play around with the language itself.

```bash
vendor/bin/phel repl
```

Read more about the [REPL](/documentation/repl) in its own chapter.

## Run a Script

Code can be executed from the command line by calling the run command, followed by the file path or namespace:

```bash
vendor/bin/phel run
# Usage:
#   run [options] [--] <path> [<argv>...]
#
# Arguments:
#   path                  The file path that you want to run.
#   argv                  Optional arguments
#
# Options:
#   -t, --with-time       With time awareness
```

[Configuration](/documentation/configuration/#srcdirs) in `phel-config.php`:

```php
<?php
return (new PhelConfig())
    ->setSrcDirs(['src']);
```

Read more about [running the code](/documentation/getting-started/#running-the-code) in the getting started page.

## Test your Phel Logic

Tests the given files. If no filenames are provided, all tests in the "tests" directory are executed.

```bash
vendor/bin/phel test
# Usage:
#   test [options] [--] [<paths>...]
#
# Arguments:
#   paths                  The file paths that you want to test.
#
# Options:
#   -f, --filter[=FILTER]  Filter by test names.
#       --testdox          Report test execution progress in TestDox format.

```

[Configuration](/documentation/configuration/#testdirs) in `phel-config.php`:

```php
<?php
return (new PhelConfig())
    ->setTestDirs(['tests']);
```

Use the `filter` option to run only the tests that contain that filter.

[Configuration](/documentation/configuration/) in `phel-config.php`:

```php
<?php
return (new PhelConfig())
    ->setTestDirs(['tests']);
```
