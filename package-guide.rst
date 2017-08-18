Creating a Package
=========================

This is a guide for creating a Buckaroo recipe from a GitHub, BitBucket or GitLab project. This is the quickest way to create and manage a package that already lives in source-control. It is also recommended, since it allows you to control updates to your recipe.

For this guide, we will be adding Buckaroo support for `an example project
<https://github.com/LoopPerfect/buckaroo-github-example>`_. However, the steps are generic, so you should be able to follow them using your own project.

If you would like to jump straight to a working GitHub recipe, take a look at `LoopPerfect/neither
<https://github.com/LoopPerfect/neither>`_. The important files are :code:`BUCK` and :code:`buckaroo.json`.


Requirements
------------

To follow this guide, you will need the following:

 - Git
 - A `GitHub <https://www.github.com/>`_ account
 - Buckaroo (see :doc:`installation`)
 - Buck

The steps are nearly identical for BitBucket and GitLab.


1. Fork the example project
---------------------------

Fork `the example project <https://github.com/LoopPerfect/buckaroo-github-example>`_ on GitHub.


2. Fetch the Project
--------------------

Next, fetch your fork from GitHub using Git:

.. code-block:: bash

   git clone https://github.com/<YOUR_GITHUB_USERNAME>/buckaroo-github-example.git
   cd buckaroo-github-example


3. Ensure that the project builds with Buck
-------------------------------------------

All Buckaroo packages build with Buck, so we need to make sure that the :code:`BUCK` files are correct.

In our example, we have a single library called :code:`example`. Try building it using Buck:

.. code-block:: bash

   buck build :example

If you are using your own project that does not yet build with Buck, then you will need to write the appropriate Buck files. Head over to `the Buck website
<https://buckbuild.com/>`_ for more guidance, or you can follow `this article on Hackernoon <https://hackernoon.com/how-to-create-a-buck-based-c-c-project-38b85273d6a6>`_.


.. note::

   To work with Buckaroo, your Buck target must be marked :code:`PUBLIC`. To do this, simply add the following to your target definition:

   .. code-block:: python

      visibility = [
        'PUBLIC',
      ]


4. Create the Project File
--------------------------

Now that we are sure the project can build with Buck, we need to create a project file. The project file gives Buckaroo various bits of meta-data about your recipe.

.. code-block:: bash

   buckaroo init

This will create a :code:`buckaroo.json` file. Open it, and ensure that the target field points to your Buck target.

For our example, the target is :code:`"example"`. The final :code:`buckaroo.json` file might look like this:

.. code-block:: javascript

   {
     "name": "buckaroo-github-example",
     "target": "example"
   }

Commit the project file to GitHub:

.. code-block:: bash

   git add buckaroo.json
   git commit -m "Adds Buckaroo project file"
   git push


5. Create a release
-------------------

Head over to the GitHub web-page for your project and create a release. It is important that you name the release in a format that Buckaroo understands. Buckaroo expects a version number prefixed with a :code:`"v"`. Some valid names are:

 - :code:`"v1.0.0"`
 - :code:`"v0.2"`
 - :code:`"v3"`


For this guide, we will name the release :code:`"v0.1.0"`.


6. Test your package
--------------------

Create a new folder alongside your project directory:

.. code-block:: bash

   cd ../
   mkdir test
   cd test

Create a Buckaroo project in this directory:

.. code-block:: bash

   buckaroo quickstart

Now we can install the GitHub recipe:

.. code-block:: bash

   buckaroo install github+<YOUR_GITHUB_USERNAME>/buckaroo-github-example

You should see a few changes to your working directory:

 - :code:`buckaroo.lock.json` will contain an exact version of your GitHub recipe
 - :code:`buckaroo/` will contain a copy of your recipe
 - :code:`BUCKAROO_DEPS` will have been generated, ready to include in your :code:`BUCK` file.

Open :code:`test/src/main.cpp` and update it to use your recipe:

.. code-block:: c++

   #include <iostream>
   #include <sum.hpp>

   int main() {
     std::cout << "sum(1, 2) = " << sum(1, 2) << std::endl;
     return 0;
   }

Now run your program using Buck:

.. code-block:: bash

   buck run :test

If everything has worked correctly, you will see the following output:

.. code-block:: bash

   sum(1, 2) = 3
