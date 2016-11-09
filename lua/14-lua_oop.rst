OOP in Lua
==========

----

Tables and functions
--------------------

.. code-block:: lua

    t = {}

    function t.f(x) -- (*)
        print(x)
    end

    t:f() -- table: 0x12520c0 (**)
    t.f() -- nil
    

* ``(*)`` is the same as 
    * ``t.f = function(x) print(x) end`` or 
    * ``function t:f() print(t) end``
* ``(**)`` means ``t.f(t)``

-----

Objects
-------

.. code-block:: lua

    cplx = {re=1, im=1}

    function cplx.add(s, o)
        s.re, s.im= s.re + o.re, s.im+o.im
    end

    function cplx.str(s)
        return s.re.."+"..s.im.."i" 
    end

    cplx:add(cplx)
    print(cplx:str())

* ``self`` can be used instead of ``s``
* ``:`` syntax also works

-----

Simple *classes*
---------------

.. code-block:: lua

    Cplx = {}

    function Cplx.new()
        return {re = 1, im = 1}
    end

    function Cplx.add(s, o)
        return {re = s.re + o.re, im =s.im+o.im}
    end

    function Cplx.str(s)
        return s.re.."+"..s.im.."i" end

    x = Cplx.new()
    y = Cplx.add(x,x)
    print(Cplx.str(y))

-----

OOP with Closure approach
------------------------------------------

.. code-block:: lua

    Cplx = {
        -- constructor
        new = function()
            local self = {re=1, im=1}
            
            -- add method
            self.add = function(o)
                return {re =self.re + o.re,
                            im = self.im + o.im}
            end
            
            return self
        end,
        
        -- static methods
        get_origo = function() return {re=0, im=0} end,
        str = function(s) return s.re.."+"..s.im.."i" end
    }

----

.. code-block:: lua

    x = Cplx.new()
    y = x:add(x)
    print(Cplx.str(y)) -- 2+2i
    print(Cplx.str(Cplx.get_origo())) -- 0+0i

-----


Metatables, metamethods
-----------------------

* metamethods are associated with events, that occur when an operation is executed (e.g.: addition, comparision...)
* only tables and userdata types can have metamethods
* metatable is a regular table containing metamethods

.. code-block:: lua

    x = {re=1, im =2}
    print(x+x) -- error
    
    mt = {
        __add = function(a,b) 
            return {re=a.re+b.re, im=a.im + b.im}
        end
    }
    setmetatable(x, mt)

    y = x+x;  print(y.re, y.im) -- 2 4

* ``getmetatable`` is used to retrieve an object's metatable

-----

Metatables
----------

* but ``y+y`` won't work

    .. code-block:: lua

        mt = { -- new metatable definition
            __add = function(a,b) 
                return setmetatable({re=a.re+b.re, im=a.im + b.im}, mt)
            end
        }
        
        z = y+y
        print(z.re, z.im) -- 4 8
        
-----

Metamethods
-----------
http://lua-users.org/wiki/MetatableEvents

.. code-block:: lua

    __index -- read a value at a key
    __newindex -- assign a value for a key
    __call -- call the table as a function
    __metatable -- result of the getmetatable call
    __tostring -- print
    __unm -- '-'
    __add -- '+'
    __sub -- '-'
    __mul -- '*'
    __div -- '/'
    __pow -- '^'
    __concat -- '..'
    __eq -- '=='
    __lt -- '<'
    __gt -- '>'
    
-------

Prototypes
----------

.. code-block:: lua

    x = {s="hello"}
    y = {}
    setmetatable(y, {__index = x})
    print(y.s)

----

OOP with metatables
-------------------

.. code-block:: lua

    Cplx = {}

    function Cplx:new()
        return setmetatable({re=1, im=1}, self)
    end

    function Cplx:__add(other)
        return setmetatable({re=self.re+other.re, 
                            im=self.im+other.im},
                self)
    end

    function Cplx:__tostring()
        return self.re.."+"..self.im.."i"
    end

    x = Cplx:new()
    y=x+x
    print(y)

-----

.. code-block:: lua

    Cplx = {}

    function Cplx:new()
        return setmetatable({re=1, im=1}, Cplx)
    end

    function Cplx:__add(other)
        return setmetatable({re=self.re+other.re, im=self.im+other.im}, Cplx)
    end

    function Cplx:__tostring()
        return self.re.."+"..self.im.."i"
    end

    setmetatable(Cplx, 
        {__call = function() 
                    return Cplx:new() end})
    x = Cplx()
    y=x+x
    print(y)
    
-----

OOP Questions
--------------

* instances
* methods, attributes
* static methods / attributes
* (multiple-) inheritance
* information hiding
* polymorphism

http://lua-users.org/wiki/ObjectOrientedProgramming
