SublimeLinter-contrib-clang-tidy
================================

[![Build Status](https://travis-ci.org/rwols/SublimeLinter-contrib-clang-tidy.svg?branch=master)](https://travis-ci.org/rwols/SublimeLinter-contrib-clang-tidy)

This linter plugin for [SublimeLinter][docs] provides an interface to [clang-tidy][clang-tidy]. It will be used with files that have the __C__, __C++__, __Objective-C__ or __Objective-C++__ syntax.

## Installation
SublimeLinter 3 must be installed in order to use this plugin. If SublimeLinter 3 is not installed, please follow the instructions [here][installation].

### Linter installation
Before using this plugin, you must ensure that `clang-tidy` is installed on your system. To install `clang-tidy`, do the following:

1. Install `clang-tidy` by typing the following in a terminal:

    ```bash
    $ brew install llvm  # OSX
    ```

   or:

    ```bash
    $ sudo apt install clang-tidy  # Ubuntu 16.04
    ```

   This plugin is untested on Windows.

2. Make sure you have a **compilation database** for your project (see the
   section *Settings*)

3. Make sure you have a `.clang-tidy` configuration file for your project.
   The `.clang-tidy` file should live **at the root of your project**. Please
   [read this blog post](http://www.labri.fr/perso/fleury/posts/programming/using-clang-tidy-and-clang-format.html) to learn how to create a `.clang-tidy`
   file.

**Note:** This plugin requires `clang-tidy` __1.0__ or later.

### Linter configuration
In order for `clang-tidy` to be executed by SublimeLinter, you must ensure that its path is available to SublimeLinter. Before going any further, please read and follow the steps in [“Finding a linter executable”][linter-finding] through “Validating your PATH” in the documentation.

Once you have installed and configured `clang-tidy`, you can proceed to install the SublimeLinter-contrib-clang-tidy plugin if it is not yet installed.

### Plugin installation
Please use [Package Control][pc] to install the linter plugin. This will ensure that the plugin will be updated when new versions are available. If you want to install from source so you can modify the source code, you probably know what you are doing so we won’t cover that here.

To install via Package Control, do the following:

1. Within Sublime Text, bring up the [Command Palette][cmd] and type `install`. Among the commands you should see `Package Control: Install Package`. If that command is not highlighted, use the keyboard or mouse to select it. There will be a pause of a few seconds while Package Control fetches the list of available plugins.

1. When the plugin list appears, type `clang-tidy`. Among the entries you should see `SublimeLinter-contrib-clang-tidy`. If that entry is not highlighted, use the keyboard or mouse to select it.

## Settings
For general information on how SublimeLinter works with settings, please see [Settings][settings]. For information on generic linter settings, please see [Linter Settings][linter-settings].

In order for linting to work, **you need a compilation database**. This is a JSON
file with the name **compile_commands.json**. It can be generated by **CMake**
by specifying `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` on the command-line when
you invoke `cmake`.

In order to let this plugin know where the compilation database is, **add the
following entry to your `.sublime-project`**:

```javascript
{
    "folders":
    [
        // ...
    ],
    "settings":
    {
        // ...
        "SublimeLinter.linters.clangtidy.compile_commands": "${project_path}/PATH/TO/YOUR/BUILD/DIR"
        // ...
    }
}
```
The plugin **will not work** if this setting is not present.

Remember: header files are never compiled. Therefore, **header files are not
in the compilation database** (by default). So, **clang-tidy will not work with
header files**. You may try to use [this python package][compdb] to enhance your existing compile_commands.json with additional header files.

## Usage
Upon opening a suitable file, and given that the compilation database as well
as the `.clang-tidy` file are present in the right locations, SublimeLinter
will run the clang-tidy linter. Note that this means that the source file is
being compiled by clang-tidy. So it may take a while before messages start to
show up.
Since clang-tidy works on source files, the clang-tidy linter will only run when
you open a source file or when you save a source file. The clang-tidy linter
**will not lint when you edit the file**. It will only lint **during load and
save**.

## Recommended Other Plugins
- [Clang Format](https://packagecontrol.io/packages/Clang%20Format)

## Contributing
If you would like to contribute enhancements or fixes, please do the following:

1. Fork the plugin repository.
1. Hack on a separate topic branch created from the latest `master`.
1. Commit and push the topic branch.
1. Make a pull request.
1. Be patient.  ;-)

Please note that modifications should follow these coding guidelines:

- Indent is 4 spaces.
- Code should pass flake8 and pep257 linters.
- Vertical whitespace helps readability, don’t be afraid to use it.
- Please use descriptive variable names, no abbreviations unless they are very well known.

Thank you for helping out!

[clang-tidy]: http://clang.llvm.org/extra/clang-tidy
[compdb]: https://github.com/Sarcasm/compdb
[docs]: http://sublimelinter.readthedocs.org
[installation]: http://sublimelinter.readthedocs.org/en/latest/installation.html
[locating-executables]: http://sublimelinter.readthedocs.org/en/latest/usage.html#how-linter-executables-are-located
[pc]: https://sublime.wbond.net/installation
[linter-finding]: http://sublimelinter.readthedocs.org/en/latest/troubleshooting.html#finding-a-linter-executable
[cmd]: http://docs.sublimetext.info/en/sublime-text-3/extensibility/command_palette.html
[settings]: http://sublimelinter.readthedocs.org/en/latest/settings.html
[linter-settings]: http://sublimelinter.readthedocs.org/en/latest/linter_settings.html
[inline-settings]: http://sublimelinter.readthedocs.org/en/latest/settings.html#inline-settings
