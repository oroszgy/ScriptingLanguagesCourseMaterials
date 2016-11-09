===================
Lua basics
===================

----------------


Visibility
----------

* every variable is global
* ``local`` makes a variable local (in a block)
* variable of the ``for`` is local
* local variable hides the global one with the same name
* the visibility of a local one starts after its declaration

.. code-block:: lua
    
    var = 42
    do
      local var = var -- ???
      var = 24
      print(var)
    end
    print(var)

---------
    

String indexing
---------------

``string.sub(s, i [, j])``

-  indexing starts from ``1``
-  closed interval from both sides

.. code-block:: lua

    string.sub("Hello Lua user", 7) --  Lua user
    string.sub("Hello Lua user", 7, 9) -- Lua
    string.sub("Hello Lua user", -8) -- Lua user
    string.sub("Hello Lua user", -8, 9) -- Lua 
    string.sub("Hello Lua user", -8, -6) -- Lua

--------------

Strings
--------

-  ``string.len("Alma") -- "4"``
-  ``string.format("%d %s", 2, "alma") -- "2 alma"``
-  ``string.upper("Alma") -- "ALMA"``
-  ``string.lower("Alma") -- "alma""``
-  ``string.reverse("Alma") -- " amlA"``

Shorter forms:

.. code-block :: lua

    mystring = "alma"
    print(#mystring==mystring:len()) -- true
    print(mystring:reverse()) -- "amla"
    -- etc.

http://www.lua.org/manual/5.1/manual.html#5.4

--------------

Math
----

-  ``math.cos(num)``, ``math.sin(num)``, ...
-  ``math.ceil(num)``, ``math.floor(num)`` -- round
-  ``math.exp(x)``, ``math.pow(x,y)`` -- ``e^x`` and ``x^y``
-  ``math.sqrt(x)`` -- ``x^(0.5)``
-  ``math.huge``, ``math.pi`` -- constants
-  ``math.log(x)``, ``math.log10(x)`` -- logarithm
-  ``math.max(...), math.min(...)`` -- maximum / minimum of the parameters
-  ``math.random ([m [, n]])`` -- random number between ``1..m`` **or** ``m..n`` 

http://www.lua.org/manual/5.1/manual.html#5.6

----

Tables
------

* associative arrays
* can be indexed by any values except  ``nil``
* can contain any type of value
* ``nil`` **as value** means, the element is deleted

.. code-block:: lua

    empty = {}
    myvar = "x"
    myint = 42
    many = { ["here"]="where", 
      there=empty; [{}]=0, [42]=24, 
      [myint]= myvar;}
      
* ``[]`` is obligatory for numbers and variables
* string quotes can be omitted
* one can separate with ``,`` or ``;``

-------

Tables
------

.. code-block:: lua

    print(many["here"]) -- where
    many["here"]=0
    print(many.here) -- 0
    print(many[{}]) -- 0


    for k,v in pairs(many) do -- generalized for
        print(k,v)
    end 
    
* do not modify your table during a loop


---------------

Tables as "arrays"
-------------------

.. code-block:: lua

    array = {'a', 'b', 'c'}
    print (#array) -- 3
    print(array[1], array[2], array[3]) -- 1 2 3
    
    for k,v in ipairs(array) do 
        print(k,v) 
    end
    
    array.x = 6
    print (#array) -- 3

-  implicit indexing (positive integers from ``1``)
-  array and table syntax can be mixed
-  ``ipairs(...)`` is used for positive integer indexes



--------------

Further "array" methods
----------------------

-  ``table.concat(table [, sep [, i [, j]]])`` -- concatenate table content
-  ``table.sort(table [, comp])`` -- order with ``comp`` function
-  ``table.insert(table, [pos,] value)`` -- "array" insertion
-  ``table.remove(table [, pos])`` -- "array" deletion
-  ``table.maxn(table)`` -- returns the index of the greatest value
-  ``unpack (list, i, j)`` - returns the elements from the given table between the indeces

.. code-block:: lua

    > a={1,2,3, alma = 1}
    > =#a
    3

http://www.lua.org/manual/5.1/manual.html#5.5

---------------

Standard IO
-------------

.. code-block:: lua
    
    print("Your name:")
    line = io.read()
    io.write("Hello "..line.."!\n")
    
-----------

I/O
----

Predefined files
~~~~~~~~~~~~~~~~~~

-  ``io.input()``, ``io.output()``
-  ``io.stdin``, ``io.stdout``, ``io.stderr``

Operations
~~~~~~~~~~~

-  ``io.read([format])`` -- \`\ ``io.input():read()``

   -  ``"*n"``, ``"*a"``, ``"l"``, ``num``
   -  returns ``nil`` if fails
   -  *buffer!*

-  ``io.write(str)`` -- \`\ ``io.output():write(str)``, ...

--------------


Files
------

-  ``file = io.open(filename [, mode])`` : open

   -  ``mode``: ``r``, ``w``, ``a``,...
   -  ``nil`` or file

-  ``io.close(file)``, ``io.flush(file)``
-  ``for line in io.lines(filename) do ... end``: open, iterate, close
-  ``io.tmpfile()``

-  ``io.type(object)``
-  ``file:read()``


-------------

``read``
----------

-  ``file:read("*all")``
-  ``file:read("*line")``
-  ``file:read("*number")``
-  ``n=42; file:read(n)``

Command line arguments
----------------------

.. code-block:: lua

    print(arg[0])    -- script name
    print(arg[1])    -- first parameter
    print(arg[2])    -- ...

    print (#arg)     -- number of parameters
