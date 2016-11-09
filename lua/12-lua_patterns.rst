Pattern matching in Lua
===================================

--------------

Similarity (Regexps)
---------------------

-  subset of the the standard regexps
-  basic workflow

   -  single character matches itself
   -  characters with special meaning: ``^$()%.[]*+-?``
   -  ``[^ ]`` character sets
   -  ``*,+,?`` multiple match

-  capture groups
-  ``^`` and ``$`` match the start / end of the string

http://www.lua.org/manual/5.1/manual.html#5.4.1

--------------

Differences(Regexps)
---------------------

-  escape character ``%``
-  ``[ ]`` predefined sets can be used inside
-  ``-`` non greedy matching 
-  ``%n`` refers to a capturing group

Character classes
-----------------

.. code-block:: none

    %a  letters
    %d  digits
    %l  lower characters
    %s  whitespace
    %w  alfanumeric characters
    ...

--------------

Operations
----------

-  ``string.match(s, pattern [, init])``
   -  matches a string with a pattern
   -  returns ``nil`` or the matching string(s)

-  ``string.gmatch (s, pattern)``
   -  returns an iterator function 

.. code-block:: lua

    s = "hello world from Lua"
    for w in string.gmatch(s, "%a+") do
        print(w)
    end
    t = {}, s = "from=world, to=Lua"
    for k, v in string.gmatch(s, "(%w+)=(%w+)") do
        t[k] = v
    end

--------------

Operations
----------

-  ``string.find (s, pattern [, init [, plain]])``

   -  returns the beginning and the end of the match
   -  in case of ``plain = true`` simple string matching
   -  with **capture groups** it also returns the matched strings

-  ``string.gsub (s, pattern, repl [, n])``

   -  returns a new string and the number of times when it replaced a substring
   -  possible values of ``repl`` parameter:

      -  **string** (%n, %0, %%)
      -  **table** -- keys are patterns values are replacements
      -  **functions** -- called when the pattern matches

--------------

.. code-block:: lua

     x = string.gsub("hello world", "(%w+)", "%1 %1")
     -- x="hello hello world world"

     x = string.gsub("hello world", "%w+", "%0 %0", 1)
     -- x="hello hello world"

     local t = {name="lua", version="5.1"}
     x = string.gsub("$name-$version.tar.gz", "%$(%w+)", t)
     -- x="lua-5.1.tar.gz"

