Command Line Interface
======================

Buckaroo provides a command-line interface for managing your project's dependencies. The following commands are the recommended way to use Buckaroo.

Init
----

.. code-block:: bash

   buckaroo init

Init is used to generate a project file in the current directory.

Quickstart
----------

.. code-block:: bash

   buckaroo quickstart

Quickstart is similar to Init, but also generates the necessary boiler-plate for a new C++ project. You should use Quickstart when starting a new project.

Resolve
-------

.. code-block:: bash

   buckaroo resolve

Reads the project file in the working directory and runs the dependency resolution algorithm, storing the results in the lock file. If there is already a lock file present, then it is overwritten. No dependencies are actually installed.

Install
-------

.. code-block:: bash

   buckaroo install google/gtest

Install can be used to add dependencies to your project. Since introducing a new dependency can result in a versioning conflict, the resolution process is run again. This may overwrite your lock file.

If you do not supply a module name, then the existing dependencies of the project are fetched and installed. If there is no lock file present, then the resolution process will be run first.

.. code-block:: bash

   buckaroo install


Uninstall
---------

.. code-block:: bash

   buckaroo uninstall google/gtest

Uninstall can be used to remove a dependency from your project. Note that the remaining dependencies are recomputed since their resolved versions may have changed as a result. This may overwrite your lock file. 


Upgrade
-------

.. code-block:: bash

   buckaroo upgrade

Upgrades the cook-books installed on your system. This allows you to use benefit from recipe improvements, additions and fixes since you first installed Buckaroo.


Version
-------

.. code-block:: bash

   buckaroo version

Outputs the version of Buckaroo that is installed.


Help
----

.. code-block:: bash

   buckaroo help
