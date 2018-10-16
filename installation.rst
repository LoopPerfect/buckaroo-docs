Installation
============

Buckaroo is available for macOS, Linux and Windows (preview).

macOS
-----

Buckaroo can be installed using `Homebrew <https://brew.sh/>`_.

Add Facebook's tap so that Homebrew can find Buck.

.. code-block:: bash

   brew tap facebook/fb
   brew tap loopperfect/lp
   brew install loopperfect/lp/buckaroo

The Homebrew formula will install Buck and Java, if required.

Verify your installation with:

.. code-block:: bash

   buckaroo version

Finally, fetch the cookbook with:

.. code-block:: bash

   buckaroo update

Linux
-----

Debian and Ubuntu via .deb
~~~~~~~~~~~~~~~~~~~~~~~~~~

We provide a `.deb` file for Debian and Ubuntu. To install it, download `buckaroo.deb <https://github.com/LoopPerfect/buckaroo/releases>`_ and double-click to install.

Alternatively, you can use the command-line:

.. code-block:: bash

   wget -O buckaroo.deb 'https://github.com/LoopPerfect/buckaroo/releases/download/v1.4.1/buckaroo.deb' 
   sudo dpkg -i buckaroo.deb


Finally, fetch the cookbook with:

.. code-block:: bash

   buckaroo update

Linuxbrew
~~~~~~~~~

Buckaroo can be installed using `Linuxbrew <http://linuxbrew.sh/>`_.

Add Facebook's tap so that Linuxbrew can find Buck.

.. code-block:: bash

   brew tap facebook/fb
   brew tap loopperfect/lp
   brew install loopperfect/lp/buckaroo

The Linuxbrew formula will install Buck and Java, if required.

Verify your installation with:

.. code-block:: bash

   buckaroo version

Finally, fetch the cookbook with:

.. code-block:: bash

   buckaroo update


Windows (preview)
-----------------

Ensure that you have `Buck <https://buckbuild.com/>`_ installed, then clone the Buckaroo source-code from GitHub:

.. code-block:: bash

   git clone git@github.com:njlr/buckaroo.git
   cd buckaroo
   git checkout tags/v1.0.0

Build Buckaroo with Buck:

.. code-block:: bash

   buck build :buckaroo-cli

Buck will output a runnable Jar file in the output folder:

.. code-block:: bash

   java -jar .\\buck-out\\gen\\buckaroo-cli.jar

Ensure that this command is on your PATH.

Finally, fetch the cookbook with:

.. code-block:: bash

   buckaroo update


Analytics
---------

By default, Buckaroo will report usage statistics to our servers. These logs allow us to improve Buckaroo by targeting real-world usage. All logs are transferred over HTTPS and are not shared with any third-party.

What is Shared?
~~~~~~~~~~~~~~~

The analytics events are as follows:

.. code-block:: javascript

   {
     session, // Random UUID generated on installation
     data: {
       os, // The OS name, e.g. "macOS"
       version, // The version of Buckaroo installed
       command // The command sent to Buckaroo
     }
   }

If in doubt, please refer to the `source-code of Buckaroo <https://github.com/LoopPerfect/buckaroo>`_ or `drop us an email <mailto:buckaroo@loopperfect.com>`_.


Disabling Analytics
~~~~~~~~~~~~~~~~~~~

If you wish to disable analytics, follow these steps:

1. Launch Buckaroo at least once:

.. code-block:: bash

   buckaroo version

2. Open the `buckaroo.json` file in your Buckaroo home folder:

.. code-block:: bash

   open ~/.buckaroo/config.json

3. Remove the property `"analytics"`. For example:

.. code-block:: javascript

   {
     "cookBooks": [
       {
         "name": "buckaroo-recipes",
         "url": "git@github.com:loopperfect/buckaroo-recipes.git"
       }
     ]
   }
