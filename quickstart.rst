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

Once you have a project file, we can start adding dependencies. Let's add `range-v3 by Eric Niebler <https://github.com/ericniebler/range-v3>`_. range-v3 is a powerful range library for C++ 11, 14 and 17.

.. code-block:: bash

   buckaroo install ericniebler/range-v3

Buckaroo will have downloaded the range-v3 source-code from GitHub and installed it locally in your project folder. We can now use the library in a sample application!

Sample Program
--------------

Our example requires some C++ 14 features, so if your compiler does not enable it by default we will need to update the project's BUCK file.

Update BUCK to:

.. code-block:: python

   include_defs('//BUCKAROO_DEPS')

   cxx_binary(
     name = 'my-project',
     header_namespace = 'my-project',
     srcs = glob([
       'my-project/src/**/*.cpp',
     ]),
     headers = subdir_glob([
       ('my-project/include', '**/*.hpp'),
       ('my-project/include', '**/*.h'),
     ]),
     compiler_flags = [
       '-std=c++14',
     ],
     deps = BUCKAROO_DEPS,
   )

Now update the main.cpp file to Beast's HTTP example:

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


Explore Buckaroo
----------------

range-v3 is just one of the many packages already available for Buckaroo. You can browse them on `buckaroo.pm <https://www.buckaroo.pm>`_ or request more on `the wishlist <https://github.com/LoopPerfect/buckaroo-wishlist>`_.


.gitignore
----------

If you are tracking your project with Git, add the following to your .gitignore:

.. code-block:: none

   /buck-out/
   /.buckd/
   /buckaroo/
   BUCKAROO_DEPS
   .buckconfig.local
