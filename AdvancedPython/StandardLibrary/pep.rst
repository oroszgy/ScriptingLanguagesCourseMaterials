Python Enhancement Proposals (PEPs)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-------------------------------------------------------------------------

**Guido van Rossum** is known as a "Benevolent Dictator For Life" (BDFL), meaning that he continues to oversee the Python development process, making decisions where necessary.

.. image:: guido.jpg
-------------------------------------------------------------------------

"A PEP is a design document providing information to the Python community, or describing a new feature for Python or its processes or environment ... "

"... (are) the primary mechanisms for proposing major new features, for collecting community input on an issue, and for documenting the design decisions that have gone into Python."

"...maintained as text files in a versioned repository, their revision history is the historical record of the feature proposal..."

* https://www.python.org/dev/peps/
* https://wiki.python.org/moin/Topically%20Organized%20PEP%20List


-------------------------------------------------------------------------

PEP20 -- The Zen of Python
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: none

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

-------------------------------------------------------------------------

.. code-block:: none

    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!


-------------------------------------------------------------------------

PEP8
^^^^^

*Style Guide for Python code*

* Indentation: 4 spaces
* Line length: 79 chars
* Blank lines: 2 for top level methods class and 1 for methods inside classes
* Encoding: UTF-8 / ASCII
* separate ``import`` statements

-------------------------------------------------------------------------

* Naming conventions:
	* ``do_something(var_one, var_two)``
	* ``ClassName``
	* ``CONSTANT_VAR``
* etc.

A tool for checking your code: https://pypi.python.org/pypi/pep8

-------------------------------------------------------------------------

Docstrings
^^^^^^^^^^
`PEP 257 <http://legacy.python.org/dev/peps/pep-0257/>`_ (and some others)

"A docstring is a **string literal that occurs as the first statement** in a *module, function, class, or method* definition. Such a docstring becomes the **__doc__** special attribute of that object."


-------------------------------------------------------------------------

One-line docstring
'''''''''''''''''''

* one sentence
* using triple quotes (``"""``)
* no newline

.. code-block:: python

    def kos_root():
        """Return the pathname of the KOS root directory."""
        global _kos_root
        if _kos_root: return _kos_root

-------------------------------------------------------------------------

Multi-line docstring
''''''''''''''''''''

Is composed of a summary, a separating new line, and optional lines describing parameters, etc.

.. code-block:: python

    def complex(real=0.0, imag=0.0):
        """Form a complex number.

        Keyword arguments:
        real -- the real part (default 0.0)
        imag -- the imaginary part (default 0.0)
        """
        if imag == 0.0 and real == 0.0:
            return complex_zero
        ...

-------------------------------------------------------------------------

Recommended readings
^^^^^^^^^^^^^^^^^^^^^

* https://google-styleguide.googlecode.com/svn/trunk/pyguide.html
* http://docs.python-guide.org/en/latest/writing/style/

-------------------------------------------------------------------------

``doctest``
^^^^^^^^^^^^

Lets you test your code by running examples embedded in your docstrings.

It evaluates statements started with ``" >>>"`` and compares their results with the next lines.

.. code-block:: python

	def multiply(a, b):
		"""
		>>> multiply(4, 3)
		12
		>>> multiply('a', 3)
		'aaa'
		"""
		return a * b

-------------------------------------------------------------------------

Running doctests
'''''''''''''''''

.. code-block:: bash

	$ python3 -m doctest mydoctest.py
	$ python3 -m doctest -v mydoctest.py # verbose

or

.. code-block:: python

	import doctest

	"""Your code"""

	if __name__ == "__main__":
		doctest.testmod()

-------------------------------------------------------------------------

Context managers
~~~~~~~~~~~~~~~~~

A context manager (`PEP 343 <http://legacy.python.org/dev/peps/pep-0343/>`_) is an object with ``__enter__`` and ``__exit__`` methods which can be used in the with statement. It permits e.g. the extraction of the exception handling structure into a class.

-------------------------------------------------------------------------

.. code-block:: python

    with manager as var:
        do_something(var)

	# is in the simplest case equivalent to

    var = manager.__enter__()
    try:
        do_something(var)
    finally:
        manager.__exit__()

-------------------------------------------------------------------------

Context managers are implemented in the std. library in several places, such as
    * ``file``
    * ``ftplib``
    * ``tempfile``, etc.

An example for files:

.. code-block:: python

    with open('/tmp/file', 'a') as f:
        # the file gets closed whatever happens
        f.write('more contents\n')

-------------------------------------------------------------------------

Type hints
~~~~~~~~~~

https://www.python.org/dev/peps/pep-0484/

.. code-block:: python

	def greeting(name: str) -> str:
		return 'Hello ' + name

-------------------------------------------------------------------------

.. code-block:: python

	Url = str
	def retry(url: Url, retry_count: int) -> None:
		pass



	from typing import TypeVar, Iterable, Tuple

	T = TypeVar('T', int, float, complex)
	Vector = Iterable[Tuple[T, T]]

	def inproduct(v: Vector) -> T:
		return sum(x*y for x, y in v)
