Python basics
=============

----

Python
------

* general purpose programming language
* high level 
* dynamic but strong typing
* platform independent
* object-oriented
* partly support for functional paradigm
* garbage collector

----

Duck typing
~~~~~~~~~~~~

*"When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck."* -- James WhitComb Riley

.. code-block:: python

    def f(something):
        for e in something:
            print(e)
            
    f(open("input.txt"))
    f([1,2,3])
    f("hello")

*"Simply stated: provided you can perform the job, we don't care who your parents are."*

-----

Usage
--------

* general purpose
* system programming
* rapid GUI modelling
* prototyping
* text processing
* research
    * *scipy*
    * *numpy*
    * *nltk*
    * ...
* mobile development

----

Install the interpreter!
-------------------------

----

``import this``
---------------

.. sourcecode:: none

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity,
        refuse the temptation to guess.
    There should be one -- and preferably only one
        -- obvious way to do it.

        
----

``import this``
---------------

.. sourcecode:: none

    Although that way may not be obvious at first
        unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain,
        it's a bad idea.
    If the implementation is easy to explain,
        it may be a good idea.
    Namespaces are one honking great idea --
        let's do more of those!


----

Development environment
-----------------------

We use Python **3.x** (and not 2.x)!

IDE:

    * **Pycharm** (Free for academic users)
    * **Notepad++**
    * Spyder
    * IDLE
    * *Eclipse+PyDev*

Documentation
~~~~~~~~~~~~~
* http://docs.python.org/3/
* http://www.diveintopython3.org/
* Programming in Python 3

----

Interpreting
---------------

* several interpreters available
    * **CPython**, PyPy, Stackless Python
    * Jython, Pyjamas, IronPython, RPython

Cython
~~~~~~
"bytecode interpreter"::

    hello.py --> hello.pyc -- |VM|
       generating bytecode
                    interpreting

----

Basic types
----------------

* everything is an object, thus has methods and attributes
* ``object`` is the base class
* names/identifiers instead of variables ``=>`` everything is a *reference*
* mutable vs. immutable objects
* ``type(x)``, ``dir(x)`` type of an object and all accessible methods, attributes

----

Numbers
-------
* ``int`` type for integers
* ``float(3.14)``
* ``complex(1+2j)``
* constructor / conversion: ``int()`` / ``float()`` / ``complex()``
* operators: "``+,-,/,//,*,%, **``" and ``pow(x,y), divmod(x,y)``
* additional ``math`` library,  bitwise operations

----
    
Boolean
-------

* subtype of ``int``
* literals: ``True, False``
* basic operations: ``and or not``
* constructor / conversion: ``bool()``
* "``<,>,==,!=, <=, >=, is, is not``" operators result boolean
* everything can be evaluated as a boolean

``NoneType`` type
-----------------

* the only literal is "``None``"
* always evaluates to "``False``"

----------------------------

Equality
~~~~~~~~

As expected:

.. code-block:: python

    a = 1000
    b = 999 +1
    >>> a is b
    False
    >>> a == b
    True

But:

.. code-block:: python

    c = 2
    b = 1
    >>> b + 1 is c
    True

Try:

.. code-block:: python

    a = "I have a cat"
    b = "I have a cat"
    >>> a is b
    False

    a=sys.intern("I have a cat")
    b=sys.intern("I have a cat")
    >>> a is b
    True

https://realpython.com/python-is-identity-vs-equality/

------

Strings
--------

http://docs.python.org/3/library/string.html

.. code-block:: python

    b = 'hi!'
    a = "Hello World!"
    len(a) # 12
    a[6] # "W"
    str(1) # "1"
    b = ' :)', a+b # "Hello World! :)"
    a.find("o") # 5
    a.rfind("o") # 7
    a.split() # ['Hello', 'World!']
    a.lower() # 'hello world!'
    a.upper() # 'HELLO WORLD!'
    a.replace("World", "ITK") #' Hello ITK!'
    print("Hello {}. {}!".format(1, "Arthur"))

* multi-line strings with ``"""`` or ``'''``


----------------------------


Slicing
~~~~~~~~~~

.. code-block:: python

	myStr = "Hello"

::

	 +---+---+---+---+---+
	 | H | e | l | l | o |
	 +---+---+---+---+---+
	 0   1   2   3   4   5
	-5  -4  -3  -2  -1

.. code-block:: python

	myStr[1:]
	myStr[:-1]
	myStr[2:5]
	myStr[2:-2]
	myStr[:]

----------------------------


Type hierarchy of Python (2.x)
------------------------------

.. image:: types.gif
    :scale: 100%

http://docs.python.org/3/reference/datamodel.html#types

----

Indentation
------------

**Blocks are marked with colons (:) and with the indentation itself!**

* Wrong indentation yields error!
* Do not mix tabs and spaces!

**But** not all sort of whitespace are significant:

.. code-block:: python

    mylist = [
        "some string",
                "and another",
                    "and finally this",
    ]
    
    mystring = 'this is ' \
               'a very long string ' \
                        'that is split' \
               'across multiple lines'
               


----

Statements
----------

* ``pass``
* assignment with "``=``",  and "``x,y = y,x``" also works
* use a modul: ``import modul``
* ``del o``

* read std. input: ``input()`` function

------

Comments
--------

.. code-block:: python

    
    
    a = 42 # After the hashmark...
    
    # This is a single line comment.
    
    """ This is a multi-
    line comments
    """
    
    """
    This works as well.
    """

----------------------------

Sequence of statements
-----------------------

* separate statements with new line or "``,``" "``;``"
* one statement is in one line except if ends ``\``

.. code-block:: python

	a = 42 # nice number
	c,b = 1,2
	a = s.split( \
	  " ")


-----------------------------------------


``if``
------

.. code-block:: python

	if conditon1:
		...
	elif conditon2:
		...
	else:
		...

* no ``switch`` or ``case`` statement
* no need of brackets
* no restriction for the condition

----

Evaluating
~~~~~~~~~~

* everything can be evaluated as boolean
* lazy strategy
* the results of "``and or not``" are not ``True`` or ``False``, rather the dominating expression
* ``if x == True: ...`` ~ ``if a: ...``
* ``if x != None: ...`` ~ ``if not x: ...``


-----------------------------------------

Loops
--------

.. code-block:: python

    while condition:
        ...
    else:
        # optional block
	
    for e in iterable_element:
        ...
    else:
        # optional block
        
Others:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``"else"`` is only executed when the ``condition`` becomes  ``False``

* ``break`` -- break the loop
* ``continue`` -- skip an iteration step

----


Python program structure
------------------------

Command line processing in Linux: ``#!/usr/bin/env python``

.. code-block:: python

    #!/usr/bin/env python

    if __name__ == "__main__": 
        print("Hello World!")













