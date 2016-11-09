Functions in Lua
================

-------------------

Basics
------

.. code-block:: lua

    function myPrinter(name)
        print "hello " .. name
    end

-  the only tool for abstraction 
-  first-class values
-  function parameters are locals
-  parenthesis can be left in case of one parameter

--------------

Function definitions
--------------------

Two possible way of defining functions

.. code-block:: lua

    function f(<parameters>)
        <statements>
    end

    f = function(<parameters>)
        <statements>
    end

* builtin names can be overridden

--------------

Parameter passing
-----------------

-  only positional
-  can be called with any number of parameters
    -  if more than needed: useless parameters are dropped 
    -  if less: uninitialized parameter has ``nil`` values

.. code-block:: lua

    function f(x,y)
      print(x,y)
    end 
    f() -- nil nil
    f(1) -- 1 nil
    f(1,2,3) -- 1 2

Vararg functions
~~~~~~~~~~~~~~~~

.. code-block:: lua

    function f(...) -- any number of parameters
      a,b = ...
      print(a,b,...)
    end
    f(1,2,3) -- 1 2 1 2 3

--------------

Simulating named parameter
--------------------------

.. code-block:: lua
    
    function foo(args)
        print (args.first .. args.last)
    end

    foo{first="hello", last="world"}
    
-------------


Parameter passing
-----------------

* passing by value
* values are objects that are assigned to names
* some types are immutable

.. code-block:: lua

    function f(a)
      a = a .. "!" 
    end
    x = "Hello"
    f(x)
    print(x) -- Hello

--------------

Parameter passing
-----------------

* but some are mutable

.. code-block:: lua

    function f(t)
      t["x"] = 42
    end
    mt = {}
    f(mt)
    print(mt["x"]) -- 42


--------------

Default parameters
-------------------

.. code-block:: lua

    function incCount (n)
      n = n or 1
    count = count + n
    end

Function overloading
---------------------

.. code-block:: lua

    function f(a)
      print(a)
    end

    function f()
      print(42)
    end

    f("b") -- 42

--------------

Return values
------------------

-  ``return`` -- last statement of a block
-  without ``return`` or with *empty* ``return`` there is **no return value** 

.. code-block:: lua

    function doNothing() end -- nothing
    function doNothing2() return end -- nothing
    function getNil() return nil end -- nil
    
More than one return value
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: lua

    function returnArgs(a,b,c)
        return a,b,c
    end

--------------

Arguments vs. return values
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: lua

    print(returnArgs(1,2,3)) -- 1 2 3
    print("a",returnArgs(1,2,3)) -- "a" 1 2 3
    print(returnArgs(1,2,3), "a") -- 1 "a"
    print(returnArgs(1,2,3), returnArgs(4,5,6)) -- 1 4 5 6
    print(returnArgs(1,2,3), (returnArgs(4,5,6))) -- 1 4 
    print(doNothing(),2) -- ???
    print(doNothing(), doNothing()) -- ???


-  brackets makes returning values treated as there was only one
-  if the last parameter a function call: all the returned values are used
-  if not, just the first value is used

--------------

Closures
---------

-  functions that has inner state (*local variables*)

.. code-block:: lua

    function makeAdd(n) -- in is local for the inner fun.
      add = function(m) return n+m end
      return add
    end
    plusone = makeAdd(1)
    print(plusOne(1)) -- 2
    print (makeAdd(1)(2)) -- 3

    function makeCounter()
      local count = 0 -- local for the inner fun.
      return function() count = count +1; print(count) end
    end

    counter = makeCounter()
    counter() counter() counter() -- 1 2 3

--------------

Recursion
----------

-  similar to any other imperative language
-  *stack overflow* error may occur
-  optimized tail recursion 
    - only with using ``return``

.. code-block:: lua

    function rec()
      return rec() -- tail recursion
    end
    
    rec()

--------------

Chunks
-------

-  a code fraction that can be interpreted

   -  any line typed in the interpreter (eg. ``for``, ``if``) (plus the following lines if needed)
   -  a Lua file

-  interpreted => anonymus function
-  may contain a ``return``

.. code-block:: lua
    
    > return "hello"
    hello
    > = "hello"
    hello 

----------

Modules
=======

-  usage *policies*
-  ``require`` and ``module``
-  a module is a library, that is loaded with ``require`` and defines a global namespace (that is a table...)
-  every exported entity is part of this namespace (table)
-  first-class values
   -  RHS or LHS of an expression

-  it is not a substantive part of the language just a table

--------------

.. code-block:: lua

    -- mod.lua
    module(..., package.seeall)
    function foo() end
    myVar = 42

.. code-block:: lua

    -- testmod.lua
    require "mod"
    mod.foo()

    -- testmod2.lua
    local m = require "mod"
    local f = m.foo
    f()

--------------

Modules
-------------------

-  simplified statement: ``module(..., package.seeall)``

   -  the module name is the filename
   -  globals are exported

http://www.lua.org/pil/15.html


``require``
~~~~~~~~~~~~

-  ``require`` forces the interpreter to interpret the module
-  a module can be loaded only once
-  ``package.loaded`` table contains the loaded modules

--------------

Loading modules
-----------------

-  there is no directory representation in ANSI C
-  *patterns* are used for describe a path

   -  ``package.path`` 
   -  ``"?;?.lua;/usr/local/lua/?/?.lua"``
   -  ``'?'`` -- modul name, ``';'`` -- separator

