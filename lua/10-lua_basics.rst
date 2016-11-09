==========
Lua basics
==========

----------------

Introduction
------------

History
~~~~~~~
* 1993, Petronas
* *moon*
* ancestors: Simple Object Language, Data Entry Language
    
Application
~~~~~~~~~~~
* testing C/C++ codes
    * iOS_ / game development
.. _iOS: http://www.luanova.org/ioswithlua
* embedded data processing
* scripting applications


------

Principles
----------

* simplicity (in language and in its implementation)
* efficiency (fast interpreter)
* portability (ANSI C compatible)
* can be embedded (simple C API)
    * low cost embedding

Install
-------
* version **5.1**
* Windows: http://code.google.com/p/luaforwindows/
* http://lua-users.org/wiki/LuaBinaries
* http://www.lua.org/demo.html

IDE: http://lua-users.org/wiki/LuaIntegratedDevelopmentEnvironments

-------

Docs
----

* http://www.lua.org/docs.html
* http://www.lua.org/pil/
* http://nyelvek.inf.elte.hu/leirasok/Lua/
* http://lua-users.org/wiki

Textbooks in  library
~~~~~~~~~~~~~~~~~~~~~

* Jung, Brown - Beginning Lua Programming
* Ierusalimschy - Programming in Lua

----------

Typing
-------

* weak typing 
* ``type`` function helps

Types
~~~~~

* ``nil``
* ``boolean``
* ``number`` (~ double)
* ``string`` (8 bytes)
* ``function``
* ``userdata``
* ``table``
* ``thread``


----------------


Basics
------

Interpreter
~~~~~~~~~~~

* exit: ``CTRL`` + ``Z`` or ``C``
* history: ↑ ↓

``nil``
~~~~~
* not initialized variables
* logical value is ``false``

Comments
~~~~~~~~

* ``-- single line comment``
* ``--[[ multi-line comment ]]``

----------------

``number``
----------

Literals
~~~~~~~~~

* ``5e2``
* ``500``
* ``500.0``
* ``0x1f4``

Operations
~~~~~~~~~~

* float operations
* ``+ - * / ^``
* from Lua 5.1 ``%`` as well

``1/0=?``

----------------

``string``
------------
Literals
~~~~~~~~~
* ``"don't"`` and ``'"hello"'`` works like Python
* escape sequences ``"\n"``,``"\t"``
* multi-line strings with ```[[```` and ``]]``
    * no special characters

Operations
~~~~~~~~~~
* concatenate: ``"hello"..'world'..[[!]]``
* length: ``#"four"``
* automatic conversion: ``string`` ⇄ ``number``

http://lua-users.org/wiki/StringLibraryTutorial

----------------

``boolean`` 
~~~~~~~~~~~~~

* literals: ``true``, ``false``
* every object has a boolean value
    * ``nil`` → ``false``  
    * others  → ``true``

Operations
~~~~~~~~~~

* ``==``, ``~=``: types must match, a ``string`` is compared by its content
* ``<``, ``>``:  used on ``string`` and ``number`` types
* ``and or not``
    * lazy evaluation
    * evaluated to a subexpression value

----------------

Statements
----------

* assignment
    * ``x = 42``
    * ``x,y = y,x``
    * Garbage collection
* sequence
    * ``','``, ``';'``, whitespace

Example
~~~~~~~

.. code-block:: lua

    h,w = "Hello", 'World'
    out = "h.." "..w.."!"; print(out)


----------------

Compound statements
--------------------

``if``
~~~~~~

.. code-block:: lua

    if N == 1 then
      print("N is one")
    elseif N == 2 then
      print("N is two")
    else
      print("N is unknown")
    end

* ``elseif`` and ``else`` are optional
* ``then`` and ``end`` is obligatory
* indentation is not important

----------------

``while``
~~~~~~~~~

.. code-block:: lua

    c = 1
    while c <= 10 do
      print(c)
      c = c + 1
    end

``break``
''''''''''

* breaks the loop
* must be the last statement in a block

Blocks
~~~~~~

.. code-block:: lua

    do
      <statements>
    end

----------------

``for``
~~~~~~~~~~

.. code-block:: lua

    for c = 1,10,2 do
      print(c)
    end
    
    -- 1,3,5,7,9

* loop variable cannot be modified

``repeat``
~~~~~~~~~~~~

.. code-block:: lua

    i = 5
    repeat 
        print(i) i=i-1 
    until i<0 -- 5,4,3,2,1,0
    
* the condition is evaluated after the expression



