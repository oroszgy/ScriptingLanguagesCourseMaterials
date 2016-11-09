SciPy
======

--------------------------------------------------------

"... a Python ecosystem of software fot mathematics, science, engineering."

Core packages:

* **NumPy**
* **IPython**
* **matplotlib**
* SymPy
* SciPy library
* pandas
* nose

In addition, many others are built on top of it...

---------------------------------------------------------

SciPy library
-------------
* ``fftpack`` - discrete fourier transform algorithms
* ``integrate`` -  integration routines
* ``interpolate`` -  interpolation tools
* ``linalg`` -  linear algebra routines
* ``optimize`` -  optimization tools
* ``signal`` -  signal processing tools
* ``sparse`` -  sparse matrices
* ``stats`` -  statistical functions
* ``io`` -  data input and output
* ``special`` -  definitions of many usual math functions
* ``weave`` -  C/C++ integration

---------------------------------------------------------

``scipy.sparse``
-----------------

Data structure for representing sparse matrices

Compressed-Sparse-Row matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    """converts to CSR matrix"""
    X_csr = sparse.csr_matrix(X)
    
    """converts back to a dense array"""
    X_1 = X_csr.toarray()

* Suppports matrix algebra (e.g. ``X_csr.dot(y)``)

---------------------------------------------------------

List-in-List matrix
~~~~~~~~~~~~~~~~~~~

* effeicient element insertion

.. code-block:: python

    """converts to LIL matrix"""
    X_csr = sparse.lil_matrix(X)
    
    """converts back to a dense array"""
    X_1 = X_lil.toarray()
    
---------------------------------------------------------
    
Other data types
~~~~~~~~~~~~~~~~~

* CSC (compressed sparse column)
* BSR (block sparse row)
* COO (coordinate)
* DIA (diagonal)
* DOK (dictionary of keys)

---------------------------------------------------------

``scipy.linalg``
-----------------

http://docs.scipy.org/doc/scipy/reference/tutorial/linalg.html

* contains ``numpy.linalg`` and extends it
* might be faster (as it is compiled with BAS support)

---------------------------------------------------------


``scipy.stats``
---------------

* 80< continuous random variables & 10 discrete random variables
* statistical function
* ...


---------------------------------------------------------

``scipy.io``
-------------

Contains methods for reading and writing data

http://docs.scipy.org/doc/scipy/reference/tutorial/io.html

.. code-block:: python

    import scipy.io as sio
    mat_contents = sio.loadmat('my_file.mat')
    
    vect = np.arange(10)
    sio.savemat('np_vector.mat', {'vect':vect})

---------------------------------------------------------

``scipy.weave``
---------------

http://docs.scipy.org/doc/scipy/reference/tutorial/weave.html

Contains tools for including C/C++ code within Python.

* ``weave.inline()`` - compiles and executes C/C++ code on the fly
* ``weave.blitz()`` -  compiles NumPy Python expression for fast execution
* ``weave.ext_tools`` - classes for generating extension modules

---------------------------------------------------------


``SymPy``
---------------

http://sympy.org/en/index.html

* polynomials
* calculus
* equation solving
* combinatorics, discrete math
* geometry ...

.. code-block:: python

    expr = (x + y)**5
    expand(expr) 
    """x^5+5x^4y+10x^3y^2+10x^2y^3+5xy^4+y^5"""
    
.. code-block:: python

    l1 = Line(p1, p2)
    l2 = Line(p3, p4)
    px = intersection(l1, l2)


---------------------------------------------------------

``Pandas``
---------------

Tools for data analysis and modelling

* I/O tools for CSV/Excel/SQL/HDF5...
* data alignment tools with handling of missing data
* aggregating with a group by engine
* merging & joining
* time series functionality
* ...

http://pandas.pydata.org/

---------------------------------------------------------

``Other packages``
-------------------

Many other packages built on this library.

Examples:

* Mayavi - powerful 3D visualization
* Chaco - another plotting tool for embedded interactive plotting
* Cython - an extended Python language (extensions, integration, speed-up)

---------------------------------------------------------

``Scikits``
-------------------

http://scikits.appspot.com/scikits

Extra packages for specific functionality

* scikit-image
* scikit-bio
* scikit-learn
* cuda

---------------------------------------------------------

SciPy vs. Matlab
-----------------

http://wiki.scipy.org/NumPy_for_Matlab_Users

http://www.pyzo.org/python_vs_matlab.html

