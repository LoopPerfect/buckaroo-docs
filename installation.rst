Installation
============

Buckaroo is available for macOS, Linux and Windows (preview).

macOS
-----

Buckaroo can be installed using `Homebrew <https://brew.sh/>`_.

.. code-block:: bash

   brew install --HEAD loopperfect/lp/buckaroo

The Homebrew formula will install Buck and Java, if required.

Verify your installation with:

.. code-block:: bash

   buckaroo version

Linux
-----

Windows (preview)
-----------------

Ensure that you have `Buck <https://buckbuild.com/>`_ installed, then clone the Buckaroo source-code from GitHub:

.. code-block:: bash

   git clone git@github.com:njlr/buckaroo.git
   cd buckaroo

Build Buckaroo with Buck:

.. code-block:: bash

   buck build

Buck will output a runnable Jar file in the output folder:

.. code-block:: bash

   java -jar .\\buck-out\\gen\\buckaroo-cli.jar
