Other advanced concepts
------------------------

-------------------------------------------------------------------------


Python types
~~~~~~~~~~~~

* everything is an object


.. code-block:: python
	>>> class A: pass
	>>> type(A)
	<class 'type'>
	>>> A.__class__
	<class 'type'>

* classes are first-class objects
* => can be created / deleted anytime
* ``type`` 
    * is the class of all python classes
        * ``print A.__class__ # <type 'type'>``
    * is a (callable) object
        * ``MyClass=type(name, bases, dict)``
    
-------------------------------------------------------------------------

Metaclasses
~~~~~~~~~~~

Is the class of a class.

* metaclasses create classes, while classes create instances
* the default metaclass of classes is the ``type`` 

In practice, a class is created:
    * instantiating a class using metaclass available through the ``__metaclass__`` attribute
    * or calling the builtin ``type(name, bases, dct)`` method

-------------------------------------------------------------------------

Call ``type()`` with three parameters return a new class:
    
.. code-block:: python

    B = type("B", (object,), 
                {"f": lambda self,x : x+1})
    b = B()
    b.f(1) # 2

-------------------------------------------------------------------------

One can implement a metaclass, inheriting form the ``type`` class

.. code-block:: python

    class CustomMetaclass(type):
        def __init__(cls, name, bases, dct):
            print "Creating class %s using CustomMetaclass" 
                                                    % name
            super(CustomMetaclass, cls).__init__(name, bases, dct)

    class BaseClass(metaclass = CustomMetaclass): pass

    class Subclass1(BaseClass): pass

    # Creating class BaseClass using CustomMetaclass
    # Creating class Subclass1 using CustomMetaclass
    