Caching
=======

Buckaroo will cache files downloaded from the network and clones of Git repositories. This prevents duplicate work, and can even enable Buckaroo to work offline in some cases.


Clearing the Cache
------------------

If you would like to reclaim some disc space, it is safe to delete the Buckaroo cache folder. The location of the cache folder will vary by platform:


macOS
~~~~~

.. code-block:: bash

   ~/Library/Caches/Buckaroo


Linux
~~~~~

.. code-block:: bash

   ~/.cache/Buckaroo


Windows
~~~~~~~

.. code-block:: bat

   C:\Users\<USERNAME>\Local Settings\Application Data\Buckaroo\Cache


Any Other Platform
~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   ~/.buckaroo/caches
