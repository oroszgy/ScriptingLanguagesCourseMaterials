Functions in Python
===================

----

Defining functions
--------------------

* there is no distinction between methods and functions *(side-effect)*
* all functions are objects

Syntax:

* ``def`` statement is used to create function
* semicolon(``':'`` ) is necessary to start the body
* indentation is important! 
* no type definition! (dynamically typed language)

----

Examples:

.. code-block:: python

    def myadd(par1, par2):
        return par1 + par2
        
    def mysum(mylist):
        s = 0
        for e in mylist:
            s+=e
        return e

    def donothing(par1): pass

    print(myadd(1,mysum([2,3,4])))

----

But, what happens?

.. code-block:: python

    def myfun(a,b): 
        print(a)
    
    def myfun(a,b): 
        print(b)
    
    # The output is ...
    myfun
    myfun(1)
    myfun = 42
    myfun
    myfun(1)
   

----


Returning value
-----------------------------

* ``return`` statement is used
* the default return value is ``None``

.. code-block:: python

    def f():
        pass
    
    print(f()) # None
    
* returning several values is possible

.. code-block:: python

    def multifun(a,b):
        return a+b, a-b
    
    print(f(3,2)) # (5,1)



----------------------------------


Passing parameters 1.
----------------------

* parameters are local variables
* dynamically typed
* their references are passed
    * mutable vs immutable case!


----

Examples:

.. code-block:: python

    def f(x): 
        x=42
        print(x)
    a=0
    f(a) # 42
    print(a) # 0
    
    """This is the so called duck-typing"""
    def foo(x): 
        x+="a"
        
    a = "hello"; 
    l = [42,0]
    foo(a); print(a) # "hello"
    foo(l); print(l) # [42, 0, "a"]



----------------------------------

Passing parameters 2.
----------------------

* passing by order
* default parameters:

.. code-block:: python

	def inc(x, plus = 1):
		return x + plus

* parameter passing by keywords:

.. code-block:: python

	inc(plus=5, x=6)

* passing by order and by keyword can be mixed

----------------------------------

Default parameter
~~~~~~~~~~~~~~~~~

What is the expected behavior?

.. code-block:: python

    def function(data=[]):
        data.append(1)
        return data
    
    print(function()) # [1]
    print(function()) # [1, 1]
    print(function()) # [1, 1, 1]
    
But:

.. code-block:: python

    def function(data=None):
        data = data or []
        data.append(1)
        return data
    
    print(function()) # [1]
    print(function()) # [1]
 
-------------------

Scope and lifetime
------------------

The lifetime of an object depends on the GC.

A variable scope is its namespace (and the enclosed ones):

* names organized in namespaces
* modules and functions defines a namespaces
    * a namespace can be global or local
* every name is only accessible from its namespace
* globals, builtins might be hidden
* name resolution order: local → *enclosing* → global → builtin

-----------------------------------

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


