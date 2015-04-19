# Luacheck

[![Build Status](https://travis-ci.org/mpeterv/luacheck.png?branch=master)](https://travis-ci.org/mpeterv/luacheck)
[![Windows build status](https://ci.appveyor.com/api/projects/status/pgox2vvelagw1fux/branch/master?svg=true&passingText=Windows%20build%20passing&failingText=Windows%20build%20failing)](https://ci.appveyor.com/project/mpeterv/luacheck/branch/master)
[![Coverage Status](https://coveralls.io/repos/mpeterv/luacheck/badge.svg?branch=master)](https://coveralls.io/r/mpeterv/luacheck?branch=master)
[![License](http://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)

## Contents

* [Overview](#overview)
* [Installation](#installation)
* [Editor support](#editor-support)
* [Documentation](#documentation)
* [Development](#development)
* [Building and testing](#building-and-testing)
* [License](#license)

## Overview

Luacheck is a static analyzer and a linter for [Lua](http://www.lua.org). Luacheck detects various issues such as usage of undefined global variables, unused variables and values, accessing uninitialized variables, unreachable code and more. Most aspects of checking are configurable: there are options for defining custom project-related globals, for selecting set of standard globals (version of Lua standard library), for filtering warnings by type and name of related variable, etc. The options can be used on the command line, put into a config or directly into checked files as Lua comments.

Luacheck supports checking Lua files using syntax of Lua 5.1, Lua 5.2, Lua 5.3 and LuaJIT 2.0. Luacheck itself is written in Lua and runs on all of mentioned Lua versions.

## Installation

The easiest way to install Luacheck is to use [LuaRocks](http://luarocks.org). From your command line run the following command:

```bash
$ luarocks install luacheck # prepend with sudo if necessary
```

If it is not possible to install [LuaFileSystem](http://keplerproject.github.io/luafilesystem/) in your environment, use `luarocks install luacheck --deps-mode=none`.

For parallel checking Luacheck requires [LuaLanes](https://github.com/LuaLanes/lanes), which can be installed using LuaRocks as well. On Lua 5.3, install bleeding edge version:

```bash
$ git clone https://github.com/LuaLanes/lanes
$ cd lanes
$ luarocks make lanes-3.9.6-1.rockspec # prepend with sudo if necessary
$ cd ..
```

### Manual installation

For manual installation, only a Lua interpreter binary is required.

1. Download and unpack latest Luacheck release ([.zip](https://github.com/mpeterv/luacheck/archive/0.10.0.zip) [.tar.gz](https://github.com/mpeterv/luacheck/archive/0.10.0.tar.gz)).
2. Run `install.lua <path>` script using the Lua interpreter. If Lua interpreter is not in `PATH`, invoke it using absolute path.
3. Add `<path>/bin` to PATH or run Luacheck as `<path>/bin/luacheck`.

## Basic usage

After Luacheck is installed, run `luacheck` program from the command line. Pass a list of files, [rockspecs](https://github.com/keplerproject/luarocks/wiki/Rockspec-format) or directories (requires LuaFileSystem) to be checked:

```
$ luacheck src extra_file.lua another_file.lua
Checking src/good_code.lua               OK
Checking src/bad_code.lua                Failure

    src/bad_code.lua:3:23: unused variable length argument
    src/bad_code.lua:7:10: setting non-standard global variable embrace
    src/bad_code.lua:8:10: variable opt was previously defined as an argument on line 7

Checking src/python_code.lua             Syntax error

    src/python_code.lua:1:6: expected '=' near '__future__'

Checking extra_file.lua                  Failure

    extra_file.lua:3:18: unused argument baz
    extra_file.lua:4:8: unused loop variable i
    extra_file.lua:13:7: accessing uninitialized variable a
    extra_file.lua:14:1: value assigned to variable x is unused
    extra_file.lua:21:7: variable z is never accessed

Checking another_file.lua                Failure

    another_file.lua:2:7: unused variable height
    another_file.lua:3:7: accessing undefined variable heigth

Total: 10 warnings / 1 error in 5 files
```

For more info, see [documentation](#documentation).

## Editor support

There are a few plugins which allow using Luacheck directly inside an editor, showing warnings inline:

* For Vim, [Syntastic](https://github.com/scrooloose/syntastic/) contains [luacheck checker](https://github.com/scrooloose/syntastic/wiki/Lua%3A---luacheck);
* For Sublime Text 3 there is [SublimeLinter-luacheck](https://sublime.wbond.net/packages/SublimeLinter-luacheck) which requires [SublimeLinter](http://sublimelinter.readthedocs.org/en/latest/);
* For Atom there is [linter-luacheck](https://atom.io/packages/linter-luacheck) which requires [AtomLinter](https://github.com/AtomLinter/Linter);
* For Emacs, [Flycheck](http://www.flycheck.org/) contains [luacheck checker](http://www.flycheck.org/manual/latest/Supported-languages.html#Lua).

## Documentation

Documentation is available [online](http://luacheck.readthedocs.org). If Luacheck has been installed using LuaRocks, it can be browsed offline using `luarocks doc luacheck` command.

## Development

Luacheck is currently in development. The latest released version is 0.10.0. The interface of the `luacheck` module may change between minor releases. The command line interface is fairly stable.

Use the Luacheck issue tracker on GitHub to submit bugs, suggestions and questions. Any pull requests are welcome, too.

## Building and testing

After the Luacheck repo is cloned and changes are made, run `luarocks make` (optionally prepended with `sudo`) from its root directory to install dev version of Luacheck. To test Luacheck, ensure that you have [busted](http://olivinelabs.com/busted) installed and run `busted spec`.

## License

```
The MIT License (MIT)

Copyright (c) 2014 - 2015 Peter Melnichenko

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
