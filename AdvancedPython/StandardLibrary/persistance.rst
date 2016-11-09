Data persistance
----------------

-----------------------------------------------------

``pickle``
------------

The pickle module implements binary protocols for serializing and de-serializing a Python object structure. “Pickling” is the process whereby a Python object hierarchy is converted into a byte stream, and “unpickling” is the inverse operation.

-----------------------------------------------------

What can be pickled?
~~~~~~~~~~~~~~~~~~~~

* ``None``, ``True``, and ``False``
* numbers
* strings, bytes, bytearrays
* functions defined at the top level of a module (using def, not lambda)
* built-in functions defined at the top level of a module
* classes that are defined at the top level of a module

-----------------------------------------------------

* tuples, lists, sets, and dictionaries containing only picklable objects
* instances of such classes whose ``__dict__`` or the result of calling ``__getstate__()`` is picklable

-----------------------------------------------------

How?
~~~~

.. code-block:: python

    pickle.dump(obj, file)
    pickle.load(file)

    bytes_object = pickle.dumps(obj)
    pickle.loads(bytes_object)

-----------------------------------------------------

.. code-block:: python

    import pickle

    # An arbitrary collection of objects supported by pickle.
    data = {
    'a': [1, 2.0, 3, 4+6j],
    'b': ("character string", b"byte string"),
    'c': {None, True, False}
    }

    with open('data.pickle', 'wb') as f:
        pickle.dump(data, f)

-----------------------------------------------------

.. code-block:: python

    import pickle

    with open('data.pickle', 'rb') as f:
    # The protocol version used is detected automatically, so we do not
    # have to specify it.
        data = pickle.load(f)
-----------------------------------------------------

``shelve``
------------

A “shelf” is a persistent, dictionary-like object.

* backed by ``pickle``
* keys are ordinally strings
* the *values* in a shelf can be essentially arbitrary Python objects — anything that the pickle module can handle

-----------------------------------------------------

* works like an ordinary dictionary
* implements context manager

.. code-block:: python

    with shelve.open('spam') as db:
        db['eggs'] = 'eggs'


-----------------------------------------------------

``marshal``
------------

It contains functions that can read and write Python values in a binary format. The format is specific to Python, but independent of machine architecture issues.

* Udocumented on purpose.
* This is not a general “persistence” module.
* The marshal module exists mainly to support reading and writing the “pseudo-compiled” code for Python modules of .pyc files.

-----------------------------------------------------

JSON support
------------

Supports a ``pickle`` like serialization and deserialization of objects to JSON format.


.. code-block:: python

    import json

    json.dump(obj, file)
    json_dict = json.load(file)

    formatted_string = json.dumps(obj)
    json_dict = json.loads(formatted_string)

-----------------------------------------------------

CSV support
------------

The csv module implements classes to read and write tabular data in CSV format.

-----------------------------------------------------

.. code-block:: python

    import csv

    with open('eggs.csv', 'w', newline='') as csvfile:
        spamwriter = csv.writer(csvfile, delimiter=' ',
                                quotechar='|')
        spamwriter.writerow(['Spam'] * 5 + ['Baked Beans'])
        spamwriter.writerow(['Spam', 'Lovely Spam', 'Wonderful Spam'])

    with open('eggs.csv', newline='') as csvfile:
        spamreader = csv.reader(csvfile,
                                delimiter=' ',
                                quotechar='|')
        for row in spamreader:
            print(', '.join(row))
    # Spam, Spam, Spam, Spam, Spam, Baked Beans
    # Spam, Lovely Spam, Wonderful Spam


-----------------------------------------------------

.. code-block:: python

    import csv
    with open('names.csv', 'w') as csvfile:
        fieldnames = ['first_name', 'last_name']
        writer = csv.DictWriter(csvfile,
                                fieldnames=fieldnames)

        writer.writeheader()
        writer.writerow({'first_name': 'Baked',
            'last_name': 'Beans'})
        writer.writerow({'first_name': 'Lovely',
            'last_name': 'Spam'})

    with open('names.csv') as csvfile:
        reader = csv.DictReader(csvfile)
        for row in reader:
            print(row['first_name'], row['last_name'])



-----------------------------------------------------

XML support
------------

* ``xml.dom`` DOM API definition
* ``xml.sax`` SAX2 classes
* ``xml.etree`` ElementTree API, a simple and lightweight XML processor

https://docs.python.org/3.5/library/xml.etree.elementtree.html#module-xml.etree.ElementTree

-----------------------------------------------------

DOM example
~~~~~~~~~~~

.. code-block:: python

    from xml.dom import minidom

    doc = minidom.parse("staff.xml")
    # doc.getElementsByTagName returns NodeList
    name = doc.getElementsByTagName("name")[0]
    staffs = doc.getElementsByTagName("staff")
    for staff in staffs:
            sid = staff.getAttribute("id")
            nickname = staff.getElementsByTagName("nickname")[0]
            salary = staff.getElementsByTagName("salary")[0]

-----------------------------------------------------

SAX example
~~~~~~~~~~~~

.. code-block:: python

    import xml.sax

    class InkscapeSvgHandler(xml.sax.ContentHandler):
        def startElement(self, name, attrs):
            if name == "svg":
                for (k,v) in attrs.items():
                    print k + " " + v

    parser = xml.sax.make_parser()
    parser.setContentHandler(InkscapeSvgHandler())
    parser.parse(open("svg.xml","r"))
