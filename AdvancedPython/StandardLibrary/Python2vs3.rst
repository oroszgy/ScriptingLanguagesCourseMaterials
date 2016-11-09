=============
Python 2 vs 3
=============

--------------------------------------------------------------------------------

Basics
------

* Python 3 is incompatible with 2.x
    * due to code clean-up
* some changes have been backported:
    ``from __future__ import ...``
* forced name conventions

--------------------------------------------------------------------------------

Details:

* http://docs.python.org/2/library/__future__.html
* http://docs.python.org/3.0/whatsnew/3.0.html
* http://wiki.python.org/moin/Python2orPython3
* http://docs.python.org/2/library/2to3.html

--------------------------------------------------------------------------------

``print``
---------

* became a function
* ``from __future__ import print_function``

.. code-block:: python

    Old: print "The answer is", 2*2
    New: print("The answer is", 2*2)

    Old: print x,           # Trailing comma suppresses newline
    New: print(x, end=" ")  # Appends a space instead of a newline

    Old: print              # Prints a newline
    New: print()            # You must call the function!

    print("It is", 2**32, "!", sep="")

-----

Views and Iterators vs Lists
----------------------------

* ``dict.keys()``, ``dict.items()`` was lists but became views
* ``dict.iterkeys(), iteritems() and itervalues()`` not supperted anymore
* ``map(), filter()`` return iterators
* ``range()`` became a generator
* ``zip()`` became an iterator

----

Ordering, comparisions
----------------------

* ``1 < ''``, ``0>None`` raise ``TypeError``
* ``sort()`` and ``sorted()`` no longer accepts ``cmp`` argument, thus ``key`` should be used

Integers
--------

* ``long`` renamed to ``int``
* ``1/2`` equals ``0.5``
* ``1.0//2.0`` equals ``0.0``
* there is no upper bould for an integer
* ``sys.maxint`` is used as a theoretic maximum

------

Text
-------
Text vs. data:

* all text is Unicode with type ``str``
* data is stored in ``bytes``
* conversion between bytes to strings: ``encode(), decode()``
* ``basestring`` type is deprecated

* ``u".."`` is no longer valid

----

Text
----

Internal changes:

* all API functions uses Unicode strings
* default source encoding is UTF-8
* non-ASCII letters are allowed in identifiers

* ``open()`` use an encoding to map files
* ``StringIO`` became ``io.StringIO``

------

New syntax
-----------

.. code-block:: python

    # Extended unpacking
    a,b, *rest = some_sequence
    *rest, a,b = some_sequence

    # dict comprehension
    {k:v for k,v in stuff.items()}

    # set comprehension
    {k for k in stuff}

----

Changed syntax
--------------
* new Metaclass syntax "``class C(metaclass=M)``"
* ``raw_input()`` became ``input()``
* new style classes are default:
    "``class A: pass``" and
    "``class A(object): pass``" are equal

-----

* ``nonlocal`` statement: reach an outer but non-blobal
* ``True``, ``False``, ``None`` are reserved words

-----

Exceptions
----------

Simplified ``except``, thus only allowed constructions are:

.. code-block:: python

    except ValueError as e:
        pass

    except (ValueError, TypeError) as e:
        pass

Simplified ``raise`` statement: "``raise Exception(args)``"

----

Others
------
* ``long`` and ``int`` types were merged
* updated integer literals
* library changes
* applied naming conventions
* "``%``" string formatting is deprecated, use the ``format`` function:
    ``"The story of {0}, {1}, and {c}".format(a, b, c=d)``

http://dev.pocoo.org/~gbrandl/py3
