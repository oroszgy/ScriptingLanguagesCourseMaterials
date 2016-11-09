``argparse``
------------

The argparse module makes it easy to write user-friendly command-line interfaces. The program defines what arguments it requires, and argparse will figure out how to parse those out of ``sys.argv```. The argparse module also automatically generates help and usage messages and issues errors when users give the program invalid arguments.

------------------------------------------------------

.. code-block:: python

    import argparse
    parser = argparse.ArgumentParser(description='This is a sample program')
    parser.add_argument("echo")
    args = parser.parse_args()

    print(args.echo)

``$ python sample.py echo``

------------------------------------------------------

Examples
~~~~~~~~

Positional arguments
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    parser.add_argument("square", type=int,
                        help="display a square of a given number")

    parser.add_argument('dir', nargs='?', default=os.getcwd())

------------------------------------------------------

Optional arguments
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    parser.add_argument("-v", "--verbosity", type=int,
                    help="increase output verbosity")

    parser.add_argument("-v", "--verbose",
                        help="increase output verbosity",
                        action="store_true")

------------------------------------------------------

Package components
------------------

``__init__.py``
~~~~~~~~~~~~~~~~~

* packages are directories having a ``__init__.py``
* it was necessary for packages before Python 3.3
* since then it became optional: any directory can be a package thus can be imported
* rule of thumb: use ``__init__.py`` if you want create a package

------------------------------------------------------

``__main__.py``
~~~~~~~~~~~~~~~~~

.. code-block:: None

    myproject/
    |-- simple
      |-- __main__.py

    file: __main__.py

       print("hello world")

    $ python -m simple
    hello world



------------------------------------------------------

Relative imports
~~~~~~~~~~~~~~~~~

* ``from . import something``
* ``from .. import something``
* ``from ... import something``

But ``__name__`` is used to resolve the hierarchy!

------------------------------------------------------

``~$ python -m package.subpackage1.moduleX``

.. code-block:: none

    ~/package/
        __init__.py
        subpackage1/
            __init__.py
            moduleX.py     <==
            moduleY.py
        subpackage2/
            __init__.py
            moduleZ.py
        moduleA.py

------------------------------------------------------

.. code-block:: python

    from .moduleY import spam
    from .moduleY import spam as ham
    from . import moduleY
    from ..subpackage1 import moduleY
    from ..subpackage2.moduleZ import eggs
    from ..moduleA import foo
    from ...package import bar

------------------------------------------------------

Rule of thumb
~~~~~~~~~~~~~

Use absolute imports!
'''''''''''''''''''''''''''


.. code-block:: python

    from package.subpackage1.moduleY import spam
    from package.subpackage1.moduleY import spam as ham
    from package.subpackage1 import moduleY
    from package.subpackage1 import moduleY
    from package.subpackage2.moduleZ import eggs
    from package.moduleA import foo
    from package import bar



------------------------------------------------------

RsT
~~~

ReStructuredText is a plaintext markup syntax used as the default documentation format for Python projects.

http://docutils.sourceforge.net/rst.html

http://docutils.sourceforge.net/docs/user/rst/quickref.html
