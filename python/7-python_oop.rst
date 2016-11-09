=============
OOP in Python
=============

--------------------------------------------------------------------------------

Basics
~~~~~~

http://docs.python.org/3/tutorial/classes.html

* everything is an object
* classes as well, but
    * defines a new namespace
    * are callable
    * ``object`` is their base class
* instances
    * are created by classes
    * inherit the namespace of the class
* there is no interfaces or abstract classes

--------------------------------------------------

Class statement
~~~~~~~~~~~~~~~

.. code-block:: python

    class T(object):
        def do(self): print("Hello")
    class T(object): pass

    t = T()
    t.do()   # AttributeError

    class X(object):
        class Y(object):
            class Z(object): pass

    x = X()
    y  = x.Y()
    z = X.Y.Z()

---------------------------------------------

Basic syntax
~~~~~~~~~~~~

.. code-block:: python

    class Vehicle(object):
        vehicle_name = "train"
        
        def add_passanger(self, name):  
            self.last_passanger = name

        def get_last_passanger(self):
            return self.last_passanger

    my_train = Vehicle()
    print(my_train.vehicle_name)
    
    my_train.add_passanger("John")            
    print(my_train.last_passanger)          
    print(my_train.get_last_passanger())

--------------------------------------------------


Instance and class attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    >>> class TestData(object):
    ...     spam = 42
    ...
    >>> x = TestData()
    >>> y = TestData()
    >>> x.myAttr = 1; print(x.myAttr)
    1
    >>> TestData.spam = 99
    >>> x.spam, y.spam, TestData.spam
    (99, 99, 99)
    >>> x.spam = 88
    >>> x.spam, y.spam, TestData.spam
    (88, 99, 99)

--------------------------------------------------------------------------------


Methods
~~~~~~~

* a method is just another object...
* is bound to an instance object
* the first parameter is ``self` referring to the instance object (implicit parameter)
* ``Vehicle.add_passanger(my_train, "John")`` call is translated to ``my_train.add_passanger("John")``
* accessing method from another one: ``self.method()``

.. code-block:: python

    my_train.x = "42"
    print my_train.x
    my_train.my_foo = lambda x: x+1
    print(my_train.my_foo(0))

--------------------------------------------------

Constructor, destructor
~~~~~~~~~~~~~~~~~~~~~~~~

* implicit constructor (with 1 parameter)
* implicit destructor (does nothing)

.. code-block:: python

    class Train(object):
        def __init__(self, capacity):   
            self.capacity = capacity    

        def __del__(self):              
            pass

    t = T(1)
    del t

--------------------------------------------------------------------------------

Object creation and initialization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``__init__(self)``
    * instance level method
    * initialize the object
    * does not return anything
    * called after the object creation
    
* ``__new__(cls)``
    * class level method
    * returns the new object
    

--------------------------------------------------------------------------------

Class-level methods
~~~~~~~~~~~~~~~~~~~~

* can be created with decorators 
* creating a classmethod lets you access the class as well

.. code-block:: python

    class T(object):
        @staticmethod
        def static_method():
            print("Hello!")

        @classmethod
        def class_method(cls):
            print(cls.__name__)

    o = T()
    T.static_method() # "Hello!"
    o.static_method()  # "Hello!"

    T.class_method()  # "T"
    o.class_method()   # "T"

--------------------------------------------------------------------------------

More on methods
~~~~~~~~~~~~~~~

* overloading?
* no abstract methods: ``raise NotImplementedError()``
* special methods: http://docs.python.org/3/reference/datamodel.html#special-method-names
    * numeric operators
    * comparisons
    * emulating containers, callables, ...


----------------------------------------------------------

Visibility
~~~~~~~~~~
* every attribute is visible and accessible by default
* you may start the *non API* attributes with ``_``
* name mangling helps:  ``__name`` is transformed to ``_Classname__name``

.. code-block:: python

    class Test(object):
        def __hidden(self): print("You won!")

    t = Test()
    t.__hidden()      # ERROR!
    t._Test__hidden() # "You won!"

Controlling attribute access
''''''''''''''''''''''''''''

* ``__setattr__``
* ``__getattr__``
* ``__delattr__``

------------------------------------------


Inheritance
~~~~~~~~~~~

.. code-block:: python

    class A(object):
        def __init__(self):
            print("init A"); self.__x = "a"

    class B1(A):
        def __init__(self):
            print("init B1"); self.__x = "b"

    class B2(A):
        def __init__(self):
            A.__init__(self); print("init B2")

    class B3(A): pass

    b1 = B1(),    # init B1
    b2 = B2()   # init A init B2
    b3 = B3()   # init A

--------------------------------------------------------------------------------

Multiple inheritance
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    class C1(B1,B2):
        def get_x(self): return self.__x
    class C2(B2, B1):
        def get_x(self): return self.__x

    c1 = C1()   # init B1
    c2 = C2()   # init A init B2
    print(c1.get_x(), c2.get_x()) # AtributeError

    #====BUT=====
    
    class C1(B1,B2):
        def get_x(self): return self._B1__x
    class C2(B2, B1):
        def get_x(self): return self._A__x

    c1, c2 = C1(), C2()
    print(c1.get_x(), c2.get_x()) # b a

---------------------------

``super``
~~~~~~~~~

.. code-block:: python

    class T(object):
        a = 0
    class A(T):
        pass
    class B(T):
        a = 2
    class C(A,B):
        pass
    c = C()
    
    super(C,c).a # 2
    
* uses the method resolution order 
* the MRO of ``C`` is ``[C, A, B, T, object]``
* with ``super`` there is no need for explicitly name the parent
* returns a proxy object 

---------------------------


Python type hierarchy
~~~~~~~~~~~~~~~~~~~~~

* Method resolution order: http://www.python.org/download/releases/3/mro/
* Python type hierarchy: http://docs.python.org/3/reference/datamodel.html#the-standard-type-hierarchy
* built-in types can be used as base classes

.. code-block:: python

    def MyList(list): pass
    l = MyList()
    l.append(1)
    print(l)



---------------------------

Exceptions
~~~~~~~~~~~~~~~~~~~~

* one can define its own exception class
* ``BaseException`` or ``Exception`` used as a base class
* name convention ``SomethingError``

.. code-block:: python

    class MyError(Exception): pass

    
    class CustomError(Exception):
        def __init__(self, value):
            self.parameter = value
        def __str__(self):
            return repr(self.parameter)

    
---------------------------

Docstrings
~~~~~~~~~~~

http://www.python.org/dev/peps/pep-0257/
http://google-styleguide.googlecode.com/svn/trunk/pyguide.html

* first statement (that is a string) in a module, function, class, package
* thus becames the ``__doc__`` attribute
* use always ``"""triple double quotes"""``
* can be one-line or multiline


--------

Style guides
~~~~~~~~~~~~~

* http://www.python.org/dev/peps/pep-0008/
* http://www.seas.upenn.edu/~lignos/py_antipatterns.html
