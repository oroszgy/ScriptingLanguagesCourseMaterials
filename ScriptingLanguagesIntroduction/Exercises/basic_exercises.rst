=============
Exercises
=============

1. Basics
---------

#. What are the values of the following expressions? (Why?)
    a. ``"a" + 1``
    b. ``type("3.14")``; ``type(type("3.14"))``
    b. ``type``; ``type(type)``
    c. ``2.0/3.0``; ``2.0/3``; ``2/3.0``; ``2/3``; 
    d. ``2//3``; ``2.5//2.1``; ``2.5%2.1``
    e. ``"a"<"b"``; ``"a"<"á"``; ``"á"<"b"``
    f. ``None``; ``type(None)``
    g. ``bool(1)``; ``bool(0.1)``; ``bool(0)``
    h. ``bool("a")``; ``bool("")``; ``bool(" ")``
    i. ``bool(bool)``; ``bool(None)``
    j. ``True or 2``; ``True and 2``
    k. ``1 or 2``; ``1 and 2``; ``0 and 1``; ``0 or 1``
    l. ``-1 and ("empty" and 0.0) or str(type(8 is (7+1)))[8:-3] is  "boo"``
    

#. Read two strings from the user and print their concatenation, without the first character of each. The strings will be at least length 1. E.g.: ``'Hello', 'There' → 'ellohere'``

#. Write a script that decides on a string (which is typed by the user) whether it is a palindrome.

#. Print "True" if the strings "cat" and "dog" appear the same number of times in the given string.

     .. code-block:: none
     
        $ python myscript.py < echo 'catcat'
        False
        $ python myscript.py < echo '1cat1cadodog'
        True

#. Transform a non-empty string (read from the user) like "Code" to another such as "CCoCodCode", "Program" to "PPrProProgProgrPrograProgram" etc.

#. Given 2 strings, ``a`` and ``b``. Count the number of the positions where they contain the same two character long substring. E.g. "xxcaazz" and "xxbaaz" yields 3, since the "xx", "aa", and "az" substrings appear in the same place in both strings.

#. Create a simple script that works like a calculator. It reads expressions from the user until "q" is inputted, then evaluates it and prints the results to the output.
    * The script should handle simple expressions containing only one operator.
    
#. Implement a script that evaluates Roman numbers that are given by the user. 
    * After printing the value, ask the user for the next task, till she types "quit".
    * Check the input before the evaluation!

2. Data structures
------------------

#. "One liners" -- use comprehension!

    #. Create a list of numbers in which the elements are less than 1000 and are not divisible by neither 2 or 5.
    #. Create a list with the even powers of 2 that are less than 100. 
    #. Create a list containing a the coordinates of a three dimensional (3x3x3) matrix. (``(1,1,1), (1,1,2) ... (3,3,3)``)
    #. Transform a string by omitting the lowercase characters.
    #. Calculate the symmetric difference of two sets.
    #. Split a multiline string into list of lists representing words in lines. (``E.g. [["First", "line"], ["Second", "line"]]``)
    

#. A sparse matrix is a matrix with a lot of 0 elements. We want to save memory by storing only the nonzero elements. Using the Python dictionary datatype, create a representation of sparse matrices, with the following interface:

    * ``m_new()`` -- returns an all-zero matrix
    * ``m_set(m, i, j, e)`` -- sets the value at row ``i``, column ``j`` to ``e``
    * ``m_get(m, i, j)`` -- returns the value at position ``(i,j)``
    
    Define the scalar multiplication as well: ``s_mul(mlambda, m)`` that returns a **new** matrix.
    
#. Write a script that takes a word from the user and prints a dictionary that counts the number of times each letter appears.
    
    a. Read the string as a command line argument, instead of interactively. 
    
#. A sparse vector is a vector whose entries are almost all zero, like [1, 0, 0, 0, 0, 0, 0, 2, 0]. Storing all those zeros wastes memory and dictionaries are commonly used to keep track of just the nonzero entries. For example, the vector shown earlier can be represented as {0:1, 7:2}, since the vector it is meant to represent has the value 1 at index 0 and the value 2 at index 7. Write a function / script that converts a dictionary to its sparse vector representation and vica versa.   

#. Write a function ``removeCommonElements(t1, t2)`` that takes in 2 tuples as arguments and returns a sorted tuple containing elements that are only found in one of them.

3. Functions
------------

#. Create a function: given a non-negative number ``num``, return ``True`` if ``num`` is within 2 of a multiple of 10.

#. We want to make a row of bricks that is goal inches long. We have a number of small bricks (1 inch each) and big bricks (5 inches each). Return ``True`` if it is possible to make the goal by choosing from the given bricks. This is a little harder than it looks and can be done without any loops.

    .. code-block:: python
    
        >>> make_bricks(3, 1, 8)
        True
        >>> make_bricks(3, 1, 9)
        False
        >>> make_bricks(3, 2, 10)
        True
        
#. Return the "centered" average of an array of integers, which we'll say is the mean average of the values, except ignoring the largest and smallest values in the array. If there are multiple copies of the smallest value, ignore just one copy, and likewise for the largest value. Use int division to produce the final average. You may assume that the array's length 3 or more.

    .. code-block:: python

        >>> centered_average([1, 2, 3, 4, 100])
        3
        >>> centered_average([1, 1, 5, 5, 10, 8, 7])
        5

#. Given an list of integers, return ``True`` if the array contains a 2 next to a 2 somewhere. 2 should be a (default) parameter.

    .. code-block:: python

        >>> has_x([1, 2, 2])
        True
        >>> has_x([1, 2, 1, 2])
        False
        >>> has_x([1, 3, 3, 2], 3)
        True

#. Write a function ``shiftByTwo(*args)`` that accepts a variable number of arguments and returns a tuple with the argument list shifted to the right by two indices. See the example below.

    .. code-block::

        >>> shiftByTwo(1,2,3,4,5,6)
        (5, 6, 1, 2, 3, 4)

#. Write a function ``sortByIndex(aList)`` that takes in a list of tuples in the following format: (index, value) and returns a new tuple with its elements sorted based by their index.

    .. code-block:: python

        >>> sortByIndex([(2,'Programming'), (3, 'is'), (1, 'Python'), (4, 'Fun')])
        ('Python', 'Programming', 'is', 'Fun')

#. Write a recursive function ``countX`` that takes a string and returns the number of uppercase 'X' characters in the string.

#. Write a function ``numbersInbetween(start, end)`` that takes in two numbers and returns a comma-separated string with all the numbers in between the start and end number inclusive of both numbers.

    .. code-block:: python

        >>> numbersInbetween(5, 10)
        '5,6,7,8,9,10'
        >>> numbersInbetween(5, 0)
        'Invalid'

#. Write a recursive function that traverses the tree given below and appends a new left node with the name ``42`` to each leaf node!

    .. code-block:: python

        Tree = {
            'name': 'animals',
            'left_branch': {
                'name': 'birds',
                'left_branch': {
                    'name': 'seed eaters',
                    'left_branch': {
                        'name': 'house finch',
                        'left_branch': None,
                        'right_branch': None,
                    },
                    'right_branch': {
                        'name': 'white crowned sparrow',
                        'left_branch': None,
                        'right_branch': None,
                    },
                },
                'right_branch': {
                    'name': 'insect eaters',
                    'left_branch': {
                        'name': 'hermit thrush',
                        'left_branch': None,
                        'right_branch': None,
                    },
                    'right_branch': {
                        'name': 'black headed phoebe',
                        'left_branch': None,
                        'right_branch': None,
                    },
                },
            },
            'right_branch': None,
        }

#. Implement a function called ``transmogr`` that returns all the values from an iterable that satisfy a predicate. Optionally, it applies a series of transforms to each returned value. The function takes these arguments:

    #. values -- A list of values. Actually, it could be any iterable.

    #. predicate -- A function that takes a single argument, performs a test on that value, and returns True or False.

    #. transforms -- (optional) A list of functions. Apply each function in this list and returns the resulting value. So, for example, if the function is called like this: `` transmogr([11, 22], p, [f, g])`` where ``f``, ``g`` and ``p`` are functions, ``p(11)==True`` and ``p(22)==False``, then the returned value should equal ``[g(f(11))]``
    
    *Optional: Implement this exercise as a generator function. (Apply all the transformations before yielding!)*

    
#. Implement the higher order functions ``map()``, ``filter()`` and ``reduce()``. They are built-ins but writing them by yourself might be a good exercise. You should use alternative function names, so that you can compare your solutions to the built-ins.

#. Using the higher order function ``filter()``, define a function ``filter_long_words(words, n)`` that takes a list of words and an integer ``n`` and returns the list of words that are longer than ``n``.
    a. use ``n=5`` as default parameter

#. Using the higher order function ``reduce()``, write a function ``max_in_list(nums)`` that takes a list of numbers and returns the largest one.

#. A memoized function is a function that remembers the returned values for all arguments it was previously called with. It does not calculate the result for the same arguments twice. Instead, it returns the remembered result. This is useful for expensive calculations. Your task is to write a function, that takes a regular function as argument and returns the memoized version.
        
#. Use builtin functions to:
    #. Count the number of characters in a list.
    #. Implement the following metric: list ``l1`` is *greater* than ``l2`` (with the same size), if at least half of the elements of ``l1`` is greater than their counterparts in ``l2`` (having the same index)
    #. Count whitespaces in a string.
    #. Create a dictionary from a set of strings (keys) with the number of their uppercase characters (as values).
    #. Calculate the value of *pi* iteratively.
    
    
#. Generate randomly a set of quadratic functions and find which has the maximal value in the discrete interval [0..10].

#. We want to make a row of bricks that is goal inches long. We have a number of small bricks (1 inch each) and big bricks (5 inches each). Return ``True`` if it is possible to make the goal by choosing from the given bricks. This is a little harder than it looks and can be done without any loops.

    .. code-block:: python
    
        >>> make_bricks(3, 1, 8)
        True
        >>> make_bricks(3, 1, 9)
        False
        >>> make_bricks(3, 2, 10)
        True

#. Return the "centered" average of an array of integers, which we'll say is the mean average of the values, except ignoring the largest and smallest values in the array. If there are multiple copies of the smallest value, ignore just one copy, and likewise for the largest value. Use int division to produce the final average. You may assume that the array's length 3 or more.

    .. code-block:: python

        >>> centered_average([1, 2, 3, 4, 100])
        3
        >>> centered_average([1, 1, 5, 5, 10, 8, 7])
        5        

4. I/O
------

#. Implement the Unix ``sort`` command: the program reads lines from a file (if it is given) or from the standard input then prints them in alphabetical order.

#. Implement the Unix ``tr`` command: the program reads lines from a file (if it is given as the last parameter) or from the standard input then replaces the first set of characters with the second set of characters.

    .. code-block:: guess
    
        $ echo "Hello" | tr "lo" "10"
        He110

  

#. Implement the following Unix commands (as before): 

    .. TODO:nem ismerik az emberek a unixos parancsokat - Marci
   
    a) ``uniq`` with the optional parameter ``-c``
    b) ``less``
    c) ``head``, ``tail`` with the optional ``-n `` parameter
    d) ``cut`` with the ``-f`` and ``-d`` options

#. From the standard input *recode* the Hungarian accents in the following way:

    .. code-block:: guess
    
        ó -> o' ő -> o" ö -> o: ü -> u: ű -> u" é -> e' á -> a' í -> i'

#. In cryptography, a Caesar cipher is a very simple encryption techniques in which each letter in the plain text is replaced by a letter some fixed number of positions down the alphabet. For example, with a shift of 3, A would be replaced by D, B would become E, and so on. The method is named after Julius Caesar, who used it to communicate with his generals. *ROT-13* ("rotate by 13 places") is a widely used example of a Caesar cipher where the shift is 13. In Python, the key for ROT-13 may be represented by means of the following format in a text file:

    .. code-block:: 
    
        'a':'n', 'b':'o', 'c':'p', 'd':'q', 'e':'r', 'f':'s', 'g':'t', 'h':'u',
        'i':'v', 'j':'w', 'k':'x', 'l':'y', 'm':'z', 'n':'a', 'o':'b', 'p':'c',
        'q':'d', 'r':'e', 's':'f', 't':'g', 'u':'h', 'v':'i', 'w':'j', 'x':'k',
        'y':'l', 'z':'m', 'A':'N', 'B':'O', 'C':'P', 'D':'Q', 'E':'R', 'F':'S',
        'G':'T', 'H':'U', 'I':'V', 'J':'W', 'K':'X', 'L':'Y', 'M':'Z', 'N':'A',
        'O':'B', 'P':'C', 'Q':'D', 'R':'E', 'S':'F', 'T':'G', 'U':'H', 'V':'I',
        'W':'J', 'X':'K', 'Y':'L', 'Z':'M'
            
    Your task in this exercise is to implement an encoder/decoder of ROT-13. Once you're done, you will be able to read the following secret message: ``"Pnrfne pvcure? V zhpu cersre Pnrfne fnynq!"s``
    Note that since English has 26 characters, your ROT-13 program will be able to both encode and decode texts written in English.

#. A *hapax legomenon* (often abbreviated to hapax) is a word which occurs only once in either the written record of a language, the works of an author, or in a single text. Define a function ``hapax(file_path)``that reads a text file and returns all of the hapaxes. 
    a. Make sure your program ignores capitalization.
    
#. In a game of Lingo, there is a hidden word, five characters long. The object of the game is to find this word by guessing, and in return receive two kinds of clues: 

    1. the characters that are fully correct, with respect to identity as well as to position, 
    2. the characters that are indeed present in the word, but which are placed in the wrong position. 
  
    Write a program with which one can play Lingo. Use square brackets to mark characters correct in the sense of 1), and ordinary parentheses to mark characters correct in the sense of 2). (Words to be guessed are stored in a text file.) Assuming, for example, that the program conceals the word "tiger", you should be able to interact with it in the following way:

    .. code-block:: none

        >>> import lingo
        snake
        Clue: snak(e)
        fiest
        Clue: f[i](e)s(t)
        times
        Clue: [t][i]m[e]s
        tiger
        Clue: [t][i][g][e][r]

   
#. From the `names.html<names.html>`_ file create a ``male_names.txt`` and a ``female_names.txt`` containing the most popular given names in 2011.

    * Use UTF-8 files.
    * Sort the names by their popularity.
    * Take the input and output file names command line arguments.

#. Create a "local search engine" that finds the text file in a directory structure that is the most relevant according to a search query. (Relevancy is calculated: ``# query words occurance / # words in the document``)

        .. code-block:: bash
        
            $ search.py "Barack Obama" ./
            ./subdir/presidents.txt   0.0236
        
    a) Make your app work recursively with the ``-r`` option! (you can use ``argparse`` module)
    b) Print the first ``n`` (5) documents with the ``-n 5`` option.
    
    
5. Regular expressions
----------------------

#. What do the following regular expressions mean?
    a) ``[.]``
    b) ``\**``
    c) ``^[*]+$``
    d) ``^\*+$``
    e) ``^#``
    f) ``^$``
    g) ``*.*``
    h) ``.{1,8}\..{3}``
    i) ``b[ae]n?``
    j) ``^(not|to|be)``
    k) ``([()])``
    l) ``</?[^>]+>``
    
#. Solve the following interactive exercises
    a) numbers http://regexone.com/example/0
    b) phone numbers http://regexone.com/example/1
    c) e-mail address http://regexone.com/example/2
    d) html tags http://regexone.com/example/3
    e) special file names http://regexone.com/example/4
    f) extracting information from a log file http://regexone.com/example/6

#. Write a regular expression that matches
    #. URLs,
    #. email addresses at PPKE ITK,
    #. Python lists that are not nested,
    #. bold parts of an HTML file,
    #. lines that have more than five **words**.


#. Collect the URLs from the `Pythagorean_theorem.html <Pythagorean_theorem.html>`_.
    
    a) How many of them are referreing to an element which is inside the document?
    b) Print them sorting by the number of their occurance!

#. Define a simple "spell check" function ``correct()`` that takes a string and transforms it as described below:
    1. two or more occurrences of the space character is compressed into one
    2. inserts an extra space after a period if the period is followed by a letter. 
    
    E.g. ``correct("This   is  very funny  and    cool.Indeed!")`` should return ``"This is very funny and cool. Indeed!"``

    .. tokenizacio fogalmat nem tanultuk; Unicode literal legujabb Python 3-ban kerult vissza, ez talan fontos !Javítva - így már érthetőbb?
    
#. In natural language processing, tokenisation is the process of splitting a sentence into tokens (that are either words or punctuation marks). Do a basic word tokenisation script for Hungarian texts which splits tokens with spaces.

    .. code-block:: python

        >> word_tokenize(u"Josh, this is a (very) nice day!")
        u"Jush ⬛, this is a (⬛ very ⬛) nice day ⬛!"

#. To translate numbers, dates or URL is a challenge for machine translation systems. These words greatly increase the vocabulary size because MT systems should learn all numburs one-by-one. The solution is placeholders. The task is to create a script which mark all matched numbers in parallel data and change them to a symbol.

    E.g.    ``I live in the 2nd floor.     A 2. emeleten lakom.``
        should become 
            ``I live in the ⬛num_1⬛ ⬛nd foor ⬛.      A ⬛num_1⬛ ⬛. emeleten lakom ⬛.``
            
    E.g.    `` The date is 26/03/2019.     Ma 2019. 03. 26.-a van.``
        should become
            ``The date is ⬛date_1⬛ ⬛.       Ma ⬛date_1⬛ ⬛. ⬛-⬛ a van ⬛.

#. Create a script which shortens a python script by removing all lines that are empty or contain only  comments. 


6. OOP
------

    .. Utolso reszfeladat eleg sokfelekeppen ertelmezheto ! Raktam példát a végére, így érthetőbb?

#. Implement a ``Point`` class that represents two dimensional points.
    A. Basics
        * define a constructor that takes two optional parameters with 0 default values, and assigns these values to ``x`` and ``y``
        * define a ``set(x,y)``, a ``get_x()`` and a ``get_y()`` method
    B. Operators (http://docs.python.org/3/reference/datamodel.html#special-method-names)
        * implement the plus operator
        * define a ``__str__`` method
        * implement ``__setitem__`` and ``__getitem__`` methods

    .. code-block:: python
        
        >>> p1 = Point(1,2)
        >>> p2 = Point(3,5)
        >>> print(p1+p2)
        Point(4, 7)
        >>> print(p1[0]+p1[1]+p2[0]+p2[1])
        11
            
    .. file belinkelese - Marci
#. Download the file ``BadKangaroo.py`` and find the error in the code.

    .. Design Patterns kovetkezo feleves targy, magyarazat szukseges, vagy ki is hagyhatjuk ezt a peldat
#. Implement the following design patterns:
    * Singleton (with lazy initialization) http://en.wikipedia.org/wiki/Singleton_pattern
    * Composite http://en.wikipedia.org/wiki/Composite_pattern

#. Implement a class for rational (``Rat``) numbers. Define the following functions:
    * add operator,
    * substraction operator,
    * constructor,
    * string representation,
    * multiplication operator\*,
    * divide operator\*.
    
    .. code-block:: python
    
            x = Rat(2,3)
            y = Rat(2,6)
            print(x) # 2/3
            print(y) # 1/3 (!)
            z = x+y
            print(z) # 1/1
            
    
    .. TODO Python 3-ra atirni (print fv stb.) tenylegesen tesztelni - Marci
#. Create a sparse vector representation (use dictionaries). Multiplication of two vectors should mean scalar product. Make your code compile against the following tests:

    .. code-block:: python
    
            ####### Basics #######
            
            x = SparseVector()
            x[1] = 1.0
            x[3] = 3.0
            x[5] = 5.0
            print('len(x)', len(x))
            for i in range(len(x)):
                print('...', i, x[i])

            y = SparseVector()
            y[1] = 10.0
            y[2] = 20.0
            y[3] = 30.0

            print(x) # [1.0, 0.0, 3.0, 0.0, 5.0]
            
            ####### Full exercise #######
            
            print('x + y', x + y)
            print('y + x', y + x)

            print('x * y', x * y)
            print('y * x', y * x)

            ####### Extra ##########
            
            z = [0.0, 0.1, 0.2, 0.3, 0.4, 0.5]

            print('x + z', x + z)
            print('x * z', x * z)
            print('z + x', z + x)
        
#. Implement an addition (``Add``) functor class. 
    a) With ``+``, ``*`` operators and string representation:
    
        .. code-block:: python
        
            a2 = Add(2)
            print(a2(1))     # 3
            a1 = Add(1)
            print(a1)        # "+1"
            a3 = a1+a2
            print(a3(1))     # 4
            a4 = a2*a2
            print(a4(1))     # 5
            
            
    b) With comparison and subtraction operators:
    
        .. code-block:: python
        
                print(a2 == a2, a1 < a2, a4 < a2)    # True, True, False
                print(a1-a2)     # "+-1'
                print(a2.plus)   # 2
                a2.plus = -1    # AttributeError

#. **Zoo animal hierarchy.** Consider the class tree shown in the figure.
    Implement six classes which model the taxonomy in the figure. (Use Python inheritance!) Then, add a ``speak()`` method to each class, this should print a unique message. Implement a ``reply()`` method as well in the top-level ``Animal`` superclass that calls ``self.speak`` to invoke the category-specific message printer. Finally, remove the speak method from your Hacker class so that it picks up the default above it. When you’re finished, your classes should work this way:
    
    .. image:: zoo.png
        
    .. code-block:: python

        >>> from zoo import Cat, Hacker
        >>> spot = Cat()
        >>> spot.reply()                   # Animal.reply; calls Cat.speak
        meow
        >>> data = Hacker()                # Animal.reply; calls Primate.speak
        >>> data.reply()
        Hello world!
        
#. Implement an ordered dictionary class! An instance object must remember the insertion order of the elements, thus when the elements are enumerated the (key,value) pairs should appear in the order of their insertion. (Hint: https://docs.python.org/3/library/stdtypes.html#dict.items)

    .. code-block:: python
    
        od = MyOrderedDict()
        od[1] = "a"
        od["hello"] = 0
        od[None] = 3.14
        
        for k,v in od.items():
            print(k,v)
        
        """
        Result:
            1 "a"
            "hello" 0
            None 3.14
        """
        
7. Lua
------

#. Create a linked list representation using tables.
    
    .. code-block:: lua 
        
        -- "a"->"l"->"m"->"a"
        print(list.element) 
        print(list.next.element)
    
    a) Store strings by reading the values from the standard input.
    b) If no more string is given print the list!
    c) Make your list double-linked.
    
#. Create an application that reads lines from the std. input and writes them back but ignores Lua-style comments.

#. Find assignments from a ``.lua`` file, then print each variable's value. (Use string matching!)

    a)
        .. code-block:: lua
        
            a = 42
            x,y = 1,3
            x,y = y,x
    b)
        .. code-block:: lua
        
            a,b,c = 42, 0
            a,b,c = 1,2,3,4
            
#. Implement a table that accesses indices in an *ignorcase* way.

    .. code-block:: lua
        
            tbl.x = 42
            print(tbl.x, tbl.X) -- 42, 42
            tbl.X = 24
            print(tbl.x, tbl.X) -- 24, 24
            
#. Create a type for rational numbers using metatables by implementing  multiplication and division operations.
