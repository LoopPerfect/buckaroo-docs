Anatomy of a Recipe
===================

A Buckaroo recipe is a file that describes a module that can be imported into your projects. Recipes are encoded as JSON.


Example
-------

For example, here's a recipe for the `Beast <https://github.com/vinniefalco/beast/>`_ HTTP library:


.. code-block:: javascript

   {
     "name": "Beast",
     "license": "BSL-1.0",
     "url": "https://github.com/vinniefalco/beast",
     "github": {
       "owner": "vinniefalco",
       "project": "beast"
     },
     "versions": {
       "0.0.1": {
         "source": {
           "url": "https://github.com/vinniefalco/Beast/archive/6d5547a32c50ec95832c4779311502555ab0ee1f.zip",
           "sha256": "8a600dfa3394164f79ad7dfa6942d8d4b6c6c7e5b8cc9b5f82519b682db25aae",
           "subPath": "Beast-6d5547a32c50ec95832c4779311502555ab0ee1f"
         },
         "buck": {
           "url": "https://raw.githubusercontent.com/njlr/Beast/71d1bde64bf5ee52579441b00ad446959231d8d2/BUCK",
           "sha256": "1dce5d9f5c883e193e54c2dfc033a5485b9e8e87bb34d8c38ab03ed148ccd968"
         },
         "dependencies": {
           "boost/range": "1.63.0",
           "boost/intrusive": "1.63.0",
           "boost/lexical-cast": "1.63.0",
           "boost/math": "1.63.0",
           "boost/system": "1.63.0",
           "boost/asio": "1.63.0"
         }
       }
     }
   }


Name
~~~~

.. code-block:: javascript

   "name": "Beast",

This is the friendly name of the package.

Note that the file-name of the recipe is the identifier used by the :code:`install` command, so the :code:`name` field may contain spaces, etc.


Meta-data
~~~~~~~~~

.. code-block:: javascript

   "license": "BSL-1.0",
   "url": "https://github.com/vinniefalco/beast",
   "github": {
     "owner": "vinniefalco",
     "project": "beast"
   },

This optional meta-data is used to generate the pages on `buckaroo.pm <https://www.buckaroo.pm>`_. Note that the license should be a comma-separated list of `SPDX codes <https://spdx.org/licenses/>`_.


Versions
~~~~~~~~

.. code-block:: javascript

     "versions": {

The :code:`versions` element is a dictionary of semantic versions to source locations.

.. code-block:: javascript

   "0.0.1": {
     "source": {
       "url": "https://github.com/vinniefalco/Beast/archive/6d5547a32c50ec95832c4779311502555ab0ee1f.zip",
       "sha256": "8a600dfa3394164f79ad7dfa6942d8d4b6c6c7e5b8cc9b5f82519b682db25aae",
       "subPath": "Beast-6d5547a32c50ec95832c4779311502555ab0ee1f"
     },
     "buck": {
       "url": "https://raw.githubusercontent.com/njlr/Beast/71d1bde64bf5ee52579441b00ad446959231d8d2/BUCK",
       "sha256": "1dce5d9f5c883e193e54c2dfc033a5485b9e8e87bb34d8c38ab03ed148ccd968"
     },
     "dependencies": {
       "boost/range": "1.63.0",
       "boost/intrusive": "1.63.0",
       "boost/lexical-cast": "1.63.0",
       "boost/math": "1.63.0",
       "boost/system": "1.63.0",
       "boost/asio": "1.63.0"
     }
   }

Each version object contains information on how to fetch the source-code. In case the source-code does not contain a :code:`BUCK` file, one may be injected using the information in the :code:`buck` element.


Source
~~~~~~

.. code-block:: javascript

   "source": {
     "url": "https://github.com/vinniefalco/Beast/archive/6d5547a32c50ec95832c4779311502555ab0ee1f.zip",
     "sha256": "8a600dfa3394164f79ad7dfa6942d8d4b6c6c7e5b8cc9b5f82519b682db25aae",
     "subPath": "Beast-6d5547a32c50ec95832c4779311502555ab0ee1f"
   },

Every :code:`source` should point to a zip-file containing the source-code of the module. It is hashed to ensure integrity, so always choose a URL that is stable.

The :code:`subPath` element can be used to change the root of the source-code.

For example, suppose the zip-file has this structure:

.. code-block:: guess

   .
   +-- module.zip
       +-- sources
           +-- include
               +-- math.hpp
               +-- utils.hpp

If the :code:`subPath` is :code:`"sources/include"`, then the extracted code would be:

.. code-block:: guess

   .
   +-- math.hpp
   +-- utils.hpp

This feature is particularly useful for GitHub, which puts source-code into a sub-folder called  :code:`<project>-<commit>`.


Buck
~~~~

.. code-block:: javascript

   "buck": {
     "url": "https://raw.githubusercontent.com/njlr/Beast/71d1bde64bf5ee52579441b00ad446959231d8d2/BUCK",
     "sha256": "1dce5d9f5c883e193e54c2dfc033a5485b9e8e87bb34d8c38ab03ed148ccd968"
   },

The :code:`buck` element points to a remote Buck definition. If present, the remote :code:`BUCK` file gets saved into the root folder of the source-code. This allows us to support packages that do not currently support Buck.

The :code:`buck` element is only required when the source-code does not already contain a :code:`BUCK` file.


Dependencies
~~~~~~~~~~~~

.. code-block:: javascript

   "dependencies": {
     "boost/range": "1.63.0",
     "boost/intrusive": "1.63.0",
     "boost/lexical-cast": "1.63.0",
     "boost/math": "1.63.0",
     "boost/system": "1.63.0",
     "boost/asio": "1.63.0",
     "github+loopperfect/neither": "*"
   }

The :code:`dependencies` element defines the modules that the recipe requires to build. These are of the following format:

.. code-block:: guess

   (<source>+)?<owner>/<project>: <version>

The source section is optional and is used to refer to recipes outside of the official cookbook. The most common source is GitHub (see :doc:`github`), and more will be added over time. 

A small DSL is provided for versioning:

.. code-block:: guess

   *                    // Any version
   v1                   // Exactly version 1.0.0
   2                    // Exactly version 2.0.0
   1.2                  // Exactly version 1.2.0
   1.2.3                // Exactly version 1.2.3
   1.0.1 - 4.3          // Between 1.0.1 and 4.3 inclusive
   [ 7.2, 7.3, 8 ]      // Either 7.2.0, 7.3.0 or 8.0.0
   >= 4.7               // Version 4.7 or greater
   <= 6.5.1             // Version 6.5.1 or greater

When multiple versions of a dependency can be resolved, the higher version is always chosen.
