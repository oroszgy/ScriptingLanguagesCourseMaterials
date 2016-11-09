Concurrency
===========

------------------------------------------------------------

Basic concepts
---------------

* multitasking
* simultaneous task execution
* CPU bound tasks
* I/O bound tasks
* shared memory
* threads
* processes
* distributed computing

------------------------------------------------------------

Things to consider

* Performance of the
	* application
	* programmer

* whether your problem is CPU or IO bound

------------------------------------------------------------

``threading``
-------------

https://docs.python.org/3/library/threading.html

"..this module is loosely based on Java’s threading model..."

------------------------------------------------------------

``Thread`` class
    * ``is_alive()``
    * ``join()``
    * ``start()``
    * ``run()`` # Contains the implementation of the thread
    * ``setDaemon()``

------------------------------------------------------------

.. code-block:: python

	import threading

	class MyThread(threading.Thread)
	    def run(self):
	        """thread worker function"""
	        print('Worker')

	t = MyThread()
	t.start()


------------------------------------------------------------

.. code-block:: python

    import threading

    def worker():
        """thread worker function"""
        print('Worker')

    t = threading.Thread(target=worker)
    t.start()

------------------------------------------------------------

Accessing to shared data
--------------------------

Thread synchronization primitives:

* Lock
* RLcok
* Sempahore
* Event
* Condition

------------------------------------------------------------

``Lock``
---------

Mutex exclusion lock

.. code-block:: python

	x_lock = threading.Lock()

	x_lock.acquire()
	# ..critical section
	x_lock.relase()

------------------------------------------------------------

... or with context managers:


.. code-block:: python

	x_lock = threading.Lock()

	with x_lock:
		# critical section

------------------------------------------------------------

``RLock``
---------

Reentrant mutex lock:

* it can be reacquired multiple times **by the same thread**
* only one thread is allowed to execute

------------------------------------------------------------

``Semaphore``
------------

* ``acquire()`` -- wait if the count is 0
* ``relase()`` -- increment the count
* they can be called in any order by any thread

------------------------------------------------------------

``Event``
---------

Used for notifying threads about an event.

* Easy wating instead of busy loops
* Broadcasting massages

.. code-block:: python

	e = threading.Event()
	e.isSet() # Returns True if the event is True
	e.set() # Sets event to True
	e.clear() # Sets event ot False
	e.wait() # Waits until event becomes True

------------------------------------------------------------

``Condition``
--------------

Is a combination of locking and signalling

.. code-block:: python

	cv = threading.Condition() # create a condition with an optional lock parameter
	cv.acquire() # Acquire the underlying lock
	cv.release() # Release the underlying lock
	cv.wait() # Wait for condition
	cv.notify(n=1) # Wake up one thread witing on this condition
	cv.notifyAll() # Wake up all threads waiting on this condition

------------------------------------------------------------

.. code-block:: python

	"""Producer thread"""
	# ... generate item
	condition.acquire()
	# ... add item to resource
	condition.notify() # signal that a new item is available
	condition.release()

	"""Consumer thread"""
	condition.acquire()
	while True:
	    # ... get item from resource
	    if item:
	        break
	    condition.wait() # sleep until item becomes available
	condition.release()
	# ... process item

------------------------------------------------------------

... but
-------

* deadlocks are easy to create
* non-deterministic scheduling
* ...

------------------------------------------------------------

``Queue``
--------------

* **thread safe**
* Instead of sharing the memory, you can send data between threads.
* Queues are a convenient way to organize applications in a producer/consumer model.

------------------------------------------------------------

Usage:
~~~~~~

.. code-block:: python

	from Queue import Queue
	q = Queue([maxsize]) # Create a queue
	q.put(item) # Put an item on the queue
	q.get() # Get an item from the queue
	q.empty() # Check if empty
	q.full() # Check if full

	q.task_done() # Signal that work is done
	q.join() # Wait for all work to be done

------------------------------------------------------------

Global Interpreter Lock
------------------------

**But Python has a Global Interpreter Lock (GIL)**
    * thus only one thread can be executed at the same time
    * not efficient on CPU intense tasks
    * however, it can only help on I/O bounded tasks
    * threads are necessary for GUI apps

------------------------------------------------------------

* A thread is a real system thread
* managed by the host OS
* only one python thread can be executed in the interpreter
* whenever a thread runs it holds the GIL

------------------------------------------------------------

Sulutions
---------

* message passing:
	1. Create several Python applications
	2. Implement a Message passing protocol

* use processes from the ``multiprocessing`` module

------------------------------------------------------------

``multiprocessing``
--------------------

* The ``multiprocessing`` module provides access to processes instead threads.
* Meaning, that there are no shared memory spaces!
* You can use the **same API shown for threads**

------------------------------------------------------------

.. code-block:: python

	import multiprocessing

	class MyProcess(multiprocessing.Process):
		def run(self):
			print("Hello")

Easy way:

.. code-block:: python

    import multiprocessing

    def worker():
        """thread worker function"""
        print('Worker')

    t = multiprocessing.Process(target=worker)
    t.start()


------------------------------------------------------------



``Pipe``
---------

Pipes are a pair of connection objects for sending and receiving objects

``(c1, c2) = multiprocessing.Pipe()``


.. code-block:: python

	c.send(obj) # Send an object
	c.recv() # Receive an object
	c.send_bytes(buffer) # Send a buffer of bytes
	c.recv_bytes([max]) # Receive a buffer of bytes
	c.poll([timeout]) # Check for data

------------------------------------------------------------

.. code-block:: python

	import multiprocessing

	def consumer(p1, p2):
		x = p2.recv()
		print(x)

	p1, p2 = multiprocessing.Pipe()
	cons = multiprocessing.Process(
		target=consumer,
		args=(p1, p2)
	)
	cons.start()
	item = "alma"
	p1.send(item)
	p1.close()
	cons.join()

------------------------------------------------------------

``Queue``
---------

* Processes can be also used with queues.
* They are implemented on top of pipes

.. code-block:: python

	from multiprocessing import Queue
	q = Queue()
	q.put(item) # Put an item on the queue
	item = q.get() # Get an item from the queue

------------------------------------------------------------

``Pool``
~~~~~~~~

"One can create a pool of processes which will carry out tasks submitted to it with the Pool class."

Processes can be started using:

* ``apply(func[, args[, kwds]])``
* ``apply_async(func[, args[, kwds[, callback[, error_callback]]]])``
* ``map(func, iterable[, chunksize])``
* ``map_async(func, iterable[, chunksize[, callback[, error_callback]]])``

Async methods yields an ``AsyncResult`` object

------------------------------------------------------------

.. code-block:: python

	from multiprocessing.pool import Pool

	def f(x):
	    print(x)
	    return x*x

	with Pool(processes=4) as pool:
	    result = pool.apply_async(f, (10,))
	    print(result.get(timeout=1))

	    print(pool.map(f, range(10)))

	    res = pool.map_async(f, range(10))
	    pool.close()
	    pool.join()
	    print(res.get())

------------------------------------------------------------


``concurrent.futures``
----------------------

http://python.org/dev/peps/pep-3148/

"provides a high-level interface for asynchronously executing callables ... using":

* Executors
    * ``ThreadPoolExecutor`` vs  ``ProcessPoolExecutor``
    * ``submit, map`` is used for starting execution

------------------------------------------------------------

* ``Future`` objects
    * is returned when a process/thread is executed
    * it can be used to monitor the execution
    * ``cancel, done, result, exception, add_done_callback``


------------------------------------------------------------

.. code-block:: python

    import concurrent.futures
    CORES = 4

    def hard():
        print(99*99)

    monitors = []
    with concurrent.futures.ProcessPoolExecutor(
            max_workers=CORES) as ex:
        for num in range(CORES):
            f = ex.submit(hard)
            monitors.append(f)
