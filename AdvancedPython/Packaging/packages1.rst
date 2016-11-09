Introduciton to package management
==================================

--------------------------------------------------------------------------

Python Package Index
--------------------

also known as ``pypi`` or "The cheeseshop" is a repository of open-source third-party packages.

http://pypi.python.org/pypi

--------------------------------------------------------------------------

Packages
--------

A package can be either a **Wheel** or an **Egg**, but Wheel is currently considered the standard for built and binary packaging for Python.

http://python-packaging-user-guide.readthedocs.org/en/latest/wheel_egg/

--------------------------------------------------------------------------

``easy_install``
----------------

... is a deprecated tool for installing packages from the Python

* automatically downloads, builds, installs packages
* looks in the `Python Packaging Index <http://pypi.python.org/pypi>`_
* installs a Python Egg

--------------------------------------------------------------------------

``pip``
--------

... is an enhanced tool for installing packages from the Python.

.. code:: bash

    $ pip install SomePackage           # latest version
    $ pip install SomePackage==1.0.4    # specific version
    $ pip install "SomePackage>=1.0.4"  # minimum version
    $ pip install --upgrade SomePackage # upgrade

--------------------------------------------------------------------------

* ``pip`` is part of the standard library from v3.4
* All packages are downloaded before installation. Partially-completed installation doesn’t occur as a result.
* The code is relatively concise and cohesive, making it easier to use programmatically.
* Native support for other version control systems (Git, Mercurial and Bazaar)
* Uninstallation of packages.
* Simple to define fixed sets of requirements and reliably reproduce a set of packages.


--------------------------------------------------------------------------

* ``install`` -- install package
    * ``--upgrade``
    * ``--user`` --  uses ``$PYTHONUSERBASE``
* ``uninstall`` -- remove package
* ``list`` -- list installed packages
* ``search`` -- search for packages
* ``show`` -- package details
* ``freeze`` -- output installed packages in a requirement file
* ``wheel`` -- build a wheel file from a requirements file

--------------------------------------------------------------------------

Dependency management of ``pip``:

``requirements.txt``

.. code-block:: none

    MyApp
    Framework==0.9.4
    Library>=0.2

``$ pip install -r requirements.txt``

``$ pip freeze > requirements.txt``

--------------------------------------------------------------------------

Virtual environments
--------------------

Isolated working environments containing a copy of a Python interpreter.

* no need to install packages globally
* one can manage different versions of the same package

Available tools:

* ``venv`` -- boundled in Python 3.4
* ``virtualenv`` -- http://virtualenv.readthedocs.org/en/latest/

-----------------------------------------------------

Usage:

.. code-block:: bash

    $ virtualenv mytest
    $ source mytest/bin/activate
    (mytest)$ deactivate

    $ pyvenv mytest
    $ source mytest/bin/activate
    (mytest)$ deactivate


--------------------------------------------------------------------------

``conda``
---------

* is an open source platform independent package management system and environment management system for installing multiple versions of software packages and their dependencies and switching easily between them.
*  is also an environment manager application. A conda environment is a directory that contains a specific collection of conda packages that you have installed.

--------------------------------------------------------------------------

``conda`` package management
''''''''''''''''''''''''''''

.. code:: bash

    $ conda install SomePackage
    $ conda search SomePackage
    $ conda update SomePackage
    $ conda remove SomePackage

--------------------------------------------------------------------------

``conda`` environments
''''''''''''''''''''''

.. code:: bash

    $ conda-env create --name <env> # Creates environment based on a environment file
    $ conda-env remove --name <env> # Export a given environment
    $ conda-env export # Export a given environment
    $ conda-env list   # Lists conda environments


Usage:

.. code:: bash

    $ conda-env create mytest
    $ source activate
    (mytest)$ source deactivate

--------------------------------------------------------------------------

Demo
----

``$ conda create -n py35 python=3.5``
