Regular expressions in Python
=============================

------------------------------

Regular expressions
---------------------

* each character match itself, except some specials::

	. ^ $ * + ? { } [ ] \ | ( )


+------------+-----------------------------+---------------+
| Operator   |           Meaning           |   Example     |
+============+=============================+===============+
| ``.``      | match any character         | ``k.r``       |
+------------+-----------------------------+---------------+
| ``\``      | escape character            | ``\.``        |
+------------+-----------------------------+---------------+
| ``[]``     | define a character class    | ``b[ae]n``    |
+------------+-----------------------------+---------------+
| ``[first-``| character class between the | ``[0-9]``     |
| ``last]``  | ``first`` and the ``last``  | ``[a-z]``     |
+------------+-----------------------------+---------------+
| ``[^]``    | not matching the class      | ``[^<>]``     |
+------------+-----------------------------+---------------+
| ``?``      | matches 0 or 1 time         | ``fája?``     |
+------------+-----------------------------+---------------+
| ``+``      | matches at least once       | ``ps+zt!``    |
+------------+-----------------------------+---------------+
| ``*``      | matches 0 or more times     | ``bo.*ka``    |
+------------+-----------------------------+---------------+

----------------------

+------------+-----------------------------+---------------+
| Operator   |          Meaning            |    Example    |
+============+=============================+===============+
| ``{m,n}``  | matches ``m<  <n``     times| ``:\){1,5}``  |
+------------+-----------------------------+---------------+
| ``^``      | matches starting position   | ``^a``        |
+------------+-----------------------------+---------------+
| ``$``      | matches ending positions    | ``.*!$``      |
+------------+-----------------------------+---------------+
| ``|``      | choice                      | ``(c|h)at``   |
+------------+-----------------------------+---------------+
| ``()``     | capture group               | ``.*(b.n)``   |
+------------+-----------------------------+---------------+
| ``\n``     | reference for the n. group  | ``(ab)\1*``   |
+------------+-----------------------------+---------------+

--------------

... in Python
----------------------

http://docs.python.org/3/library/re.html

* us the ``re`` module
* some of the predefined character classes
    * ``\d`` - numerals
    * ``\D`` - not numerals
    * ``\s`` - whitespaces
    * ``\S`` - not whitespaces
    * ``\w`` - alphanumeric characters
    * ``\W`` - not alphanumeric characters
    
* the ``\`` is also an escape character in Python
* ``r"\n"`` is a raw string with length of 2

-------------------------

Matching functions
~~~~~~~~~~~~~~~~~~

``re.match(pattern, str)``

* matching from the first character of the string
* returns a ``MatchObject``, or ``None`` 

``re.search(pattern, str)``

* search the pattern in the whole strign
* returns a ``MatchObject``, or ``None``

-----------------------

``MatchObject``
~~~~~~~~~~~~~~~
* its boolean value is always ``True``
* ``.group(0)`` - the whole match
* ``.group(n)`` - the match of the ``n.`` capture group

.. code-block:: python

    m = re.match("(\\w+) \\(w+)", "Barack Obama")
    print(m.group(0)) # "Barack Obama"
    print(m.group(1)) # "Barack"
    print(m.group(2)) # "Obama"
    print(m.group(1,2)) # ("Barack", "Obama")

* ``.start(n)`` returns the starting position of the ``n.`` group
* a ``.end(n)`` returns the ending position of the ``n.`` group

---------------------------

Find
~~~~~~~
``re.findall(pattern, str)``

* finds all the matching substrings
* returns a list of strings

``re.finditer(pattern, str)``

* returns an iterator of ``MatchObject``

-----------------

Substitution, split
~~~~~~~~~~~~~~~~~~~

``re.sub(pattern, replacement, str)``

* substitution in the string: returns a new one

.. code-block:: python

    import re
    print re.sub("túró", "....", "Elmész a túróba!")

``re.split(pattern, string)``

* splits the strings leaving out the matching parts
* returns a list of strings

.. code-block:: python

    >>> re.split("\d+", "1a2b3c")
    ['', 'a', 'b', 'c']


----------------------------

Flags
~~~~~~~~~
Most of the functions accepts them through ``flags`` parameter:
    * ``re.I`` - ignore case
    * ``re.A`` - predefined classes matches ASCII strings
    * ``re.L`` - predefined classes matches became locale dependent (deprecated)
    * ``re.S`` - ``.`` character matches all (including newline)
    * ``re.M`` - ``^`` and ``$`` work also for lines
    * ``re.X`` - whitespaces are ignored, ``#`` can be used to comment 

--------------------------------------------------------------------------------

Efficiency
~~~~~~~~~~~~~~~~~~

* each ``match``, ``search``, .... call interprets the *regex*
* sometimes useful for compile it
* creates a ``Pattern`` object


.. code-block:: python

    import re
    import sys
    myregexp = re.compile("\\d+")
    for line in sys.stdin:
        if myregexp.match(line):
            print line

* ``re.escape`` can be used to escape a string

.. code-block:: python

    >>> re.escape("^.*\\(][)")
    '\\^\\.\\*\\\\\\(\\]\\[\\)'
