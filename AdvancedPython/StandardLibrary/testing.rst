Testing
-------

------------------------------------------------------------

``assert``
~~~~~~~~~~

* you can insert debugging assertions to any program

``assert expression_to_check [, expression_to_raise]``

.. code-block:: python

    >>> x=21
    >>> assert x==21
    >>> assert x==42, ":("
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    AssertionError: :(
    


------------------------------------------------------------

``unittest``
~~~~~~~~~~~~

https://docs.python.org/3/library/unittest.html

Basic concepts
    * test fixture -- the preparations/cleanups needed to perform one or more tests
    * test case -- checks for a specific response to a particular set of inputs
    * test suite -- is a collection of test cases, test suites
    * test runner -- orchestrates the execution of tests and provides the outcome to the user

------------------------------------------------------------

In practice
^^^^^^^^^^^

    * ``TestCase`` -- a test case is created with subclassing
        * ``test_someMethod`` -- a test is performed by defining a method 
        * ``setUp()`` -- is run before each test
        * ``tearDown()`` -- is run after each test
        * `assertions methods <https://docs.python.org/3/library/unittest.html#unittest.TestCase.debug>`_
            * ``assertEqual``, ``assertNotEqual``
            * ``assertTrue``, ``assertFalse``
            * ``assertIs``, ``assertIsNot``
            * ``assertIn``, ``assertNotIn``
            * ...

            
------------------------------------------------------------

A test (suite/case) can be run with: ``unittest.main()`` or

.. code-block:: bash
    
    $ python -m unittest test_module1 test_module2
    $ python -m unittest test_module.TestClass
    $ python -m unittest test_module.TestClass.test_method

        
------------------------------------------------------------

Example
^^^^^^^
.. code-block:: python

    import random
    import unittest

    class TestSequenceFunctions(unittest.TestCase):

        def setUp(self):
            self.seq = list(range(10))

        def test_shuffle(self):
            # make sure the shuffled sequence does not lose any elements
            random.shuffle(self.seq)
            self.seq.sort()
            self.assertEqual(self.seq, list(range(10)))

            # should raise an exception for 
            # an immutable sequence
            self.assertRaises(TypeError, 
                              random.shuffle, (1,2,3))
            
------------------------------------------------------------

.. code-block:: python

        def test_choice(self):
            element = random.choice(self.seq)
            self.assertTrue(element in self.seq)

        def test_sample(self):
            with self.assertRaises(ValueError):
                random.sample(self.seq, 20)
            for element in random.sample(self.seq, 5):
                self.assertTrue(element in self.seq)

    if __name__ == '__main__':
        unittest.main()



