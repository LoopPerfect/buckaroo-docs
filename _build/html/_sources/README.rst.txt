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
