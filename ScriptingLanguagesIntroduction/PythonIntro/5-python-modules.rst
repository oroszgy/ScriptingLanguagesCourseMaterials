Modules, packages
========================

Modules
-------

* all ``.py`` files are modules (compiling units)
* interpreting a module means *interpreting the given file* 
* ``import`` statement interprets a module and adds its element to the namespace
* they are accessible by their name (e. g. ``modul.foo()``)
* one can import a module if its path is in the ``sys.path``

-----

.. code-block:: python
    
    """mymath.py"""
    def myadd(a,b):
        return a+b      
    def mymul(a,b):
        return a*b
        
    """myapp.py"""
    import mymath
    mymath.myadd(1,2)
    
    from mymath import myadd
    myadd(1,2)
    mymath.mymul(1,2) # Error
    
    from mymath import *
    myadd(1,2)
    mymul(1,2)


-------------


But the *__main__* environment is skipped during importing

.. code-block:: python

    print("this is run and printed")
    
    if __name__ == "__main__":
        print("While this condition is not True, " \
                "thus the interpreter skip this section.")
                
---------------

- All the names from a module is exported not started with an "_".
- One can overwrite the exported names with using "__all__".
  
.. code-block:: python

    """mymodule.py"""

    __all__ = ["_NOT_SO_HIDDEN_NAME"]

    _NOT_SO_HIDDEN_NAME = 42


---------------

Packages
--------

Packages are directories, containing at least one module named  ``__init__.py``

Usage:

* ``import package`` 
    * interprets the ``package/__init__.py``
* ``import package.module``
    * interprets the ``package/__init__.py``
    * interprets the ``package/module.py``

------------------------------------------------------------

``import`` and ``from``
------------------------

* assigns the *module* object to a name
* one can import :
    * **from** a module or a package
    * a module, a class, a function or any **name**

* any imported object is accessible by its qualified name

.. code-block:: python

    import something
    from mymodule import myobject as mo
    from package.submodule import myclass
    from anything import *
    # ...

    mo.do()
    a = anything.Anything()
    print something.MyClass.static_foo()
    #...
    