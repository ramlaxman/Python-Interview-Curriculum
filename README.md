# Python-Interview-Questions
- Capgemini

#### What is a method?

A method is a function on some object x that you normally call as x.name(arguments...). Methods are defined as functions inside the class definition: class C: def meth (self, arg): return arg*2 + self.attribute.

#### How can I find the methods or attributes of an object?

For an instance x of a user-defined class, dir(x) returns an alphabetized list of the names containing the instance attributes and methods and attributes defined by its class.
Capgemini Python Technical Interview Questions And Answers

#### How do I call a method defined in a base class from a derived class that overrides it?

If you're using new-style classes, use the built-in super() function: class Derived(Base): def meth (self): super(Derived, self).meth() If you're using classic classes: For a class definition such as class Derived(Base): ... you can call method meth() defined in Base (or one of Base's base classes) as Base.meth(self, arguments...). Here, Base.meth is an unbound method, so you need to provide the self argument.

#### How can I organize my code to make it easier to change the base class?

You could define an alias for the base class, assign the real base class to it before your class definition, and use the alias throughout your class. Then all you have to change is the value assigned to the alias. Incidentally, this trick is also handy if you want to decide dynamically (e.g. depending on availability of resources) which base class to use. Example: BaseAlias = class Derived(BaseAlias): def meth(self): BaseAlias.meth(self) 

#### How do I find the current module name?

A module can find out its own module name by looking at the predefined global variable __name__. If this has the value '__main__', the program is running as a script. Many modules that are usually used by importing them also provide a command-line interface or a self-test, and only execute this code after checking __name__: def main(): print 'Running test...' ... if __name__ == '__main__': main() __import__('x.y.z') returns Try: __import__('x.y.z').y.z For more realistic situations, you may have to do something like m = __import__(s) for i in s.split(".")[1:]: m = getattr(m, i) 

#### How do I copy a file?

The shutil module contains a copyfile() function. 

#### How do I access a module written in Python from C?

You can get a pointer to the module object as follows: module = PyImport_ImportModule(""); If the module hasn't been imported yet (i.e. it is not yet present in sys.modules), this initializes the module; otherwise it simply returns the value of sys.modules[""]. Note that it doesn't enter the module into any namespace -- it only ensures it has been initialized and is stored in sys.modules. You can then access the module's attributes (i.e. any name defined in the module) as follows: attr = PyObject_GetAttrString(module, ""); Calling PyObject_SetAttrString() to assign to variables in the module also works.

#### How do I interface to C++ objects from Python?

Depending on your requirements, there are many approaches. To do this manually, begin by reading the "Extending and Embedding" document. Realize that for the Python run-time system, there isn't a whole lot of difference between C and C++ -- so the strategy of building a new Python type around a C structure (pointer) type will also work for C++ objects. 

#### How can I pass optional or keyword parameters from one function to another?

Collect the arguments using the * and ** specifier in the function's parameter list; this gives you the positional arguments as a tuple and the keyword arguments as a dictionary. You can then pass these arguments when calling another function by using * and **: def f(x, *tup, **kwargs): ... kwargs['width']='14.3c' ... g(x, *tup, **kwargs) In the unlikely case that you care about Python versions older than 2.0, use 'apply': def f(x, *tup, **kwargs): ... kwargs['width']='14.3c' ... apply(g, (x,)+tup, kwargs)

#### How do you make a higher order function in Python?

You have two choices: you can use nested scopes or you can use callable objects. For example, suppose you wanted to define linear(a,b) which returns a function f(x) that computes the value a*x+b. Using nested scopes: def linear(a,b): def result(x): return a*x + b return result Or using a callable object: class linear: def __init__(self, a, b): self.a, self.b = a,b def __call__(self, x): return self.a * x + self.b In both cases: taxes = linear(0.3,2) gives a callable object where taxes(10e6) == 0.3 * 10e6 + 2. The callable object approach has the disadvantage that it is a bit slower and results in slightly longer code. However, note that a collection of callables can share their signature via inheritance: class exponential(linear): # __init__ inherited def __call__(self, x): return self.a * (x ** self.b) Object can encapsulate state for several methods: class counter: value = 0 def set(self, x): self.value = x def up(self): self.value=self.value+1 def down(self): self.value=self.value-1 count = counter() inc, dec, reset = count.up, count.down, count.set Here inc(), dec() and reset() act like functions which share the same counting variable.

#### How do I convert a number to a string?

To convert, e.g., the number 144 to the string '144', use the built-in function str(). If you want a hexadecimal or octal representation, use the built-in functions hex() or oct(). For fancy formatting, use the % operator on strings, e.g. "%04d" % 144 yields '0144' and "%.3f" % (1/3.0) yields '0.333'. See the library reference manual for details.

#### What are the disadvantages of the Python programming language?

It is not best for mobile application
Due to interpreter its execution speed is not up to mark as compared to compiler
#### How is the Implementation of Python's dictionaries done?

Python dictionary needs to be declared first:
dict = { }

Key value pair can be added as:
dict[key] = value
    or
objDict.update({key:value})

Remove element by:
dict.pop(key)

Remove all:
objDict.clear()
A hash value of the key is computed using a hash function, The hash value addresses a location in an array of "buckets" or "collision lists" which contains the (key , value) pa...

#### What is used to create Unicode string in Python?
"u" should be added before the string
``
a=u"Python"
type(a) # will give you unicode
``
Add unicode before the string. Ex: unicode(text) resulting in text.
    
#### What is the built-in function used in Python to iterate over a sequence of numbers?

Syntax : range(start,end,step count)
Ex: a = range(1,10,2)
    print a

Output: [1, 3, 5, 7, 9]

If using to iterate
``
for i in range(1,10):
    print i
``
o/p:
``
    1
    2
    3
    4
    5
    6
    7
    8
    9
``
Range()
``
for i in range(10):
    print i
``
#### What is the method does join() in python belong to?

``.join([]).`` It takes any iterables into this method.
Join method is used to concatenate the elements of any list.

#### Does python support switch or case statement in Python?If not what is the reason for the same?

Dictionary can be used as case/switch .
Actually there is no switch statement in the Python programming language but the is a similar construct that can do justice to switch that is the exception handling.using try and except1,except2,except3.... and so on.

#### What is the statement that can be used in Python if a statement is required syntactically but the program requires no action?

pass

Code:
``
try x[10]:
    print(x)
except:
    pass
``
Use pass keyword over there like:
``
if a>0:
    print "Hello"
else:
    pass
``
pass keyword is used to do nothing but it fulfill the syntactical requirements.

#### What is used to represent Strings in Python.Is double quotes used for String representation or single quotes used for String representation in Python?

Both works in Python

Most preferable way by PEP 8 is in double quotes

 
#### Does Python support strongly for regular expressions? What are the other languages that support strongly for regular expressions?

Yes, Python Supports Regular Expressions Well.
There is a lot of other languages that have good support to RegEx-
    Perl
    Awk
    Sed
    Java
    etc.
 
Yes python strongly support regular expression. Other languages supporting regular expressions are: Delphi, Java, Java script, .NET, Perl, Php, Posix, python, Ruby, Tcl, Visual Basic, XML schema, VB script, Visual Basic 6.
 
#### How is memory managed in Python?

Python memory is managed by Python private heap space. All Python objects and data structures are located in a private heap. The programmer does not have an access to this private heap and interpreter...

Like other programming language python also has garbage collector which will take care of memory management in python.
 
#### Why can't lambda forms in Python contain statements?

Lambdas evaluates at run time and these do not need statements
Lambda is a anonymous function, which does not have a name and no fixed number of arguments. Represented by keyword lambda followed by statement.
Ex:
    sum = lambda a,b: a+b
    sum(2,3)
    output: 5
    Answer Question
      
    Select Best Answer

May 29 2015 08:23 AM
3412
Views
0
Ans
 
Encryption with AES/CBC/PKCS5

    radha
    Python Interview Questions

AES Encryption using CBC/PKCS5 padding in python while decrypting in java it is given below error

javax.crypto.BadPaddingException: Decryption error at sun.security.rsa.RSAPadding.unpadV15(Unknown Source) at sun.security.rsa.RSAPadding.unpad(Unknown Source) at com.sun.crypto.provider.RSACipher.doFinal(RSACipher.java:363) at com.sun.crypto.provider.RSACipher.engineDoFinal(RSACipher.java:389)...
Answer Question
Jan 04 2009 01:41 AM
7306
Views
1
Ans
 
Python Popularity

    ushanamballa
    Python Interview Questions

Why Python is not that much of popular, when compared to other programming languages?

    suji

        Mar 2nd, 2012

    Python is not so useful in web environment where the user interface is the browser. Hence, lot of people are using PHP for different design goals. Google is tightly connected with python as they make ...
    Answer Question
      
    Select Best Answer

Aug 02 2010 03:16 AM
7916
Views
1
Ans
 
Phyton Advantages and Dis-Advantages

    torch_619
    Python Interview Questions

What are the advantage and dis-advantage of Phyton programming language?

    suji

        Mar 2nd, 2012

    Python is more like java and bit cumbersome, but it leads to a better design. Python is an interpreted language, high level programming, pure object-oriented, high performance server side scripting la...
    Answer Question
      
    Select Best Answer

Jan 08 2007 11:23 AM
4501
Views
2
Ans
 
What is the optional statement used in a try ... except statement in Python?

    norman
    Python Interview Questions

    Priya Patel

        Oct 20th, 2007

    There are 2 optional clauses used in try...except statements: 1. else clause: It is useful for code that must be executed when the try block doesn't create any exception2. finally clause:Its is useful for code that must be executed irrespective of whether an exception is generated or not.
    xeio

        Sep 25th, 2007

    Try ... except (...) ... [finally]
    Answer Question
      
    Select Best Answer

Jan 08 2007 11:18 AM
4134
Views
1
Ans
 
What is List Comprehensions feature of Python used for?

    SachinDeo
    Python Interview Questions

    Priya Patel

        Oct 19th, 2007

    List comprehensions help to create and manage lists in a simpler and
    clearer way than using map(), filter() and lambda. Each list comprehension
    consists of an expression followed by a for clause, then zero or more for or
    if clauses.
    Answer Question
      
    Select Best Answer

Oct 10 2007 11:37 AM
3956
Views
0
Ans
 
What is __slots__ and when is it useful?

    Vince Gatto
    Python Interview Questions

Normally, all class objects have an __dict__ which allows new attributes to be bound to a class instance at runtime. When a class is defined with __slots__, only attributes whose names are present in the __slots__ sequence are allowed. This results in instances of this class not having an __dict__ attribute and not being able to bind new attributes at run time.__slots__ is useful because it eliminates...
Answer Question
Jan 08 2007 11:08 AM
5921
Views
1
Ans
 
Why isn't all memory freed when Python exits?

    Robert
    Python Interview Questions

    stranger1

        Sep 28th, 2007

    Objects referenced from the global namespaces of Python modules are not always deallocated when Python exits. This may happen if there are circular references. There are also certain bits of memory ...
    Answer Question
      
    Select Best Answer

Jan 08 2007 11:06 AM
3926
Views
1
Ans
 
Why was the language called as Python?

    nancyphilips
    Python Interview Questions

    stranger1

        Sep 28th, 2007

    At the same time he began implementing Python, Guido van Rossum was also reading the published scripts from "Monty Python's Flying Circus" (a BBC comedy series from the seventies, in the.
