Decorators
--------------

------------------------------------------------------------


Higher order functions
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    def my_higher_order()
        def myfun(x,y):
            return x,y

        return myfun

    f = my_higher_order()
    f(1,2) #3

    my_higher_order()(1,2) # 3

------------------------------------------------------------

Let's make ``addn`` functions:

.. code-block:: python

    def get_adder(n)
        return lambda x: x+n

    add2 = get_adder(2)
    print(add2(1)) #3

Make a linear *function* factory:

.. code-block:: python

    def linear(a,b):
            def result(x):  return a*x + b
        return result

    line_21 = linear(2,1)
    print(line_21(5)) # 11



------------------------------------------------------------

Closures
~~~~~~~~

* an inner function remembers its namespace (as above)

.. code-block:: python

    def outer(x):
        def inner():
            # x is part of the outer's namespace
            print(x)
        return inner

    print1 = outer(1)
    print2 = outer(2)
    print1() # 1
    print2() # 2

------------------------------------------------------------


Decorators
~~~~~~~~~~

https://docs.python.org/3/glossary.html#term-decorator

* is a *callable* that takes a function as an argument and return one as replacement
* usually applied with the ``@wrapper`` syntax

------------------------------------------------------------

.. code-block:: python

    def makebold(fn):
        def wrapped():
            return "<b>" + fn() + "</b>"
        return wrapped

    def makeitalic(fn):
        def wrapped():
            return "<i>" + fn() + "</i>"
        return wrapped

    @makebold
    @makeitalic
    def hello():
        return "hello world"

    print(hello())
    # <b><i>hello world</b></i>

------------------------------------------------------------

.. code-block:: python

    def bold(fun):
        def wrapped(*args, **kwargs):
            res = fun(*args, **kwargs)
            return "<b>{}</b>".format(res)
        return wrapped


    @bold
    def myfun(out1, out2):
        return out1 + " " + out2


    print(myfun("alma", out2="szilva"))

------------------------------------------------------------

Example decorators from the std. lib.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Builtins:

* ``classmethod``
* ``staticmethod``
* ``contextlib.contextmanager``
* ``functools.*``
* Properties

Others examples: https://wiki.python.org/moin/PythonDecoratorLibrary

------------------------------------------------------------


``functools``
^^^^^^^^^^^^^^

* ``total_ordering(cls)`` -- "Given a class defining one or more rich comparison ordering methods, this class decorator supplies the rest."
* ``functools.wraps(wrapped[, assigned][, updated])``

.. code-block:: python

    def makebold(fn):
        @wraps(fn)
        def wrapped():
            return "<b>" + fn() + "</b>"
        return wrapped


------------------------------------------------------------


.. code-block:: python

	from contextlib import contextmanager

	@contextmanager
	def tag(name):
		print "<%s>" % name
		yield
		print "</%s>" % name

	>>> with tag("h1"):
	...    print "foo"
	...
	<h1>
	foo
	</h1>

------------------------------------------------------------


Properties
^^^^^^^^^^

.. code-block:: python

    class C(object):
        def __init__(self):
            self._x = None

        def getx(self):
            return self._x

        def setx(self, value):
            self._x = value

        def delx(self):
            del self._x

        x = property(getx, setx, delx, "I'm the 'x' property.")

-----------------------------------------

.. code-block:: python

    class C(object):
        def __init__(self):
            self._x = None

        @property
        def x(self):
            """I'm the 'x' property."""
            return self._x

        @x.setter
        def x(self, value):
            self._x = value

        @x.deleter
        def x(self):
            del self._x

-----------------------------------------

Class decorators
~~~~~~~~~~~~~~~~

* a class decorator is a callable that takes a class and returns a class

.. code-block:: python

    def my_dec(cls):
        cls.y = 0
        return cls

    @my_dec
    class A(object): pass

    print A.y  # 0


------------------------------------------------------------

.. code-block:: python

    class MyDec(object):
        def __new__(self, cls):
            cls.x = 1
            return cls


    @MyDec
    class A(object): pass

    print A.x  # 1


------------------------------------------------------------

Class of decorators
~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    class Add():
        def __init__(self, num):
            self.__num = num

        def __call__(self, fun):
            return lambda x : fun(x) + self.__num

    @Add(1)
    @Add(2)
    def pow2(x):
        return x*x

    print(pow2(2)) # 7
