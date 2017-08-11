Quickstart
==========

Creating a Project
------------------

The fastest way to get started is to use the Quickstart feature.

First, create a directory for your project:

.. code-block:: bash

   mkdir my-project
   cd my-project

Now, run the Buckaroo quickstart command:

.. code-block:: bash

   buckaroo quickstart

This command will generate a hello-world application, folders for your source-code and a Buck build file. Buckaroo does not require a particular project layout, so feel free to tweak the Buck file.

Let's verify that the project is working as expected:

.. code-block:: bash

   buck run :my-project

You now have everything ready to start installing dependencies.


Adding a dependency
-------------------

Once you have a project file, we can start adding dependencies. Let's add `range-v3 by Eric Niebler <https://github.com/ericniebler/range-v3>`_. range-v3 is a powerful range library for C++ 11 and up.

.. code-block:: bash

   buckaroo install ericniebler/range-v3

Buckaroo will have downloaded the range-v3 source-code from GitHub and installed it locally in your project folder. We can now use the library in a sample application!

Sample Application
------------------

Our example requires some C++ 14 features, so if your compiler does not enable them by default we will need to update the project's `.buckconfig` file.

Update `.buckconfig` to:

.. code-block:: ini

   [cxx]
     cxxflags = -std=c++14

Now, let's update the main.cpp file to a simple range-v3 example:

.. code-block:: c++

   #include <iostream>
   #include <vector>
   #include <range/v3/all.hpp>

   int main() {
     auto const xs = std::vector<int>({ 1, 2, 3, 4, 5 });
     auto const ys = xs
       | ranges::view::transform([](auto x) { return x * x; })
       | ranges::to_vector;
     for (auto const& i : ys) {
       std::cout << i << std::endl;
     }
     return 0;
   }

Run the project again and you will see a list of square numbers, computed by range-v3.

.. code-block:: bash

   buck run :my-project

.gitignore
----------

If you are tracking your project with Git, add the following to your .gitignore:

.. code-block:: none

   /buck-out/
   /.buckd/
   /buckaroo/
   BUCKAROO_DEPS
   .buckconfig.local


Explore Buckaroo
----------------

range-v3 is just one of the many packages already available for Buckaroo. You can browse them on `buckaroo.pm <https://www.buckaroo.pm>`_, request more on `the wishlist <https://github.com/LoopPerfect/buckaroo-wishlist>`_ or :doc:`create your own <package-guide>`!
