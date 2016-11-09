Iterators
---------

------------------------------------------------------------

Iterator type
~~~~~~~~~~~~~

An iterator is an object implementing the iterator protocol:
https://docs.python.org/3/library/stdtypes.html#iterator-types

* allows to loop just once
* ``__next__() / next()`` -- get next element
* ``StopIteration`` is raised when the iteration is over

------------------------------------------------------------

.. code-block:: python

    >>> nums = [1,2,3]
    >>> iter(nums)
    <listiterator object at ...>
    >>> nums.__iter__()
    <listiterator object at ...>
    >>> it = iter(nums)
    >>> next(it) # next(obj) simply calls obj.next()
    1
    >>> it.__next__()
    2
    >>> next(it)
    3
    >>> next(it)
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    StopIteration

------------------------------------------------------------

``for`` can be used to iterate through an iterator

.. code-block:: python

    >>> for f in iter([1,2,3]): print(f)
    ...
    1
    2
    3

All sequences and container types implements this protocol:

.. code-block:: python

    >>> f = open('/etc/fstab')
    >>> f is f.__iter__()
    True

------------------------------------------------------------


Generators
~~~~~~~~~~

http://docs.python.org/3/tutorial/classes.html#generators

Generator functions allow to declare a function that behaves like an iterator

* In practice, "a generator is a function containing the keyword ``yield``."
* when it is called, the instructions are executed till the the next ``yield``
* cf. PEP 250

------------------------------------------------------------

.. code-block:: python

    >>> def f():
    ...   yield 3
    ...   yield 4
    >>> gen = f()
    >>> next(gen)
    3
    >>> next(gen)
    4
    >>> next(gen)
    -- finished --
    Traceback (most recent call last):
    ...
    StopIteration


------------------------------------------------------------

And your code can be more effective:

.. code-block:: python

    def firstn(n):
        num, nums = 0, []
        while num < n:
            nums.append(num)
            num += 1
        return nums

    def improved_firstn(n):
        num = 0
        while num < n:
            yield num
            num += 1

------------------------------------------------------------

Generator expressions
~~~~~~~~~~~~~~~~~~~~~

https://docs.python.org/3/tutorial/classes.html#generator-expressions

The syntax is similar to the list comprehension but will use parentheses

.. code-block:: python

    genpow = (i*i for i in range(10))

    """
    for x in genpow:
        if x > 100:
            print(x)
            break
    """

------------------------------------------------------------

Advanced generator topics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* `Bidirectional communication <http://scipy-lectures.github.io/advanced/advanced_python/index.html#bidirectional-communication>`_

* `Chaining generators <http://scipy-lectures.github.io/advanced/advanced_python/index.html#chaining-generators>`_

------------------------------------------------------------


Bidirectional communication
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

	def test_gen():
		k = 1
		s = 0
		for i in range(10):
			s += k
			k_ = yield s
			k = k_ or k

	g = test_gen()
	print(next(g))
	print(next(g))
	g.send(10)
	print(next(g))


------------------------------------------------------------



Iterators in the std. lib.
~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``range()``
* ``map()``
* ``filter()``
* ``reversed()``
* ``zip()``
* ``enumerate()``

------------------------------------------------------------


The ``itertools`` module
~~~~~~~~~~~~~~~~~~~~~~~~

"The module standardizes a core set of fast, memory efficient tools that are useful by themselves or in combination"

https://docs.python.org/3.4/library/itertools.html

-------------

.. code-block:: python


    count(10) # 10, 11, 12, ...
    cycle([1,2,3]) # 1 2 3 1 2 ...
    repeat('a', 3) # a a a

    takewhile(lambda x: x<5, [1,4,6,4,1]) # 1 4
    dropwhile(lambda x: x<5, [1,4,6,4,1]) # 6 4 1
    chain('ABC', 'DEF') # A B C D E F
    accumulate([1,2,3,4,5]) # 1 3 6 10 15
