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

Install adds and installs dependencies to your project.

.. code-block:: bash

   buckaroo install google/gtest

Install can be used to add dependencies to your project. Since introducing a new dependency can result in a versioning conflict, the resolution process is run again. This may overwrite your lock file.

Furthermore you can also ommit the organisation name and list more than one package at the same time

.. code-block:: bash

   buckaroo install gtest boost/asio

Install can also fetch buckaroo compatible projects from github using the following syntax:

.. code-block:: bash

   buckaroo install github+loopperfect/neither


If you do not supply a module name, then the existing dependencies of the project are fetched and installed. If there is no lock file present, then the resolution process will be run first.

.. code-block:: bash

   buckaroo install


Resolve
-------

Resolves the dependencies and regenerates the lock-file (buckaroo.lock.json).
The lock-file specifies the exact versions of all dependencies to ensure the reproducibility of your project.

Resolve is automatically called when installing or uninstalling a dependency.
You may want to run this if one of your dependencies updates.


Uninstall
---------

.. code-block:: bash

   buckaroo uninstall google/gtest

Uninstall can be used to remove a dependency from your project. Note that the remaining dependencies are recomputed since their resolved versions may have changed as a result. This may overwrite your lock file.


Upgrade
-------

.. code-block:: bash

   buckaroo upgrade

Upgrades the installed dependencies to the latest compatible version.


Update
-------

.. code-block:: bash

   buckaroo update

Updates the cook-books installed on your system. This allows you to use benefit from recipe improvements, additions and fixes since you first installed Buckaroo.


Version
-------

.. code-block:: bash

   buckaroo version

Outputs the version of Buckaroo that is installed.


Help
----

.. code-block:: bash

   buckaroo help
