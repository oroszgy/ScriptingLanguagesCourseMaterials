Basic data structures in Python
===============================

----

``list``
--------

a **mutable** sequence `type <http://docs.python.org/3/library/stdtypes.html#list>`_

.. code-block:: python

    empty1, empty2 = [], list()
    a = [True, 1, "alma", 5.0, []]
    1 in a # True
    a[2] = "szilva"
    a[2] # "szilva"
    a.append(-1) # add an element to the end
    a.extend([1,2]) # extends the list with another
    a + b # creates a new list
    del a[3] # remove the item at the index
    range(0,5) # [0, 1, 2, 3, 4]
    range(5) # same as above
    l = list("abc") # ["a", "b", "c"]
    " ".join(l) # "a b c"
    [1,2,3,4,5,6,7,8,9,10][1::2] # [2,4,6,8,10]

What is the difference between  ``sorted(l)`` vs. ``l.sort()``?

--------


``range``
----------

an **immutable** sequence `type <http://docs.python.org/3/library/stdtypes.html#range>`_ of **numbers**

.. code-block:: python

    list(range(3)) # [0,1,2]
    list(range(1,3)) # [1,2]
    r = list(range(0,5,2)) # [0,2,4]
    10 in r # False
    r[1] # 5
    r[1:] # range(2,5,2)

-----



``set``
--------

"unordered collection of distinct objects"

* **mutable** `type <http://docs.python.org/3/library/stdtypes.html#set>`_
* each element is `hashable <http://docs.python.org/3/glossary.html#term-hashable>`_

.. code-block:: python

    s = {1,2,3} 
	s = set([1,2,3]) # create new
	s.add(x) # add element
	s.remove(x) # remove element
	x in s # contains?
	s | t # union
	s & t # intersect
	s - t # symmetric difference
	s <= t # is subset?

* but ``frozenset`` is an **immutable** type

-----------

``tuple``
----------

"fix number of items in a definite order"

* **immutable** sequence type

.. code-block:: python

	t0 = ()
	t = (1,"a", None, ())
	t[1] # "a"
	tuple([1,2,3]) # (1,2,3)
	list((1,2,3)) # [1,2,3]
	
	t0, t1, t2, t3 = t
	a, *b = t # 1, ["a", None, ()]
	a, b, *c = t # 1, "a", [None, ()]
	a, *b, c = t # 1, ["a", None], ()

-------------

``dict``
--------

"efficient for storing of key-value pairs"

* **mutable** type
* with `many methods <http://docs.python.org/3/library/stdtypes.html#mapping-types-dict>`_
* ~ hash-table, associative array, dictionary, table, mapping types 
* a key value must be `hashable <http://docs.python.org/3/glossary.html#term-hashable>`_
* access methods returns `view objects <http://docs.python.org/3/library/stdtypes.html#dictionary-view-objects>`_
----

Basic methods:

.. code-block:: python

	dt = {}; dt2 = dict()
	d = {1 : 2, "a" : 1.0, None : "alma"}
	dt[1] = "alma"; print d["a"]
	del d["a"] # remove element with key
	d.keys() # view of keys
	d.values() # view of values
	x in d # contains key?
	
	for key,value in d.items(): # view object of (key,value) tuples
		print key,value


----------

List comprehension
------------------

* compact syntax
* generate lists on demand
* process an existing list easily

General formalism:

.. code-block:: python

    [ expression(e1, e2...)
                for e1 in container1 if condition1
                for e2 in container2 if condition2
                ... ]

----
                
Examples:

.. code-block:: python

    """ even cube numbers """
    [x*x for x in range(10) if x % 2 == 0 ]
    
    """ 3x3 matrix coordinates """
    [ [ (x,y) for y in range(3) ] for x in range(3) ]

-----

``set`` comprehension
---------------------

Examples:

.. code-block:: python

    """ set of short words"""
    { w for w in words if len(words) < 5}
    
    """ intersection of two lists"""
    { e1 for e1 in list1 for e2 in list2 if e1==e2 }

----

``dict`` comprehension
-----------------------

Examples:

.. code-block:: python
    
    """ generate a word index """
    mdcit = { word:index for index, word in enumerate(words)}
    
    """ transform an existing dictionary"""
    newdict = { k-1: v.lower() for k,v in mdict.items()}


------------

Command line arguments
----------------------

``sys.argv`` is a **list** which contains the command line arguments

.. code-block:: python

    # hello.py
    
    import sys 
    print("Hello", sys.argv[1])

Running from the shell:

.. code-block:: none

    $ python hello.py "John"
    Hello John



