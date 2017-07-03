GitHub Integration
==================

Buckaroo has GitHub integration, which allows for recipes to exist as GitHub projects. To use a GitHub project as a recipe, the following conditions must be met:

 - The GitHub project must have at least one tag, which is a semantic version (e.g. "v1.0")
 - The GitHub project must contain a `buckaroo.json` file at the root level.

If you would like to create a GitHub recipe, see :doc:`the GitHub packaging guide <github-package-guide>`.

A GitHub dependency is referred to with the prefix :code:`github+`. So, for example, to install :code:`LoopPerfect/neither` you would run:

.. code-block:: bash

   buckaroo install github+loopperfect/neither

Buckaroo will generate the Git URL from the project name and owner, fetch the repository and read the :code:`buckaroo.json` file.


Transitive Dependencies
-----------------------

GitHub recipes can even have transitive dependencies! These are specified using the usual syntax in the project file of the GitHub repository. When resolving dependencies, Buckaroo will read this project file to generate further recipes to resolve. Note that the lock file of the dependency is ignored, and the cookbook of the current system is used to resolve the dependencies of the GitHub recipe.


What if a GitHub project is deleted, or a tag is changed?
---------------------------------------------------------

Once a GitHub dependency has been resolved, the exact commit hash of the tag is written to the lock file. This means that future installations will use the same version that was resolved on the first install. If this version becomes unavailable later, the resolution process can be re-run to fetch the current available version.
