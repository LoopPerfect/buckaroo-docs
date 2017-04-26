# Buckaroo

## Introduction

Buckaroo is a dependency manager for C/C++. Using Buckaroo, it is easy to add external modules to your project in a controlled and cross-platform manner.

To use Buckaroo, you will also need to install [Buck](https://buckbuild.com/). Buck is a build system developed and maintained by Facebook, and it is used by all Buckaroo packages.


## Installation

Buckaroo is available for macOS, Linux and Windows (preview).

### macOS

Buckaroo can be installed using [Homebrew](https://brew.sh/).

```
brew install --HEAD loopperfect/lp/buckaroo
```

The Homebrew formula will install Buck and Java, if required.

Verify your installation with:

```
buckaroo version
```

### Linux



### Windows (preview)

Ensure that you have [Buck](https://buckbuild.com/) installed, then clone the Buckaroo source-code from GitHub:

```
git clone git@github.com:njlr/buckaroo.git
cd buckaroo
```

Build Buckaroo with Buck:

```
buck build
```

Buck will output a runnable Jar file in the output folder:

```
java -jar .\\buck-out\\gen\\buckaroo-cli.jar
```


## Quickstart

The fastest way to get started is to use the Quickstart feature. Create a directory for your project then run:

```
buckaroo quickstart
```

This command will generate a hello-world application, folders for your source-code and a Buck build file. Buckaroo does not require a particular project layout, so feel free to tweak the Buck file.

You now have everything ready to start installing dependencies.


## Creating a Project File

A project that uses Buckaroo dependencies must include a `buckaroo.json` file in its root folder. This is called the project file. The project file tells Buckaroo which modules the project requires and their versions.

If you used the Quickstart command, then there will already be a project file in your working directory. However, to generate only a project file, open your terminal in your project folder and run:

```
buckaroo init
```


## Adding a dependency

Once you have a project file, we can start adding dependencies. Let's add [range-v3  by Eric Niebler](https://github.com/ericniebler/range-v3).

```
buckaroo install ericniebler/range-v3
```

You will notice some new files have been created in your project folder.

### BUCKAROO_DEPS

This file contains the dependency list that is imported by your Buck build file.

### buckaroo/

This folder contains the source-code of all dependencies that have been downloaded by Buckaroo. You can regenerate this folder by running `buckaroo install`.

### .buckconfig.local

This file tells Buck where to find the dependencies downloaded by Buckaroo.


### Configuring .gitignore

It is important to add generated files to your `.gitignore`. The following rules will cover them:

```
/buck-out/
/.buckd/
/buckaroo/
BUCKAROO_DEPS
.buckconfig.local
```

## FAQ

### Which packages are available?

You can browse officially maintained packages on [the Buckaroo website](http://www.buckaroo.pm). If there is a package you would like to use but is unavailable, please [log an issue on the wish-list](https://github.com/LoopPerfect/buckaroo-wishlist/issues/new) and we will work to make it available.

### Can I host private packages?

Yes, you can. Simply add a recipe to your `config.json` file (it's inside `~/.buckaroo/`). Note that other developers on your team must also edit their `config.json`.

### How can I get help?

We are very active on [GitHub](https://github.com/LoopPerfect/buckaroo) and [StackOverflow](stackoverflow.com/questions/tagged/buckaroo). If you run into any issues, please report an issue and we will respond as soon as possible. We prefer to fix issues on public pages because it builds a knowledge base that others can use.

### What is the relationship between Buck and Buckaroo?

Buck is an open-source build system developed and maintained by Facebook. Buckaroo is a package manager for C/C++ developed and maintained by LoopPerfect. All Buckaroo dependencies use Buck as a build system, however Buckaroo is strictly a layer on top of Buck.
