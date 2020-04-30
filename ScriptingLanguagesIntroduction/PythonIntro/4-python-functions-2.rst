Advanced functions
===================

----------------------------------


Function as parameter
----------------------

* ``def`` is a statement, that creates an object
* the name of the object is the function name
* any object can be passed as a parameter

.. code-block:: python

    def calc(x):
        return (x + 2) / 10

    def f(do, with):
        return do(with)
    
    print(f) # <function f at 0x7f9201280440>
    print(f(calc, 8)) # 1

----------------------------------

Nested Functions
~~~~~~~~~~~~~~~~~

* ``def`` is just a statement
* you can create an object in the body of a function

.. code-block:: python

    def printer(*args):
        def nice_printer(x):
            print ("--%s--"%(x,))
        for a in args:
            nice_printer(a)

    printer(1,2,3)

-------------------


Anonymous functions
-------------------

``lambda`` is a statement for defining function objects



Syntax:

.. code-block:: python

    f = lambda parameters: expression(parameters)
    
    print(f) # <function <lambda> at 0x7f57dba11320>
    
    f(param)


-------------

Both type of functions do the same:

.. code-block:: python

	def calc1(x): return (x + 2) / 10
	calc2 = lambda x: (x + 2) / 10
	print (calc1(42) == calc2(42)) # True

Sometimes ``lambda`` can shorten your code:

.. code-block:: python

	def f(do, _with): return do(_with)
	print (f(lambda x: (x + 2) / 10, 8)) # 1

A more complex example:

.. code-block:: python

    f = lambda *x: [ e+1 for e in x]
    print(f(1,2,3)) # [2,3,4]

----

Local and global variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* local variables:
    * arguments of functions
    * variable defined in the body of a code block (function, loop, selection)
    * loop variable
* variables declared in the module called globals (but may be hidden)

.. code-block:: python

    var = 42
    for var in range(5):
        print(var) # 0, 1, 2, 3, 4
        
--------


``global`` statement can be used to change the value of a global variable

.. code-block:: python

    x = 42

    def h1(y):  
        x = y
        
    def h2(y): 
        global x;  
        x = y

    h1(1); print(x) # 42
    h2(1); print(x) # 1

--------

Functions parameters
----------------------

Call
~~~~~~

* ``fun(val)`` -- passing by position
* ``fun(name=val)`` -- passing by keyword

Define
~~~~~~

* ``def fun(name)``
* ``def fun(name=val)`` -- default value
* ``def fun(*name)`` -- rest of the positional parameters
* ``def fun(**name)`` -- rest of the parameters by keywords

----------------------------------

Examples:

.. code-block:: python

    def mysum(*args):
        s = 0
        for val in args: # args is a tuple
            s+=val
        return s
            
    print(mysum(1,2,3)) # 6
    
    def add(**kwargs):
        # kwargs is a dictionary
        if "x" in kwargs and "y" in kwargs:
            return kwargs["x"] + kwargs["y"]
    
    print(add(x=3, y=6)) # 9

---------------

.. code-block:: python

    def complicated(first, second=None, *args, **kwargs):
        print(first, second)
        print(args)
        print(kwargs)
   
    complicated(42, "non-empty", 1,2,3, x=0, y=1)
    
    """
    The result is:
    42 non-empty
    (1, 2, 3)
    {'y': 1, 'x': 0}
    """
            

---------------


Built-in functions
------------------

Efficiency counts!

* ``len()``
* ``max()``, ``min()``

* ``eval()``

* ``all(), filter(), map()``
* ``reduce(), sum()``
* ``zip()``
* ``next()``
* ...

http://docs.python.org/3/library/functions.html

----

Built-in functions 1.
---------------------

``map``
~~~~~~~

Applies a function for each element of a list

.. code-block:: python

    >>> map(str.lower, ["A", "B"])
    ['a', 'b']
    >>> map(max, [[4,2,0], [1,3,5]])
    [4, 5]

``filter``
~~~~~~~~~~

Constructs a new iterable from another keeping elements whose function returns ``True``

.. code-block:: python

    >>> filter(str.islower, ["a", "A", "1"])
    ['a']
    >>> filter(lambda x: x, [0, 1, [], None, {}])
    [1]

----

Built-in functions 2.
---------------------

``sum``
~~~~~~~

* summarize all elements of an iterable

.. code-block:: python

    >>> sum(range(5))
    10
    >>> sum([[1], [2,3], [4,5,6]], [])
    [1, 2, 3, 4, 5, 6]

``reduce``
~~~~~~~~~~

* apply a function of two arguments cumulatively

.. code-block:: python

    >>> from functools import reduce
    >>> reduce(lambda x,y: x*y, range(1,5))
    24

Evaluated as: ``((((1*2)*3)*4)*5)``

----

Built-in functions 3.
---------------------

``zip``
~~~~~~~

Creates an iterator of tuples from iteratables

.. code-block:: python

    >>> x = [1, 2, 3]
    >>> y = ["a", "b", "c"]
    >>> zipped = zip(x, y)
    >>> list(zipped)
    [(1, "a"), (2, "b"), (3, "c")]

The other direction:

.. code-block:: python    

    >>> x2, y2 = zip(*zipped)
    >>> x == list(x2) and y == list(y2)
    True

----

    
Random numbers
---------------

http://docs.python.org/3/library/random.html

.. code-block:: python
    
    from random import *
    
    print(choice(["a", None, 1])) # either of the three element
    
    print(random()) # a float number from [0.0, 1.0)
    
    print(randint(1,10)) #an integer from [1,10]

