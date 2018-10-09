# Python-Interview-Questions

- ##### Introduction
- ##### Data Types
- ##### Loops
- ##### Built in Data Structure
- ##### List
- ##### Tuple
- ##### Set
- ##### Frozenset
- ##### Dictionary
- ##### Ordered Dictionary
- ##### _String_
- ##### Function
- ##### Inheritance
- ##### Classes & Objects
- ##### Exceptions





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
At the same time he began implementing Python, Guido van Rossum was also reading the published scripts from "Monty Python's Flying Circus" (a BBC comedy series from the seventies, in the.

What are Mutable and Immutable Data structures in Python ?
What are tuples ?
What is difference between tuple and list ? Where will you use tuple and where will you use list ?
What is Dynamic Typing ?
Justify this statement : Everything is object in Python ?
Python is Call by Value or Call by Reference ?
    How do you create a dictionary which can preserve the order of pairs?
    Can you use mutable Data Structure as key in Dictionaries ?
    What is the use of enumerate() in Python?
    What are *args, **kwargs ?
    How instance variables are different from class variables?
    Differentiate between “*.py” file and “*.pyc” file?
    Explain difference between Map vs Reduce Vs Filter ?
    What are Lamda Functions ?
    What is List comprehension ?
    What is __init__ functions ?
    What are Generators ?
    What are Iterators ?
    Can generator be used to create Iterators ? Give example
    Can iterators be used to create generator ?
    Differentiate between Range and Xrange ?
    What is Method Resolution Order ?
    Python supports Multi-Level Inheritance or Multiple Inheritance or Both ?
    Does Python supports multi-threading ?
    What is multi-threading? What is GIL(Global interpreter lock) issue ?
    What are decorator ? How to create custom decorator ?
    How memory is managed in Python ?
    How does Python's garbage collection work?
    What are Regular Expressions ?
    Differentiate between append() and extend() methods ?
    What is Web Scraping? How do you achieve it in Python?
    Explain the use “with” statement in python?
    What are Middlewares ?
    What is Monkey patching ? Give example ?
    What's the difference between py2.x and py3.x ?
    Give examples of Python Framework ?

What is Python , Explain features of Python.
How Python is interpreted.
Explain dict.
How to pass optional or keyword arguments.
Explain indexing and slicing.
What is lambda.
Difference between str() and repr().
Explain serialization and deserialization / Pickling and unpicking.
What is list / dict compression.
What are higher ordered functions.
How to copy object in Python. Diff between shallow copy and deep copy.
How to make array in python.
How to generate random numbers.
How to handle exceptions.
When to use list/tuple/set.
Disadvantageous of python.
Diff range() and xrannge()
What is PEP8
What is virtualenv
Diff between Python 2.* and 3.*
What is decorator, usage ?
With statement and its usage.
What is class and what is self.
Explain isinstance()
What is static method, class method and instance method
Treading in python
What are iterators and generators
Explain map, filter,reduce and lambda.
Difference between new styled classed and old styled classes.
What is diff between Python and Java
What is context processor.
What is exec() and eval ()
How to pass command line argument.
What is yield ?
What is ord() and chr()
What are Metaclasses.
What is descriptor ?
Any 10 python packages you have used.
What is namespace in Python? namespace vs scope ?
What is MRO ?
== vs is ?
mutable vs immutable

1. Compare Java & Python
Criteria 	Java 	Python
Ease of use 	Good 	Very Good
Speed of coding 	Average 	Excellent
Data types 	Static typed 	Dynamically typed
Data Science & machine learning applications 	Average 	Very Good
2. What is Python?

Python is a high-level, interpreted, interactive and object-oriented scripting language. Python is designed to be highly readable. It uses English keywords frequently where as other languages use punctuation, and it has fewer syntactical constructions than other languages.
3. What is the purpose of PYTHONPATH environment variable?

PYTHONPATH − It has a role similar to PATH. This variable tells the Python interpreter where to locate the module files imported into a program. It should include the Python source library directory and the directories containing Python source code. PYTHONPATH is sometimes preset by the Python installer

Learn for free ! Subscribe to our youtube Channel.

4. What is the purpose of PYTHONSTARTUP,PYTHONCASEOK,PYTHONHOME,PYTHONSTARTUP environment variables?

PYTHONSTARTUP − It contains the path of an initialization file containing Python source code. It is executed every time you start the interpreter. It is named as .pythonrc.py in Unix and it contains commands that load utilities or modify PYTHONPATH

PYTHONCASEOK − It is used in Windows to instruct Python to find the first case-insensitive match in an import statement. Set this variable to any value to activate it.

PYTHONHOME − It is an alternative module search path. It is usually embedded in the PYTHONSTARTUP or PYTHONPATH directories to make switching module libraries easy.
5. What are the supported data types in Python?

Python has five standard data types −

    Numbers
    String
    List
    Tuple
    Dictionary

6. What is the difference between list and tuples?
LIST 	TUPLES
Lists are mutable i.e they can be edited. 	Tuples are immutable (tuples are lists which can’t be edited).
Lists are slower than tuples. 	Tuples are faster than list.
Syntax: list_1 = [10, ‘Chelsea’, 20] 	Syntax: tup_1 = (10, ‘Chelsea’ , 20)
Become Python Certified in 24 hrs.
GET CERTIFIED
7. How is memory managed in Python?

    Python memory is managed by Python private heap space. All Python objects and data structures are located in a private heap. The programmer does not have an access to this private heap and interpreter takes care of this Python private heap.
    The allocation of Python heap space for Python objects is done by Python memory manager. The core API gives access to some tools for the programmer to code.
    Python also have an inbuilt garbage collector, which recycle all the unused memory and frees the memory and makes it available to the heap space.

8. Explain Inheritance in Python with an example.

Inheritance allows One class to gain all the members(say attributes and methods) of another class. Inheritance provides code reusability, makes it easier to create and maintain an application. The class from which we are inheriting is called super-class and the class that is inherited is called a derived / child class.

They are different types of inheritance supported by Python:

    Single Inheritance – where a derived class acquires the members of a single super class.
    Multi-level inheritance – a derived class d1 in inherited from base class base1, and d2 is inherited from base2.
    Hierarchical inheritance – from one base class you can inherit any number of child classes
    Multiple inheritance – a derived class is inherited from more than one base class.

9. Whenever Python exits, why isn’t all the memory de-allocated?

    Whenever Python exits, especially those Python modules which are having circular references to other objects or the objects that are referenced from the global namespaces are not always de-allocated or freed.
    It is impossible to de-allocate those portions of memory that are reserved by the C library.
    On exit, because of having its own efficient clean up mechanism, Python would try to de-allocate/destroy every other object.

Learn Python from Experts! Enrol Today
10. What is dictionary in Python?

The built-in datatypes in Python is called dictionary. It defines one-to-one relationship between keys and values. Dictionaries contain pair of keys and their corresponding values. Dictionaries are indexed by keys.

Let’s take an example:

The following example contains some keys. Country, Capital & PM. Their corresponding values are India, Delhi and Modi respectively.

dict={‘Country’:’India’,’Capital’:’Delhi’,’PM’:’Modi’}

print dict[Country]
11. Write a one-liner that will count the number of capital letters in a file. Your code should work even if the file is too big to fit in memory.

Let us first write a multiple line solution and then convert it to one liner code.

1 with open(SOME_LARGE_FILE) as fh:

2 count = 0
3 text = fh.read()
4 for character in text:
5 if character.isupper():
6 count += 1

 
12. Write a sorting algorithm for a numerical dataset in Python.

The following code can be used to sort a list in Python:

list = [“1”, “4”, “0”, “6”, “9”]

list = [int(i) for i in list]

list.sort()

print (list)
13. How will you reverse a list?

list.reverse() − Reverses objects of list in place.
14. How will you remove last object from a list?

list.pop(obj=list[-1]) − Removes and returns last object or obj from list.
15. What are negative indexes and why are they used?

The sequences in Python are indexed and it consists of the positive as well as negative numbers. The numbers that are positive uses ‘0’ that is uses as first index and ‘1’ as the second index and the process goes on like that.

The index for the negative number starts from ‘-1’ that represents the last index in the sequence and ‘-2’ as the penultimate index and the sequence carries forward like the positive number.

The negative index is used to remove any new-line spaces from the string and allow the string to except the last character that is given as S[:-1]. The negative index is also used to show the index to represent the string in correct order.
16. Explain split(), sub(), subn() methods of “re” module in Python.

To modify the strings, Python’s “re” module is providing 3 methods. They are:

    split() – uses a regex pattern to “split” a given string into a list.
    sub() – finds all substrings where the regex pattern matches and then replace them with a different string
    subn() – it is similar to sub() and also returns the new string along with the no. of replacements.

17. What is the difference between range & xrange?

For the most part, xrange and range are the exact same in terms of functionality. They both provide a way to generate a list of integers for you to use, however you please. The only difference is that range returns a Python list object and x range returns an xrange object.

This means that xrange doesn’t actually generate a static list at run-time like range does. It creates the values as you need them with a special technique called yielding. This technique is used with a type of object known as generators. That means that if you have a really gigantic range you’d like to generate a list for, say one billion, xrange is the function to use.

This is especially true if you have a really memory sensitive system such as a cell phone that you are working with, as range will use as much memory as it can to create your array of integers, which can result in a Memory Error and crash your program. It’s a memory hungry beast.
18. What is pickling and unpickling?

Pickle module accepts any Python object and converts it into a string representation and dumps it into a file by using dump function, this process is called pickling. While the process of retrieving original Python objects from the stored string representation is called unpickling.
19. What is map function in Python?

map function executes the function given as the first argument on all the elements of the iterable given as the second argument. If the function given takes in more than 1 arguments, then many iterables are given. #Follow the link to know more similar functions
20. How to get indices of N maximum values in a NumPy array?

We can get the indices of N maximum values in a NumPy array using the below code:
import numpy as np

arr = np.array([1, 3, 2, 4, 5])

print(arr.argsort()[-3:][::-1])
21. What is a Python module?

A module is a Python script that generally contains import statements, functions, classes and variable definitions, and Python runnable code and it “lives” file with a ‘.py’ extension. zip files and DLL files can also be modules.Inside the module, you can refer to the module name as a string that is stored in the global variable name .
22. Name the File-related modules in Python?

Python provides libraries / modules with functions that enable you to manipulate text files and binary files on file system. Using them you can create files, update their contents, copy, and delete files. The libraries are : os, os.path, and shutil.

Here, os and os.path – modules include functions for accessing the filesystem

shutil – module enables you to copy and delete the files.
23. Explain the use of with statement?

In python generally “with” statement is used to open a file, process the data present in the file, and also to close the file without calling a close() method. “with” statement makes the exception handling simpler by providing cleanup activities.

General form of with:

with open(“filename”, “mode”) as file-var:

processing statements

note: no need to close the file by calling close() upon file-var.close()
24. Explain all the file processing modes supported by Python?

Python allows you to open files in one of the three modes. They are:

read-only mode, write-only mode, read-write mode, and append mode by specifying the flags “r”, “w”, “rw”, “a” respectively.

A text file can be opened in any one of the above said modes by specifying the option “t” along with

“r”, “w”, “rw”, and “a”, so that the preceding modes become “rt”, “wt”, “rwt”, and “at”.A binary file can be opened in any one of the above said modes by specifying the option “b” along with “r”, “w”, “rw”, and “a” so that the preceding modes become “rb”, “wb”, “rwb”, “ab”.
25. How many kinds of sequences are supported by Python? What are they?

Python supports 7 sequence types. They are str, list, tuple, unicode, byte array, xrange, and buffer. where xrange is deprecated in python 3.5.X.
26. How do you perform pattern matching in Python? Explain

Regular Expressions/REs/ regexes enable us to specify expressions that can match specific “parts” of a given string. For instance, we can define a regular expression to match a single character or a digit, a telephone number, or an email address, etc.The Python’s “re” module provides regular expression patterns and was introduce from later versions of Python 2.5. “re” module is providing methods for search text strings, or replacing text strings along with methods for splitting text strings based on the pattern defined.
27. How to display the contents of text file in reverse order?

    convert the given file into a list.
    reverse the list by using reversed()
    Eg: for line in reversed(list(open(“file-name”,”r”))):
    print(line)

28. What is the difference between NumPy and SciPy?

    In an ideal world, NumPy would contain nothing but the array data type and the most basic operations: indexing, sorting, reshaping, basic element wise functions, et cetera.
    All numerical code would reside in SciPy. However, one of NumPy’s important goals is compatibility, so NumPy tries to retain all features supported by either of its predecessors.
    Thus NumPy contains some linear algebra functions, even though these more properly belong in SciPy. In any case, SciPy contains more fully-featured versions of the linear algebra modules, as well as many other numerical algorithms.
    If you are doing scientific computing with python, you should probably install both NumPy and SciPy. Most new features belong in SciPy rather than NumPy.

29. Which of the following is an invalid statement?
a) abc = 1,000,000
b) a b c = 1000 2000 3000
c) a,b,c = 1000, 2000, 3000
d) a_b_c = 1,000,000

Answer: b
30. What is the output of the following? try: if '1' != 1: raise
a) some Error has  occured
b) some Error has not occured
c) invalid code
d) none of the above

Answer: C
31. Suppose list1 is [2, 33, 222, 14, 25], What is list1[-1] ?

25
32. To open a file c:\scores.txt for writing?

fileWriter = open(“c:\\scores.txt”, “w”)
33. Name few Python modules for Statistical, Numerical and scientific computations ?

numPy – this module provides an array/matrix type, and it is useful for doing computations on arrays. scipy – this module provides methods for doing numeric integrals, solving differential equations, etc pylab – is a module for generating and saving plots
34. What is TkInter?

TkInter is Python library. It is a toolkit for GUI development. It provides support for various GUI tools or widgets (such as buttons, labels, text boxes, radio buttons, etc) that are used in GUI applications. The common attributes of them include Dimensions, Colors, Fonts, Cursors, etc.
35. Is Python object oriented? what is object oriented programming?

Yes. Python is Object Oriented Programming language. OOP is the programming paradigm based on classes and instances of those classes called objects. The features of OOP are:

Encapsulation, Data Abstraction, Inheritance, Polymorphism.
36. What is multithreading? Give an example.

It means running several different programs at the same time concurrently by invoking multiple threads. Multiple threads within a process refer the data space with main thread and they can communicate with each other to share information more easily.Threads are light-weight processes and have less memory overhead. Threads can be used just for quick task like calculating results and also running other processes in the background while the main program is running.
37. Does Python supports interfaces like in Java? Discuss.

Python does not provide interfaces like in Java. Abstract Base Class (ABC) and its feature are provided by the Python’s “abc” module. Abstract Base Class is a mechanism for specifying what methods must be implemented by its implementation subclasses. The use of ABC’c provides a sort of “understanding” about methods and their expected behaviour. This module was made available from Python 2.7 version onwards.
38. What are Accessors, mutators, @property?

Accessors and mutators are often called getters and setters in languages like “Java”. For example, if x is a property of a user-defined class, then the class would have methods called setX() and getX(). Python has an @property “decorator” that allows you to ad getters and setters in order to access the attribute of the class.
39. Differentiate between append() and extend() methods.?

Both append() and extend() methods are the methods of list. These methods a re used to add the elements at the end of the list.

append(element) – adds the given element at the end of the list which has called this method.

extend(another-list) – adds the elements of another-list at the end of the list which is called the extend method.
40. Name few methods that are used to implement Functionally Oriented Programming in Python?

Python supports methods (called iterators in Python3), such as filter(), map(), and reduce(), that are very useful when you need to iterate over the items in a list, create a dictionary, or extract a subset of a list.

filter() – enables you to extract a subset of values based on conditional logic.

map() – it is a built-in function that applies the function to each item in an iterable.

reduce() – repeatedly performs a pair-wise reduction on a sequence until a single value is computed.
41. What is the output of the following?

x = [‘ab’, ‘cd’]
print(len(map(list, x)))

A TypeError occurs as map has no len().
42. What is the output of the following?

x = [‘ab’, ‘cd’]
print(len(list(map(list, x))))

Explanation: The length of each string is 2.
43. Which of the following is not the correct syntax for creating a set?

    a) set([[1,2],[3,4]])
    b) set([1,2,2,3,4])
    c) set((1,2,3,4))
    d) {1,2,3,4}

Answer : a

Explanation : The argument given for the set must be an iterable.
44. Explain a few methods to implement Functionally Oriented Programming in Python.

Sometimes, when we want to iterate over a list, a few methods come in handy.

    filter()

Filter lets us filter in some values based on conditional logic.

>>> list(filter(lambda x:x>5,range(8)))

[6, 7]

    map()

Map applies a function to every element in an iterable.

>>> list(map(lambda x:x**2,range(8)))

[0, 1, 4, 9, 16, 25, 36, 49]

    reduce()

Reduce repeatedly reduces a sequence pair-wise until we reach a single value

>>> from functools import reduce

>>> reduce(lambda x,y:x-y,[1,2,3,4,5])

-13
45. Explain database connection in Python Flask?

Flask supports database powered application (RDBS). Such system requires creating a          schema, which requires piping the shema.sql file into a sqlite3 command.  So you need to install   sqlite3 command in order to create or initiate the database in Flask.

Flask allows to request database in three ways

    before_request() : They are called before a request and pass no arguments
    after_request() : They are called after a request and pass the response that will be sent to the client
    teardown_request(): They are called in situation when exception is raised, and response are not guaranteed. They are called after the response been constructed. They are not allowed to modify the request, and their values are ignored.

46. Write a Python function that checks whether a passed string is palindrome Or not? Note: A palindrome is a word, phrase, or sequence that reads the same backward as forward, e.g., madam or nurses run.

def isPalindrome(string):
left_pos = 0
right_pos = len(string) – 1

while right_pos >= left_pos:
if not string[left_pos] == string[right_pos]:
return False
left_pos += 1
right_pos -= 1
return True
print(isPalindrome(‘aza’))
47. Write a Python program to calculate the sum of a list of numbers.

def list_sum(num_List):
if len(num_List) == 1:
return num_List[0]
else:
return num_List[0] + list_sum(num_List[1:])

print(list_sum([2, 4, 5, 6, 7]))

Sample Output:

24
48. How to retrieve data from a table in MySQL database through Python code? Explain.

    import MySQLdb module as : import MySQLdb
    establish a connection to the database.
    db = MySQLdb.connect(“host”=”local host”, “database-user”=”user-name”, “password”=”password”, “database-name”=”database”)
    initialize the cursor variable upon the established connection: c1 = db.cursor()
    retrieve the information by defining a required query string. s = “Select * from dept”
    fetch the data using fetch() methods and print it. data = c1.fetch(s)
    close the database connection. db.close()

49. Write a Python program to read a random line from a file.
``
import random
def random_line(fname):
    lines = open(fname).read().splitlines()
    return random.choice(lines)
    print(random_line(‘test.txt’))
``
50. Write a Python program to count the number of lines in a text file.
``
def file_lengthy(fname):
with open(fname) as f:
for i, l in enumerate(f):
pass
return i + 1
print(“Number of lines in the file: “,file_lengthy(“test.txt”))
``

What are list comprehensions ?
When to use list comprehensions and when to avoid list comprehensions ?
Difference between range and xrange ?
What is lambda function ?
What are Map, filter and reduce functions ?
Difference between deep copy and shallow copy ?
What are the different types of exceptions generated in python ?
How to write your own custom exception handling ?
Difference between input and raw_input ?
Why do we write __name__ == "__main__" in a python script ?
Please explain 'with' statement in python
Why does the exception handling have a finally block ?
Does python provide thread safe multi-threading ?
What do you mean by non blocking IO ?
How to use *args and **kwargs in python ?


Q.1. What are the key features of Python?

If it makes for an introductory language to programming, Python must mean something. These are its qualities:

    Interpreted
    Dynamically-typed
    Object-oriented
    Concise and simple
    Free
    Has a large community

Follow this link to explore more features of Python Programming

Q.2. Differentiate between deep and shallow copy.

A deep copy copies an object into another. This means that if you make a change to a copy of an object, it won’t affect the original object. In Python, we use the function deepcopy() for this, and we import the module copy. We use it like:

    >>> import copy
    >>> b=copy.deepcopy(a)

Deep Copy - Python Interview Questions and Answers

Deep Copy – Python Interview Questions and Answers

A shallow copy, however, copies one object’s reference to another. So, if we make a change in the copy, it will affect the original object. For this, we have the function copy(). We use it like:

    >>> b=copy.copy(a)

Shallow Copy - Python Interview Questions and Answers

Shallow Copy – Python Interview Questions and Answers

Refer this link to know more about Deep & Shallow Copy in Python

Q.3. Differentiate between lists and tuples.

The major difference is that a list is mutable, but a tuple is immutable. Examples:

    >>> mylist=[1,3,3]
    >>> mylist[1]=2
    >>> mytuple=(1,3,3)
    >>> mytuple[1]=2

Traceback (most recent call last):

File “<pyshell#97>”, line 1, in <module>

mytuple[1]=2

TypeError: ‘tuple’ object does not support item assignment

For more insight, refer to Tuples vs Lists.
2. Basic Python Interview Questions for Freshers

Q.4 to Q.20 are some basic Python Interview question for freshers, however Experience can also refer these questions to revise basic concepts.

Q.4. Explain the ternary operator in Python.

Unlike C++, we don’t have ?: in Python, but we have this:

[on true] if [expression] else [on false]

If the expression is True, the statement under [on true] is executed. Else, that under [on false] is executed.

Below is how you would use it:

    >>> a,b=2,3
    >>> min=a if a<b else b
    >>> min

2

    >>> print("Hi") if a<b else print("Bye")

Hi

Are you familiar with all kinds of Python Operators?

Q.5. How is multithreading achieved in Python?

A thread is a lightweight process, and multithreading allows us to execute multiple threads at once. As you know, Python is a multithreaded language. It has a multi-threading package.

The GIL (Global Interpreter Lock) ensures that a single thread executes at a time. A thread holds the GIL and does a little work before passing it on to the next thread. This makes for an illusion of parallel execution. But in reality, it is just threaded taking turns at the CPU. Of course, all the passing around adds overhead to the execution.

Q.6. Explain inheritance in Python.

When one class inherits from another, it is said to be the child/derived/sub class inheriting from the parent/base/super class. It inherits/gains all members (attributes and methods).
Python Interview Questions - inheritance in Python.

Python Interview Questions – Inheritance in Python

Inheritance lets us reuse our code, and also makes it easier to create and maintain applications. Python supports the following kinds of inheritance:

    Single Inheritance- A class inherits from a single base class.
    Multiple Inheritance- A class inherits from multiple base classes.
    Multilevel Inheritance- A class inherits from a base class, which, in turn, inherits from another base class.
    Hierarchical Inheritance- Multiple classes inherit from a single base class.
    Hybrid Inheritance- Hybrid inheritance is a combination of two or more types of inheritance.

For more on inheritance, refer to Python Inheritance.

Q.7. What is Flask?

Python Flask, as we’ve previously discussed, is a web microframework for Python. It is based on the ‘Werkzeug, Jinja 2 and good intentions’ BSD license. Two of its dependencies are Werkzeug and Jinja2. This means it has around no dependencies on external libraries. Due to this, we can call it a light framework.

A session uses a signed cookie to allow the user to look at and modify session contents. It will remember information from one request to another. However, to modify a session, the user must have the secret key Flask.secret_key.

Q.8. How is memory managed in Python?

Python has a private heap space to hold all objects and data structures. Being programmers, we cannot access it; it is the interpreter that manages it. But with the core API, we can access some tools. The Python memory manager controls the allocation.

Additionally, an inbuilt garbage collector recycles all unused memory so it can make it available to the heap space.

Q.9. Explain help() and dir() functions in Python.

The help() function displays the documentation string and help for its argument.

    >>> import copy
    >>> help(copy.copy)

Help on function copy in module copy:

copy(x)

Shallow copy operation on arbitrary Python objects.

See the module’s __doc__ string for more info.

The dir() function displays all the members of an object(any kind).

    >>> dir(copy.copy)

[‘__annotations__’, ‘__call__’, ‘__class__’, ‘__closure__’, ‘__code__’, ‘__defaults__’, ‘__delattr__’, ‘__dict__’, ‘__dir__’, ‘__doc__’, ‘__eq__’, ‘__format__’, ‘__ge__’, ‘__get__’, ‘__getattribute__’, ‘__globals__’, ‘__gt__’, ‘__hash__’, ‘__init__’, ‘__init_subclass__’, ‘__kwdefaults__’, ‘__le__’, ‘__lt__’, ‘__module__’, ‘__name__’, ‘__ne__’, ‘__new__’, ‘__qualname__’, ‘__reduce__’, ‘__reduce_ex__’, ‘__repr__’, ‘__setattr__’, ‘__sizeof__’, ‘__str__’, ‘__subclasshook__’]

Let’s explore more Functions in Python

Q.10. Whenever you exit Python, is all memory de-allocated?

The answer here is no. The modules with circular references to other objects, or to objects referenced from global namespaces, aren’t always freed on exiting Python.

Plus, it is impossible to de-allocate portions of memory reserved by the C library.

Q.11. What is monkey patching?

Dynamically modifying a class or module at run-time.

    >>> class A:
        def func(self):
            print("Hi")
    >>> def monkey(self):
            print "Hi, monkey"
    >>> m.A.func = monkey
    >>> a = m.A()
    >>> a.func()

Hi, monkey

Q.12. What is a dictionary in Python?

A python dictionary is something I have never seen in other languages like C++ or Java programming. It holds key-value pairs.

    >>> roots={25:5,16:4,9:3,4:2,1:1}
    >>> type(roots)

<class ‘dict’>

    >>> roots[9]

3

A dictionary is mutable, and we can also use a comprehension to create it.

    >>> roots={x**2:x for x in range(5,0,-1)}
    >>> roots

{25: 5, 16: 4, 9: 3, 4: 2, 1: 1}

Q.13. What do you mean by *args and **kwargs?

In cases when we don’t know how many arguments will be passed to a function, like when we want to pass a list or a tuple of values, we use *args.

    >>> def func(*args):
        for i in args:
            print(i)  
    >>> func(3,2,1,4,7)

3

2

1

4

7

**kwargs takes keyword arguments when we don’t know how many there will be.

    >>> def func(**kwargs):
        for i in kwargs:
            print(i,kwargs[i])
    >>> func(a=1,b=2,c=7)

a.1

b.2

c.7

The words args and kwargs are a convention, and we can use anything in their place.

Any doubt yet in Basic Python Interview Questions and answers for Freshers? Please ask in Comments.

Q.14. Write Python logic to count the number of capital letters in a file.

    >>> import os
    >>> os.chdir('C:\\Users\\lifei\\Desktop')
    >>> with open('Today.txt') as today:
        count=0
        for i in today.read():
            if i.isupper():
                count+=1
        print(count)

26

Q.15. What are negative indices?

Let’s take a list for this.

    >>> mylist=[0,1,2,3,4,5,6,7,8]

A negative index, unlike a positive one, begins searching from the right.

    >>> mylist[-3]

6

This also helps with slicing from the back:

    >>> mylist[-6:-1]

[3, 4, 5, 6, 7]

Q.16. How would you randomize the contents of a list in-place?

For this, we’ll import the function shuffle() from the module random.

    >>> from random import shuffle
    >>> shuffle(mylist)
    >>> mylist

[3, 4, 8, 0, 5, 7, 6, 2, 1]

Q.17. Explain join() and split() in Python.

join() lets us join characters from a string together by a character we specify.

    >>> ','.join('12345')

‘1,2,3,4,5’

split() lets us split a string around the character we specify.

    >>> '1,2,3,4,5'.split(',')

[‘1’, ‘2’, ‘3’, ‘4’, ‘5’]

Q.18. Is Python case-sensitive?

A language is case-sensitive if it distinguishes between identifiers like myname and Myname. In other words, it cares about case- lowercase or uppercase. Let’s try this with Python.

    >>> myname='Ayushi'
    >>> Myname

Traceback (most recent call last):

File “<pyshell#3>”, line 1, in <module>

Myname

NameError: name ‘Myname’ is not defined

As you can see, this raised a NameError. This means that Python is indeed case-sensitive.

Let’s Discuss Errors and Exceptions in Python Programming

Q.19. How long can an identifier be in Python?

In Python, an identifier can be of any length. Apart from that, there are certain rules we must follow to name one:

    It can only begin with an underscore or a character from A-Z or a-z.
    The rest of it can contain anything from the following: A-Z/a-z/_/0-9.
    Python is case-sensitive, as we discussed in the previous question.
    Keywords cannot be used as identifiers. Python has the following keywords:

and	def	False	import	not	True
as	del	finally	in	or	try
assert	elif	for	is	pass	while
break	else	from	lambda	print	with
class	except	global	None	raise	yield
continue	exec	if	nonlocal	return	

Q.20. How do you remove the leading whitespace in a string?

Leading whitespace in a string is the whitespace in a string before the first non-whitespace character. To remove it from a string, we use the method lstrip().

    >>> '   Ayushi '.lstrip()

‘Ayushi   ‘

As you can see, this string had both leading and trailing whitespaces. lstrip() stripped the string of the leading whitespace. If we want to strip the trailing whitespace instead, we use rstrip().

    >>> '   Ayushi '.rstrip()

‘   Ayushi’

These were basic Python Interview Questions and answers for Freshers.
3. Advanced Python Interview Questions and Answers for Experienced

Q. 21 to Q. 35 are some Advanced Python Interview questions for Experience along with their answers and Examples.

Q.21. How would you convert a string into lowercase?

We use the lower() method for this.

    >>> 'AyuShi'.lower()

‘ayushi’

To convert it into uppercase, then, we use upper().

    >>> 'AyuShi'.upper()

‘AYUSHI’

Also, to check if a string is in all uppercase or all lowercase, we use the methods isupper() and islower().

    >>> 'AyuShi'.isupper()

False

    >>> 'AYUSHI'.isupper()

True

    >>> 'ayushi'.islower()

True

    >>> '@yu$hi'.islower()

True

    >>> '@YU$HI'.isupper()

True

So, characters like @ and $ will suffice for both cases.

Also, istitle() will tell us if a string is in title case.

    >>> 'The Corpse Bride'.istitle()

True

Refer this link to explore more Python Strings with functions

Q.22. What is the pass statement in Python?

There may be times in our code when we haven’t decided what to do yet, but we must type something for it to be syntactically correct. In such a case, we use the pass statement.

    >>> def func(*args):
               pass 
    >>>

Similarly, the break statement breaks out of a loop.

    >>> for i in range(7):
        if i==3: break
        print(i)

0

1

2

Finally, the continue statement skips to the next iteration.

    >>> for i in range(7):
        if i==3: continue
        print(i)

0

1

2

4

5

6

Q.23. What is a closure in Python?

A closure is said to occur when a nested function references a value in its enclosing scope. The whole point here is that it remembers the value.

    >>> def A(x):
        def B():
            print(x)
        return B
    >>> A(7)()

7

For more depth on closures, refer to Closures in Python.

Q.24. Explain the //, %, and ** operators in Python.

The // operator performs floor division. It will return the integer part of the result on division.

    >>> 7//2

3

Normal division would return 3.5 here.

Similarly, ** performs exponentiation. a**b returns the value of a raised to the power b.

    >>> 2**10

1024

Finally, % is for modulus. This gives us the value left after the highest achievable division.

    >>> 13%7

6

    >>> 3.5%1.5

0.5

Any Doubt yet in Advanced Python Interview Questions and Answers for Experienced? Please Comment.

Q.24. How many kinds of operators do we have in Python? Explain arithmetic operators.

This type of Python Interview Questions and Answers can decide your knowledge in Python. Answer the Python Interview Questions with some good Examples.

Here in Python, we have 7 kinds of operators: arithmetic, relational, assignment, logical, membership, identity, and bitwise.

We have seven arithmetic operators. These allow us to perform arithmetic operations on values:

    Addition (+) This adds two values.

    >>> 7+8

15

    Subtraction (-) This subtracts he second value from the first.

    >>> 7-8

-1

    Multiplication (*) This multiplies two numbers.

    >>> 7*8

56

    Division (/) This divides the first value by the second.

    >>> 7/8

0.875

    >>> 1/1

1.0

For floor division, modulus, and exponentiation refer to the previous question.

Q.25. Explain relational operators in Python.

Relational operators compare values.

    Less than (<) If the value on the left is lesser, it returns True.

    >>> 'hi'<'Hi'

False

    Greater than (>) If the value on the left is greater, it returns True.

    >>> 1.1+2.2>3.3

True

This is because of the flawed floating-point arithmetic in Python, due to hardware dependencies.

    Less than or equal to (<=) If the value on the left is lesser than or equal to, it returns True.

    >>> 3.0<=3

True

    Greater than or equal to (>=) If the value on the left is greater than or equal to, it returns True.

    >>> True>=False

True

    Equal to (==) If the two values are equal, it returns True.

    >>> {1,3,2,2}=={1,2,3}

True

    Not equal to (!=) If the two values are unequal, it returns True.

    >>> True!=0.1

True

    >>> False!=0.1

True

Q.26. What are assignment operators in Python?

This one is an Important Interview question in Python Interview.

We can combine all arithmetic operators with the assignment symbol.

    >>> a=7
    >>> a+=1
    >>> a

8

    >>> a-=1
    >>> a

7

    >>> a*=2
    >>> a

14

    >>> a/=2
    >>> a

7.0

    >>> a**=2
    >>> a

49.0

    >>> a//=3
    >>> a

16.0

    >>> a%=4
    >>> a

0.0

Q.27. Explain logical operators in Python.

We have three logical operators- and, or, not.

    >>> False and True

False

    >>> 7<7 or True

True

    >>> not 2==2

False

Q.28. What are membership, operators?

With the operators ‘in’ and ‘not in’, we can confirm if a value is a member in another.

    >>> 'me' in 'disappointment'

True

    >>> 'us' not in 'disappointment'

True

Q.29. Explain identity operators in Python.

This is one of the very commonly asked Python Interview Questions and answers it with examples.

The operators ‘is’ and ‘is not’ tell us if two values have the same identity.

    >>> 10 is '10'

False

    >>> True is not False

True

Q.30. Finally, tell us about bitwise operators in Python.

These operate on values bit by bit.

    AND (&) This performs & on each bit pair.

    >>> 0b110 & 0b010

2

    OR (|) This performs | on each bit pair.

    >>> 3|2

3

    XOR (^) This performs an exclusive-OR operation on each bit pair.

    >>> 3^2

1

    Binary One’s Complement (~) This returns the one’s complement of a value.

    >>> ~2

-3

    Binary Left-Shift (<<) This shifts the bits to the left by the specified amount.

    >>> 1<<2

4

Here, 001 was shifted to the left by two places to get 100, which is binary for 4.

    Binary Right-Shift (>>)

    >>> 4>>2

1

For more insight on operators, refer to Operators in Python.

Q.31. How would you work with numbers other than those in the decimal number system?

With Python, it is possible to type numbers in binary, octal, and hexadecimal.

    Binary numbers are made of 0 and 1. To type in binary, we use the prefix 0b or 0B.

    >>> int(0b1010)

10

To convert a number into its binary form, we use bin().

    >>> bin(0xf)

‘0b1111’

    Octal numbers may have digits from 0 to 7. We use the prefix 0o or 0O.

    >>> oct(8)

‘0o10’

    Hexadecimal numbers may have digits from 0 to 15. We use the prefix 0x or 0X.

    >>> hex(16)

‘0x10’

    >>> hex(15)

‘0xf’

Q.32. How do you get a list of all the keys in a dictionary?

Be specific in these type of Python Interview Questions and Answers.

For this, we use the function keys().

    >>> mydict={'a':1,'b':2,'c':3,'e':5}
    >>> mydict.keys()

dict_keys([‘a’, ‘b’, ‘c’, ‘e’])

Q.33. Why are identifier names with a leading underscore disparaged?

Since Python does not have a concept of private variables, it is a convention to use leading underscores to declare a variable private. This is why we mustn’t do that to variables we do not want to make private.

Q.34. How can you declare multiple assignments in one statement?

There are two ways to do this:

    >>> a,b,c=3,4,5 #This assigns 3, 4, and 5 to a, b, and c respectively
    >>> a=b=c=3 #This assigns 3 to a, b, and c

Q.35. What is tuple unpacking?

First, let’s discuss tuple packing. It is a way to pack a set of values into a tuple.

    >>> mytuple=3,4,5
    >>> mytuple

(3, 4, 5)

This packs 3, 4, and 5 into mytuple.

Now, we will unpack the values from the tuple into variables x, y, and z.

    >>> x,y,z=mytuple
    >>> x+y+z

Q.1. What data types does Python support?

This is the most basic python interview question.

Python provides us with five kinds of data types:

    Numbers- Numbers use to hold numerical values.

    >>> a=7.0
    >>>

    Strings- A string is a sequence of characters.  We declare it using single or double quotes.

    >>> title="Ayushi's Book"

    Lists- A list is an ordered collection of values, and we declare it using square brackets.

    >>> colors=['red','green','blue']
    >>> type(colors)

<class ‘list’>

    Tuples- A tuple, like a list, is an ordered collection of values. The difference. However, is that a tuple is immutable. This means that we cannot change a value in it.

Python Interview Questions and Answers

Python Interview Questions and Answers – Python Data Types

    >>> name=('Ayushi','Sharma')
    >>> name[0]='Avery'

Traceback (most recent call last):

File “<pyshell#129>”, line 1, in <module>

name[0]=’Avery’

TypeError: ‘tuple’ object does not support item assignment

    Dictionary- A dictionary is a data structure that holds key-value pairs. We declare it using curly braces.

    >>> squares={1:1,2:4,3:9,4:16,5:25}
    >>> type(squares)

<class ‘dict’>

    >>> type({})

<class ‘dict’>

We can also use a dictionary comprehension:

    >>> squares={x:x**2 for x in range(1,6)}
    >>> squares

{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

Follow this link to know more about Python Data Structure

Q.2. What is a docstring?

A docstring is a documentation string that we use to explain what a construct does. We place it as the first thing under a function, class, or a method, to describe what it does. We declare a docstring using three sets of single or double quotes.

    >>> def sayhi():
        """
        The function prints Hi
        """
        print("Hi")
    >>> sayhi()

 

Hi

To get a function’s docstring, we use its __doc__ attribute.

    >>> sayhi.__doc__

‘\n\tThis function prints Hi\n\t’

A docstring, unlike a comment, is retained at runtime.

Q.3. What is the PYTHONPATH variable?

PYTHONPATH is the variable that tells the interpreter where to locate the module files imported into a program. Hence, it must include the Python source library directory and the directories containing Python source code. You can manually set PYTHONPATH, but usually, the Python installer will preset it.
2. Basic Python Interview Questions

Q.4. What is slicing?

These are the types of basic Python interview questions for freshers.

Slicing is a technique that allows us to retrieve only a part of a list, tuple, or string. For this, we use the slicing operator [].

    >>> (1,2,3,4,5)[2:4]

(3, 4)

    >>> [7,6,8,5,9][2:]

[8, 5, 9]

    >>> 'Hello'[:-1]

‘Hell’

Q.5. What is a namedtuple?

A namedtuple will let us access a tuple’s elements using a name/label. We use the function namedtuple() for this, and import it from collections.

    >>> from collections import namedtuple
    >>> result=namedtuple('result','Physics Chemistry Maths') #format
    >>> Ayushi=result(Physics=86,Chemistry=95,Maths=86) #declaring the tuple
    >>> Ayushi.Chemistry

95

As you can see, it let us access the marks in Chemistry using the Chemistry attribute of object Ayushi.

To learn more about namedtuples, refer to namedtuple in Python.

Q.6. How would you declare a comment in Python?

Unlike languages like C++, Python does not have multiline comments. All it has is octothorpe (#). Anything following a hash is considered a comment, and the interpreter ignores it.

    >>> #line 1 of comment
    >>> #line 2 of comment

In fact, you can place a comment anywhere in your code. You can use it to explain your code.

Q.7. How would you convert a string into an int in Python?

If a string contains only numerical characters, you can convert it into an integer using the int() function.

    >>> int('227')

227

Let’s check the types:

    >>> type('227')

<class ‘str’>

    >>> type(int('227'))

 <class ‘int’>

Q.8. How do you take input in Python?

For taking input from user, we have the function input(). In Python 2, we had another function raw_input().

The input() function takes, as an argument, the text to be displayed for the task:

    >>> a=input('Enter a number')

Enter a number7

But if you have paid attention, you know that it takes input in the form of a string.

    >>> type(a)

<class ‘str’>

Multiplying this by 2 gives us this:

    >>> a*=2
    >>> a

’77’

So, what if we need to work on an integer instead?

We use the int() function for this.

    >>> a=int(input('Enter a number'))

Enter a number7

Now when we multiply it by 2, we get this:

    >>> a*=2
    >>> a

14

Q.9. What is a frozen set in Python?

Answer these type of Python Interview Questions with Examples.

First, let’s discuss what a set is. A set is a collection of items, where there cannot be any duplicates. A set is also unordered.

    >>> myset={1,3,2,2}
    >>> myset

{1, 2, 3}

This means that we cannot index it.

    >>> myset[0]

Traceback (most recent call last):

File “<pyshell#197>”, line 1, in <module>

myset[0]

TypeError: ‘set’ object does not support indexing

However, a set is mutable. A frozen set is immutable. This means we cannot change its values. This also makes it eligible to be used as a key for a dictionary.

    >>> myset=frozenset([1,3,2,2])
    >>> myset

frozenset({1, 2, 3})

    >>> type(myset)

<class ‘frozenset’>

For more insight on sets, refer to Python Sets and Booleans.

Q.10. How would you generate a random number in Python?

This kind of Python interview Questions and Answers can Prove your depth of knowledge.

To generate a random number, we import the function random() from the module random.

    >>> from random import random
    >>> random()

0.7931961644126482

Let’s call for help on this.

    >>> help(random)

Help on built-in function random:

random(…) method of random.Random instance

random() -> x in the interval [0, 1).

This means that it will return a random number equal to or greater than 0, and less than 1.

We can also use the function randint(). It takes two arguments to indicate a range from which to return a random integer.

    >>> from random import randint
    >>> randint(2,7)

6

    >>> randint(2,7)

5

    >>> randint(2,7)

7

    >>> randint(2,7)

6

    >>> randint(2,7)

2

Q.11. How will you capitalize the first letter of a string?

Simply using the method capitalize().

    >>> 'ayushi'.capitalize()

‘Ayushi’

    >>> type(str.capitalize)

<class ‘method_descriptor’>

However, it will let other characters be.

    >>> '@yushi'.capitalize()

‘@yushi’

Q.12. How will you check if all characters in a string are alphanumeric?

For this, we use the method isalnum().

    >>> 'Ayushi123'.isalnum()

True

    >>> 'Ayushi123!'.isalnum()

False

Other methods that we have include:

    >>> '123.3'.isdigit()

False

    >>> '123'.isnumeric()

True

    >>> 'ayushi'.islower()

True

    >>> 'Ayushi'.isupper()

False

    >>> 'Ayushi'.istitle()

True

    >>> '   '.isspace()

True

    >>> '123F'.isdecimal()

False

Q.13. What is the concatenation?

This is very basic Python Interview Question, try not to make any mistake in this.

Concatenation is joining two sequences. We use the + operator for this.

    >>> '32'+'32'

‘3232’

    >>> [1,2,3]+[4,5,6]

[1, 2, 3, 4, 5, 6]

    >>> (2,3)+(4)

Traceback (most recent call last):

File “<pyshell#256>”, line 1, in <module>

(2,3)+(4)

TypeError: can only concatenate tuple (not “int”) to tuple

Here, 4 is considered an int. Let’s do this again.

    >>> (2,3)+(4,)

(2, 3, 4)

Any query yet in basic Python interview questions and answers for freshers? Please Comment.

Q.14. What is a function?

When we want to execute a sequence of statements, we can give it a name. Let’s define a function to take two numbers and return the greater number.

    >>> def greater(a,b):
           return a is a>b else b
    >>> greater(3,3.5)

 

3.5

You can create your own function or use one of Python’s many built-in functions.

Q.15. Explain lambda expressions. When would you use one?

When we want a function with a single expression, we can define it anonymously. A lambda expression may take input and returns a value. To define the above function as a lambda expression, we type the following code in the interpreter:

    >>> (lambda a,b:a if a>b else b)(3,3.5)

3.5

Here, a and b are the inputs. a if a>b else b is the expression to return. The arguments are 3 and 3.5.

It is possible to not have any inputs here.

    >>> (lambda :print("Hi"))()

Hi

For more insight into lambdas, refer to Lambda Expressions in Python.

Q.16. What is recursion?

When a function makes a call to itself, it is termed recursion. But then, in order for it to avoid forming an infinite loop, we must have a base condition. Let’s take an example.

    >>> def facto(n):
        if n==1: return 1
        return n*facto(n-1)
    >>> facto(4)

24

For more on recursion, visit Recursion in Python.

Q.17. What is a generator?

Python generator produces a sequence of values to iterate on. This way, it is kind of an iterable.

We define a function that ‘yields’ values one by one, and then use a for loop to iterate on it.

    >>> def squares(n):
        i=1
        while(i<=n):
            yield i**2
            i+=1
    >>> for i in squares(7):
        print(i)

1

4

9

16

25

36

49

Q.18. So, what is an iterator, then?

An iterator returns one object at a time to iterate on. To create an iterator, we use the iter() function.

odds=iter([1,3,5,7,9])

Then, we call the next() function on it every time we want an object.

    >>> next(odds)

1

    >>> next(odds)

3

    >>> next(odds)

5

    >>> next(odds)

7

    >>> next(odds)

9

And now, when we call it again, it raises a StopIteration exception. This is because it has reached the end of the values to iterate on.

    >>> next(odds)

Traceback (most recent call last):

File “<pyshell#295>”, line 1, in <module>

next(odds)

StopIteration

For more on iterators, refer to Python iterators.

Q.19. Okay, we asked you about generators and iterators, and you gave us the right answers. But don’t they sound similar?

They do, but there are subtle differences:

    For a generator, we create a function. For an iterator, we use in-built functions iter() and next().
    For a generator, we use the keyword ‘yield’ to yield/return an object at a time.
    A generator may have as many ‘yield’ statements as you want.
    A generator will save the states of the local variables every time ‘yield’ will pause the loop. An iterator does not use local variables; it only needs an iterable to iterate on.
    Using a class, you can implement your own iterator, but not a generator.
    Generators are fast, compact, and simpler.
    Iterators are more memory-efficient.

Read Generators vs Iterators in Python.

Q.20. We know Python is all the rage these days. But to be truly accepting of a great technology, you must know its pitfalls as well. Would you like to talk about this?

Of course. To be truly yourself, you must be accepting of your flaws. Only then can you move forward to work on them. Python has its flaws too:

    Python’s interpreted nature imposes a speed penalty on it.
    While Python is great for a lot of things, it is weak in mobile computing, and in browsers.
    Being dynamically-typed, Python uses duck-typing (If it looks like a duck, it must be a duck). This can raise runtime errors.
    Python has underdeveloped database access layers. This renders it a less-than-perfect choice for huge database applications.
    And then, well, of course. Being easy makes it addictive. Once a Python-coder, always a Python coder.

So while it has problems, it is also a wonderful tool for a lot of things. Refer to Python Advantages and Disadvantages.
3. Python Interview Questions for Experienced

These are the Advanced Python Interview Questions and Answers for Experienced, however they can also refer the basic Python Interview Questions and Answers for Freshers for basic knowledge.

Q.21. What does the function zip() do?

One of the less common functions with beginners, zip() returns an iterator of tuples.

    >>> list(zip(['a','b','c'],[1,2,3]))

[(‘a’, 1), (‘b’, 2), (‘c’, 3)]

Here, it pairs items from the two lists, and creates tuples with those. But it doesn’t have to be lists.

    >>> list(zip(('a','b','c'),(1,2,3)))

[(‘a’, 1), (‘b’, 2), (‘c’, 3)]

Q.22. If you are ever stuck in an infinite loop, how will you break out of it?

For this, we press Ctrl+C. This interrupts the execution. Let’s create an infinite loop to demonstrate this.

    >>> def counterfunc(n):
        while(n==7):print(n)
    >>> counterfunc(7)

7

7

7

7

7

7

7

7

7

7

7

7

7

7

7

7

7

Traceback (most recent call last):

File “<pyshell#332>”, line 1, in <module>

counterfunc(7)

File “<pyshell#331>”, line 2, in counterfunc

while(n==7):print(n)

KeyboardInterrupt

    >>>

Any doubt yet in Python Advanced interview Questions? Please comment.

Q.23. Explain Python’s parameter-passing mechanism.

To pass its parameters to a function, Python uses pass-by-reference. If you change a parameter within a function, the change reflects in the calling function. This is its default behavior. However, when we pass literal arguments like strings, numbers, or tuples, they pass by value. This is because they are immutable.

Q.24. With Python, how do you find out which directory you are currently in?

To find this, we use the function/method getcwd(). We import it from the module os.

    >>> import os
    >>> os.getcwd()

‘C:\\Users\\lifei\\AppData\\Local\\Programs\\Python\\Python36-32’

    >>> type(os.getcwd)

<class ‘builtin_function_or_method’>

We can also change the current working directory with chdir().

    >>> os.chdir('C:\\Users\\lifei\\Desktop')
    >>> os.getcwd()

‘C:\\Users\\lifei\\Desktop’

For more on this, read up on Python Directory.

Q.25. How will you find, in a string, the first word that rhymes with ‘cake’?

For our purpose, we will use the function search(), and then use group() to get the output.

    >>> import re
    >>> rhyme=re.search('.ake','I would make a cake, but I hate to bake')
    >>> rhyme.group()

‘make’

And as we know, the function search() stops at the first match. Hence, we have our first rhyme to ‘cake’.

Q.26. How would you display a file’s contents in reversed order?

Let’s first get to the Desktop. We use the chdir() function/method form the os module for this.

    >>> import os
    >>> os.chdir('C:\\Users\\lifei\\Desktop')

The file we’ll use for this is Today.txt, and it has the following contents:

OS, DBMS, DS, ADA

HTML, CSS, jQuery, JavaScript

Python, C++, Java

This sem’s subjects

Debugger

itertools

container

Let’s read the contents into a list, and then call reversed() on it:

    >>> for line in reversed(list(open('Today.txt'))):
       print(line.rstrip())

container

itertools

Debugger

This sem’s subjects

Python, C++, Java

HTML, CSS, jQuery, JavaScript

OS, DBMS, DS, ADA

Without the rstrip(), we would get blank lines between the output.

Q.27. What is Tkinter?

Tkinter is a famous Python library with which you can craft a GUI. It provides support for different GUI tools and widgets like buttons, labels, text boxes, radio buttons, and more. These tools and widgets have attributes like dimensions, colors, fonts, colors, and more.

You can also import the tkinter module.

    >>> import tkinter
    >>> top=tkinter.Tk()

This will create a new window for you:

This creates a window with the title ‘My Game’. You can position your widgets on this.

Follow this link to know more about Python Libraries

Q.28. How is a .pyc file different from a .py file?

While both files hold bytecode, .pyc is the compiled version of a Python file. It has platform-independent bytecode. Hence, we can execute it on any platform that supports the .pyc format. Python automatically generates it to improve performance(in terms of load time, not speed).

Q.29. How do you create your own package in Python?

We know that a package may contain sub-packages and modules. A module is nothing but Python code.

To create a package of our own, we create a directory and create a file __init__.py in it. We leave it empty. Then, in that package, we create a module(s) with whatever code we want. For a detailed explanation with pictures, refer to Python Packages.

Q.30. How do you calculate the length of a string?

This is simple. We call the function len() on the string we want to calculate the length of.

    >>> len('Adi Shakara')



Q.1. What does the following code output?

    >>> def extendList(val, list=[]):
          list.append(val)
          return list
    >>> list1 = extendList(10)
    >>> list2 = extendList(123,[])
    >>> list3 = extendList('a')
    >>> list1,list2,list3

Ans. ([10, ‘a’], [123], [10, ‘a’])

You’d expect the output to be something like this:

([10],[123],[‘a’])

Well, this is because the list argument does not initialize to its default value ([]) every time we make a call to the function. Once we define the function, it creates a new list. Then, whenever we call it again without a list argument, it uses the same list. This is because it calculates the expressions in the default arguments when we define the function, not when we call it.

Let’s revise the Basis of Python Programming

Q.2. What is a decorator?

Ans. A decorator is a function that adds functionality to another function without modifying it. It wraps another function to add functionality to it. Take an example.

    >>> def decor(func):
        def wrap():
            print("$$$$$$$$$$$$$$$$$")
            func()
            print("$$$$$$$$$$$$$$$$$")

return wrap

    >>> @decor
    def sayhi():
        print("Hi")

    >>> sayhi()

$$$$$$$$$$$$$$$$$

Hi

$$$$$$$$$$$$$$$$$

Decorators are an example of metaprogramming, where one part of the code tries to change another. For more on decorators, read Python Decorators.
2. Basic Python Programming Interview Questions

Below are some Basic Python Programming Interview Questions and answers for freshers.

Q.3. Write a regular expression that will accept an email id. Use the re module.

Ans.

    >>> import re
    >>> e=re.search(r'[0-9a-zA-Z.]+@[a-zA-Z]+\.(com|co\.in)$','ayushiwashere@gmail.com')
    >>> e.group()

‘ayushiwashere@gmail.com’

To brush up on regular expressions, check Regular Expressions in Python.

Q.4. How many arguments can the range() function take?

Ans. The range() function in Python can take up to 3 arguments. Let’s see this one by one.

a. One argument

When we pass only one argument, it takes it as the stop value. Here, the start value is 0, and the step value is +1.

    >>> list(range(5))

[0, 1, 2, 3, 4]

    >>> list(range(-5))

[]

    >>> list(range(0))

[]

b. Two arguments

When we pass two arguments, the first one is the start value, and the second is the stop value.

    >>> list(range(2,7))

[2, 3, 4, 5, 6]

    >>> list(range(7,2))

[]

    >>> list(range(-3,4))

[-3, -2, -1, 0, 1, 2, 3]

c. Three arguments

Here, the first argument is the start value, the second is the stop value, and the third is the step value.

    >>> list(range(2,9,2))

[2, 4, 6, 8]

    >>> list(range(9,2,-1))

[9, 8, 7, 6, 5, 4, 3]

Q.5. Does Python have a switch-case statement?

Ans.  In languages like C++, we have something like this:

    switch(name)
    {
        case ‘Ayushi’:
            cout<<”Monday”;
            break;
        case ‘Megha’:
            cout<<”Tuesday”;
            break;
        default:
            cout<<”Hi, user”;
    }

But in Python, we do not have a switch-case statement. Here, you may write a switch function to use. Else, you may use a set of if-elif-else statements. To implement a function for this, we may use a dictionary.

    >>> def switch(choice):
        switcher={
            'Ayushi':'Monday',
            'Megha':'Tuesday',
           print(switcher.get(choice,'Hi, user'))

return

    >>> switch('Megha')

Tuesday

    >>> switch('Ayushi')

Monday

    >>> switch('Ruchi')

Hi, user

Here, the get() method returns the value of the key. When no key matches, the default value (the second argument) is returned.

Any doubt yet in Python Programming interview Questions. Please Comment.

Q.6. How do you debug a program in Python? Answer in brief.

Ans.  To debug a Python program, we use the 
module. This is the Python debugger; we will discuss it in a tutorial soon. If we start a program using pdb, it will let us step through the code.

Q.7. List some pdb commands.

Some pdb commands include-

<b> — Add breakpoint

<c> — Resume execution

< s > — Debug step by step

<n> — Move to next line

<l> — List source code

<p> — Print an expression

Q.8. What command do we use to debug a Python program?

Ans.  To start debugging, we first open the command prompt, and get to the location the file is at.

Microsoft Windows [Version 10.0.16299.248]

(c) 2017 Microsoft Corporation. All rights reserved.

 

C:\Users\lifei> cd Desktop

C:\Users\lifei\Desktop>

Then, we run the following command (for file try.py):

C:\Users\lifei\Desktop>python -m pdb try.py

> c:\users\lifei\desktop\try.py(1)<module>()

-> for i in range(5):

(Pdb)

Then, we can start debugging.

Q.9. What is a Counter in Python?

Ans.  The function Counter() from the module ‘collections’. It counts the number of occurrences of the elements of a container.

    >>> from collections import Counter
    >>> Counter([1,3,2,1,4,2,1,3,1])

Counter({1: 4, 3: 2, 2: 2, 4: 1})

Python provides us with a range of ways and methods to work with a Counter. Read Python Counter.

Q.10. What is NumPy? Is it better than a list?
Python Programming Interview Questions - Numpy vs List

Python Programming Interview Questions – Numpy vs List

Ans.  NumPy, a Python package, has made its place in the world of scientific computing. It can deal with large data sizes, and also has a powerful N-dimensional array object along with a set of advanced functions.

Yes, a NumPy array is better than a Python list. This is in the following ways:

    It is more compact.
    It is more convenient.
    It Is more efficiently.
    It is easier to read and write items with NumPy.

Read our latest tutorial on Python NumPy

Q.11. How would you create an empty NumPy array?

Ans.  To create an empty array with NumPy, we have two options:

a. Option 1

    >>> import numpy
    >>> numpy.array([])

array([], dtype=float64)

b. Option 2

    >>> numpy.empty(shape=(0,0))

array([], shape=(0, 0), dtype=float64)

Refer Python Libraries

Q.12. What is PEP 8?

Ans.  PEP 8 is a coding convention that lets us write more readable code. In other words, it is a set of recommendations.

Q.13. What is pickling and unpickling?

Ans.  To create portable serialized representations of Python objects, we have the module ‘pickle’. It accepts a Python object (remember, everything in Python is an object). It then converts it into a string representation and uses the dump() function to dump it into a file. We call this pickling. In contrast, retrieving objects from this stored string representation is termed ‘unpickling’.

Q.14. What is a namespace in Python?
Python Programimng Interview Questions and Answers - Python NamespacesPython Namespaces

Python Programming Interview Questions and Answers – Python Namespaces

Ans.  A namespace is a collection of names. It maps names to corresponding objects. When different namespaces contain objects with the same names, this avoids any name collisions. Internally, a namespace is implemented as a Python dictionary.

On starting the interpreter, it creates a namespace for as long as we don’t exit. We have local namespaces, global namespaces, and a built-in namespace.

Just Follow this link to know more about Python Namespace

Q.15. How would you perform unit-testing on your Python code?

Ans.  For this purpose, we have the module unittest in Python. It has the following members:

FunctionTestCase

SkipTest

TestCase

TestLoader

TestResult

TestSuite

TextTestResult

TextTestRunner

defaultTestLoader

expectedFailure

findTestCases

getTestCaseNames

installHandler

main

makeSuite

registerResult

removeHandler

removeResult

skip

skipIf

skipUnless

So Q2 to Q15 were some Basic Python Programming Interview Questions and Answers for Freshers. Experienced can also refer these Python Interview Questions for revision.
3. Advanced Python Interview Questions and Answers

Below are some Advanced Python Programming Interview Questions For Experienced. I recommend freshers to also refer these interview questions for advanced knowledge.

Q.16. Explain the use of the ‘nonlocal’ keyword in Python.

Ans.  First, let’s discuss the local and global scope. By example, a variable defined inside a function is local to that function. Another variable defined outside any other scope is global to the function.

Suppose we have nested functions. We can read a variable in an enclosing scope from inside he inner function, but cannot make a change to it. For that, we must declare it nonlocal inside the function. First, let’s see this without the nonlocal keyword.

    >>> def outer():
        a=7
        def inner():
            print(a)
        inner()
    >>> outer()

7 

    >>> def outer():
        a=7
        def inner():
            print(a)
            a+=1
            print(a)
        inner()

    >>> outer()

Traceback (most recent call last):

File “<pyshell#462>”, line 1, in <module>

outer()

File “<pyshell#461>”, line 7, in outer

inner()

File “<pyshell#461>”, line 4, in inner

print(a)

UnboundLocalError: local variable ‘a’ referenced before assignment

So now, let’s try doing this with the ‘nonlocal’ keyword:

    >>> def outer():
        a=7
        def inner():
            nonlocal a
            print(a)
            a+=1
            print(a)

inner()

    >>> outer()

7

8

Q.17. So, then, what is the global keyword?

Ans.  Like we saw in the previous question, the global keyword lets us deal with, inside any scope, the global version of a variable.

The problem:

    >>> a=7
    >>> def func():
        print(a)
        a+=1
        print(a)

The solution:

    >>> a=7
    >>> def func():
        global a
        print(a)
        a+=1
        print(a)
    >>> func()

7

8

Q.18. How would you make a Python script executable on Unix?

Ans. For this to happen, two conditions must be met:

    The script file’s mode must be executable
    The first line must begin with a hash(#). An  example of this will be: #!/usr/local/bin/python

Q.19. What functions or methods will you use to delete a file in Python?

Ans. For this, we may use remove() or unlink().

    >>> import os
    >>> os.chdir('C:\\Users\\lifei\\Desktop')
    >>> os.remove('try.py')
    >>>

When we go and check our Desktop, the file is gone. Let’s go make it again so we can delete it again using unlink().

    >>> os.unlink('try.py')
    >>>

Both functions are the same, but unlink is the traditional Unix name for it.

Q.20. What are accessors, mutators, and @property?

Ans. What we call getters and setters in languages like Java, we term accessors and mutators in Python. In Java, if we have a user-defined class with a property ‘x’, we have methods like getX() and setX(). In Python, we have @property, which is syntactic sugar for property(). This lets us get and set variables without compromising on the conventions. For a detailed explanation on property, refer to Python property.

Any Doubt yet in Advanced Python Interview Questions and Answers for Experienced? Please Comment.

Q.21. Explain a few methods to implement Functionally Oriented Programming in Python.

Ans. Sometimes, when we want to iterate over a list, a few methods come in handy.
Python Interview Questions - Python Methods

Python Interview Questions – Python Methods

a. filter()

Filter lets us filter in some values based on conditional logic.

    >>> list(filter(lambda x:x>5,range(8)))

[6, 7]

b. map()

Map applies a function to every element in an iterable.

    >>> list(map(lambda x:x**2,range(8)))

[0, 1, 4, 9, 16, 25, 36, 49]

c. reduce()

Reduce repeatedly reduces a sequence pair-wise until we reach a single value.

    >>> from functools import reduce
    >>> reduce(lambda x,y:x-y,[1,2,3,4,5])

-13

Q.22. Differentiate between the append() and extend() methods of a list.

Ans. The methods append() and extend() work on lists. While append() adds an element to the end of the list, extend adds another list to the end of a list.

Let’s take two lists.

    >>> list1,list2=[1,2,3],[5,6,7,8]

This is how append() works:

    >>> list1.append(4)
    >>> list1

[1, 2, 3, 4]

And this is how extend() works:

    >>> list1.extend(list2)
    >>> list1

[1, 2, 3, 4, 5, 6, 7, 8]

Refer Python Lists

Q.23. Consider multiple inheritances here. Suppose class C inherits from classes A and B as class C(A,B). Classes A and B both have their own versions of method func(). If we call func() from an object of class C, which version gets invoked?

Ans. In our article on Multiple Inheritance in Python, we discussed Method Resolution Order (MRO). C does not contain its own version of func(). Since the interpreter searches in a left-to-right fashion, it finds the method in A, and does not go to look for it in B.

Q.24. Which methods/functions do we use to determine the type of instance and inheritance?

Ans. Here, we talk about three methods/functions- type(), isinstance(), and issubclass().
Python Interview Questions - Python Methods

Python Interview Questions – Python Methods/Functions

a. type()

This tells us the type of object we’re working with.

    >>> type(3)

<class ‘int’>

    >>> type(False)

<class ‘bool’>

    >>> type(lambda :print("Hi"))

<class ‘function’>

    >>> type(type)

<class ‘type’>

b. isinstance()

This takes in two arguments- a value and a type. If the value is of the kind of the specified type, it returns True. Else, it returns False.

    >>> isinstance(3,int)

True

    >>> isinstance((1),tuple)

False

    >>> isinstance((1,),tuple)

True

c. issubclass()

This takes two classes as arguments. If the first one inherits from the second, it returns True. Else, it returns False.

    >>> class A: pass
    >>> class B(A): pass
    >>> issubclass(B,A)

True

    >>> issubclass(A,B)

False

Q.25. What do you mean by overriding methods?

Ans. Suppose class B inherits from class A. Both have the method sayhello()- to each, their own version. B overrides the sayhello() of class A. So, when we create an object of class B, it calls the version that class B has.

    >>> class A:
        def sayhello(self):
            print("Hello, I'm A")
    >>> class B(A):
       def sayhello(self):
           print("Hello, I'm B")
    >>> a=A()
    >>> b=B()
    >>> a.sayhello()

Hello, I’m A

    >>> b.sayhello()

Hello, I’m B

Refer this link to know more about Method Overriding in Python

Q.26. What is JSON? Describe in brief how you’d convert JSON data into Python data?

Ans. JSON stands for JavaScript Object Notation. It is a highly popular data format, and it stores data into NoSQL databases. JSON is generally built on the following two structures:

    A collection of <name,value> pairs
    An ordered list of values.

Python supports JSON parsers. In fact, JSON-based data is internally represented as a dictionary in Python. To convert JSON data into Python data, we use the load() function from the JSON module.

 How can you implement functional programming and why would you?
- Explain ctypes and why you would use them?
- What is multiple inheritence and when should you use it?
- What is a meta class?
- What are properties and what's the point?
- What are decorators, how do I define my own?
- Why/When would I use a lambda function?
- What's the difference between 2.7+ and 3?
- What is a unicode string?
- What does the yield statement do?
- What is a generator?
- Why would I use one?
- What is polymorphism, when would I use it?
- How do you go about packaging python code?
- Is Python compiled?, If yes how so, if not how so.
- What does  __some-variable__  mean?
- Should I import an entire module?
- What does dynamicly/duck typed mean?
- When would I not use Python?
- What is DRY, how can I apply it through OOP or FP?
- When would I use Python?

1. What are the differences between Python and Java ?
Python Vs Java
Comparison 	Python 	Java
Performance Speed 	Fast 	Not as much as Python
Indentation 	Must be followed 	Using proper flower braces is enough
Typing 	Dynamically typed 	Static typed
Accessability 	Simple and compact 	Not as much as Python
Platforms 	Not compatible to many 	Platform independent
Database Access 	Weak compared to JAVA 	Strong (JDBC)

Q2. How is Python executed?

Python files are compiled to bytecode. which is then executed by the host.
Alternate Answer:
Type python .pv at the command line.

Q3. What is the difference between .py and .pyc files?

.py files are Python source files. .pyc files are the compiled bvtecode files that is generated by the Python compiler

Q4. How do you invoke the Python interpreter for interactive use?

python or pythonx.y where x.y are the version of the Python interpreter desired.

Q5. How are Phon blocks defined?

By indents or tabs. This is different from most other languages which use symbols to define blocks. Indents in Python are significant.

Q6. What is the Pthon interpreter prompt?

Three greater-than signs: >>> Also, when the int
erpreter is waiting for more input the prompt changes to three periods

Q7. How do you execute a Python Script?

From the command line, type python .py or pythonx.y
.py where the x.y is the version of the Python interpreter desired.
Learn how to use Python, from beginner basics to advanced techniques, with online video tutorials taught by industry experts. Enroll for Free Python Training Demo!

Q8. Explain the use of try: except: raise, and finally:

Try, except and finally blocks are used in Python error handling. Code is executed in the try block until an error occurs. One can use a generic except block, which will receive control after all errors, or one can use specific exception handling blocks for various error types. Control is transferred to the appropriate except block. In all cases, the finally block is executed. Raise may be used to raise your own exceptions.

Q9. Illustrate the proper use of Python error handling.

Code Example:
try:
….#This can be any code
except:
…# error handling code goes here
finally.
…# code that will be executed regardless of exception handling goes here.

Q10. What happens if an error occurs that is not handled in the except block?

The program tenuinates. and an execution trace is sent to sys.stderr.

Q11. How are modules used in a Python program?

Modules are brought in via the import statement.

Q12. How do you create a Python function?

Functions are defined using the def statement. An example might be def foo(bar):

Q13. How is a Python class created?

Classes are created using the class statement. An example might be class aa rdva rk(fooba r):

Q14. How is a Python class instantiated?

The class is instantiated by calling it directly. An example might be
myclass =aardvark(5)

Q15. In a class definition, what does the __ init_O function do?

It overrides the any initialization from an inherited class, and is called when the class is instantiated.

Q16. How does a function return values?

Functions return values using the return statement.

Q17. What happens when a function doesn’t have a return statement? Is this valid?

Yes, this is valid. The function will then return a None object. The end of a function is defined by the block of code being executed (i.e., the indenting) not by any explicit keyword.

Q18. What is the lambda operator?

The lambda operator is used to create anonymous functions. It is mostly used in cases where one wishes to pass functions as parameters. or assign them to variable names.

Q19. Explain the difference between local and global namespaces.

Local namespaces are created within a function. when that function is called. Global name spaces are created when the program starts.

Q20. Name the four main types of namespaces in Python?

    Global, Local, Module and Class namespaces. 

Q21. When would you use triple quotes as a delimiter?

Triple quotes ‘’”” or ‘“ are string delimiters that can span multiple lines in Python. Triple quotes are usually used when spanning multiple lines, or enclosing a string that has a mix of single and double quotes contained therein.

Q22. What are the two major loop statements?

for and while

Q23. Under what circumstances would von use a while statement rather than for?

The while statement is used for simple repetitive looping and the for statement is used when one wishes to iterate through a list of items, such as database records, characters in a string, etc.

Q24. What happens if.ou put an else statement after after block?

The code in the else block is executed after the for loop completes, unless a break is encountered in the for loop execution. in which case the else block is not executed.

Q25. Explain the use of break and continue in Python looping.

The break statement stops execution of the current loop. and transfers control to the next block. The continue statement ends the current block’s execution and jumps to the next iteration of the loop.

Q26. When would you use a continue statement in a for loop?

When processing a particular item was complete; to move on to the next, without executing further processing in the block. The continue statement says, “I’m done processing this item, move on to the next item.”

Q27. When would you use a break statement in a for loop?

When the loop has served its purpose. As an example. after finding the item in a list searched for, there is no need to keep looping. The break statement says, I’m done in this loop; move on to the next block of code.”

Q28. What is the structure of afor loop?

for in : … The ellipsis represents a code block to be executed, once for each item in the sequence. Within the block the item is available as the current item from the entire list.

Q29. What is the structure of a while loop?

while : … The ellipsis represents a code block to be executed. until the condition becomes false. The condition is an expression that is considered true unless it evaluates to o, null or false.

Q30. Use a for loop and illustrate how you would define and print the characters in a string out, one per line.

myString = “I Love Python”
for myChar hi myString:
print myChar

Q31. Given the string “I LoveQPython” use afor loop and illustrate printing each character tip to, but not including the Q.

inyString = “I Love Pijtlzon”
for myCizar in myString:
fmyC’har ==
break
print myChar

Q32. Given the string “I Love Python” print out each character except for the spaces, using a for loop.

inyString = I Love Python”
for myCizar in myString:
fmyChar == ‘’ ‘’:
continue
print myChar

Q33. Illustrate how to execute a ioop ten times.

i=1
while i < 10:

Q34. How to use GUI that comes with Python to test your code?

That is just an editor and a graphical version of the interactive shell. You write or load code and run it, or type it into the shell.
There is no automated testing.

Q35. What is Python good for?

Python is a high-level general-purpose programming language that can be applied to many different classes of problems.
The language comes with a large standard library that covers areas such as string processing like regular expressions, Unicode, calculating differences between files, Internet protocols like HTTP, FTP, SMTP, XML-RPC, POP, IMAP, CGI programming, software engineering like unit testing, logging, profiling, parsing Python code, and operating system interfaces like system calls, file systems, TCP/IP sockets.

Q36. How does the Python version numbering scheme work?

Python versions are numbered A.B.C or A.B.
A is the major version number. It is only incremented for major changes in the language.
B is the minor version number, incremented for less earth-shattering changes.
C is the micro-level. It is incremented for each bug fix release.
Not all releases are bug fix releases. In the run-up to a new major release, ‘A’ series of development releases are made denoted as alpha, beta, or release candidate.
Alphas are early releases in which interfaces aren’t finalized yet; it’s not unexpected to see an interface change between two alpha releases.
Betas are more stable, preserving existing interfaces but possibly adding new modules, and release candidates are frozen, making no changes except as needed to fix critical bugs.
Alpha, beta and release candidate versions have an additional suffix.
The suffix for an alpha version is “aN” for some small number N,
The suffix for a beta version is “bN” for some small number N,
And the suffix for a release candidate version is “cN” for some small number N.
In other words, all versions labeled 2.0aN precede the versions labeled 2.0bN, which precede versions labeled 2.0cN, and those precede 2.0.
You may also find version numbers with a “+” suffix, e.g. “2.2+”. These are unreleased versions, built directly from the subversion trunk. In practice, after a final minor release is made, the subversion trunk is incremented to the next minor version, which becomes the “a0” version, e.g. “2.4a0”.

Q37. Where is math.py (socket.py, regex.py, etc.) source file?

If you can’t find a source file for a module, it may be a built-in or dynamically loaded module implemented in C, C++ or other compiled language. In this case you may not have the source file or it may be something like mathmodule.c, somewhere in a C source directory (not on the Python Path). There are (at least) three kinds of modules in Python:
Modules written in Python (.py);
Modules written in C and dynamically loaded (.dll, .pyd, .so, .sl, etc);
Modules written in C and linked with the interpreter; to get a list of these, type;
Import sys print sys.builtin_module_names;

Q38. How do I make a Python script executable on UNIX?

You need to do two things:
The script file’s mode must be executable and the first line must begin with “#!” followed by the path of the Python interpreter. The first is done by executing chmod +x scriptfile or perhaps chmod 755 ‘script’ file.
The second can be done in a number of ways.
The most straightforward way is to write:
#!/usr/local/bin/python
As the very first line of your file, using the pathname for where the Python interpreter is installed on your platform. If you would like the script to be independent of where the Python interpreter lives, you can use the “env” program. Almost all UNIX variants support the following, assuming the python interpreter is in a directory on the users $PATH:
#! /usr/bin/env python
Don’t do this for CGI scripts. The $PATH variable for CGI scripts is often minimal, so you need to use the actual absolute pathname of the interpreter. Occasionally, a user’s environment is so full that the /usr/bin/env program fails; or there’s no env program at all. In that case, you can try the following hack (due to Alex Rezinsky):
#! /bin/sh
“””:”
exec python $0 ${1+”$@”}
“””
The minor disadvantage is that this defines the script’s __doc__ string. However, you can fix that by adding:
__doc__ = “””…Whatever…”””

Q39. Why don’t my signal handlers work?

The most common problem is that the signal handler is declared with the wrong argument list. It is called as:
handler (signum, frame)
So it should be declared with two arguments:
def handler(signum, frame):

Q40. How do I test a Python program or component?

Python comes with two testing frameworks:
The documentation test modulefinds examples in the documentation strings for a module and runs them, comparing the output with the expected output given in the documentation string.
The unit test moduleis a fancier testing framework modeled on Java and Smalltalk testing frameworks.
For testing, it helps to write the program so that it may be easily tested by using good modular design. Your program should have almost all functionality encapsulated in either functions or class methods. And this sometimes has the surprising and delightful effect of making the program run faster because local variable accesses are faster than global accesses.
Furthermore the program should avoid depending on mutating global variables, since this makes testing much more difficult to do.
The “global main logic” of your program may be as simple as:
if __name__==”__main__”:
main_logic()
at the bottom of the main module of your program.
Once your program is organized as a tractable collection of functions and class behaviors, you should write test functions that exercise the behaviors.
A test suite can be associated with each module which automates a sequence of tests.
You can make coding much more pleasant by writing your test functions in parallel with the “production code”, since this makes it easy to find bugs and even design flaws earlier.
“Support modules” that are not intended to be the main module of a program may include a self-test of the module.
if __name__ == “__main__”:
self_test()
Even programs that interact with complex external interfaces may be tested when the external interfaces are unavailable by using “fake” interfaces implemented in Python.

Q41. How do I find undefined g++ symbols __builtin_new or __pure_virtual?

To dynamically load g++ extension modules, you must:
Recompile Python
Re-link it using g++ (change LINKCC in the python Modules Makefile)
Link your extension module using g++ (e.g., “g++ -shared -o mymodule.so mymodule.o”).

Q42. How do I send mail from a Python script?

Use the standard library module smtplib. Here’s a very simple interactive mail sender that uses it. This method will work on any host that supports an SMTP listener.
import sys, smtplib
fromaddr = raw_input(“From: “)
toaddrs = raw_input(“To: “).split(‘,’)
print “Enter message, end with ^D:”
msg = ”
while 1:
line = sys.stdin.readline()
if not line:
break
msg = msg + line
# The actual mail send
server = smtplib.SMTP(‘localhost’)
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
A UNIX-only alternative uses send mail. The location of the send mail program varies between systems; sometimes it is /usr/lib/sendmail, sometime /usr/sbin/sendmail. The send mail manual page will help you out. Here’s some sample code:
SENDMAIL = “/usr/sbin/sendmail” # sendmail location
import os
p = os.popen(“%s -t -i” % SENDMAIL, “w”)
p.write(“To: receiver@example.comn“)
p.write(“Subject: testn”)
p.write(“n”) # blank line separating headers from body
p.write(“Some textn”)
p.write(“some more textn”)
sts = p.close()
if sts != 0:
print “Sendmail exit status”, sts

Q43. How can I mimic CGI form submission (METHOD=POST)? I would like to retrieve web pages that are the result of posting a form. Is there existing code that would let me do this easily?

Yes. Here’s a simple example that uses httplib:
#!/usr/local/bin/python
import httplib, sys, time
### build the query string
qs = “First=Josephine&MI=Q&Last=Public”
### connect and send the server a path
httpobj = httplib.HTTP(‘www.some-server.out-there’, 80)
httpobj.putrequest(‘POST’, ‘/cgi-bin/some-cgi-script’)
### now generate the rest of the HTTP headers…
httpobj.putheader(‘Accept’, ‘*/*’)
httpobj.putheader(‘Connection’, ‘Keep-Alive’)
httpobj.putheader(‘Content-type’, ‘application/x-www-form-urlencoded’)
httpobj.putheader(‘Content-length’, ‘%d’ % len(qs))
httpobj.endheaders()
httpobj.send(qs)
### find out what the server said in response…
reply, msg, hdrs = httpobj.getreply()
if reply != 200:
sys.stdout.write(httpobj.getfile().read())
Note that in general for URL-encoded POST operations, query strings must be quoted by using urllib.quote(). For example to send name=”Guy Steele, Jr.”:
>>> from urllib import quote
>>> x = quote(“Guy Steele, Jr.”)
>>> x
‘Guy%20Steele,%20Jr.’
>>> query_string = “name=”+x
>>> query_string
‘name=Guy%20Steele,%20Jr.’

Q44. Why is that none of my threads are not running? How can I make it work?

As soon as the main thread exits, all threads are killed. Your main thread is running too quickly, giving the threads no time to do any work.
A simple fix is to add a sleep to the end of the program that’s long enough for all the threads to finish:
import threading, time
def thread_task(name, n):
for i in range(n): print name, i
for i in range(10)

Q45. Installation of Python 3.6.1

Download the required 3.6.1 python, executable installer file from the www.python.org.com website.
Installation Process:
Click on the downloaded executable installer
Click On ‘Run’
Click on Customize Installation
Click on ‘Next’
Select the installation location by clicking on browse button
Click on ‘Install’
Click on ‘Yes’
Click on ‘Close’
Path: Path is an environment variable of operating system by using e=which we can make it available the softwares which are installed in the directory to all other directions of the operating system.
To set Path:
Right click on my computer
Click on properties
Click on Advanced system setting
Click on advanced
Click on environment variables
Go to system variables, select ‘path’
Click on ‘edit’
Copy the installation folder location of python software in the begging of the variable value
Click on ‘OK’
Now path setting is secured.

Q46. What Are The Implementation In Python Program?

Python program can be implemented by two ways
1. Interactive Mode (Submit statement by statement explicitly)
2. Batch Mode (Writing all statements and submit all statements)
In Interactive mode python command shell is required. It is available in installation of python cell.
In Interactive mode is not suitable for developing the projects & Applications
Interactive mode is used for predefined function and programs.
Example: 
X=1000
Y=2000
X+Y
3000
QuitX+Y
X, Y is not find.
Interactive  mode is unfit for looping purpose.
Interactive Mode:
The concept of submitting one by one python statements explicitly in the python interpreter is known as “Interactive Mode”
In Order to submit the one by one python statements explicitly to the python interpreter we use python command line shell.
Python command line shell is present in python software
We can open the python command line shell by executing python command on command prompt or terminal
Example:
c:/users/mindmajix>python
>>>3+4
       7
>>> ‘mindmajix’*3
‘mindmajix mindmajix mindmajix’
>>> x=1000
>>>y=2000
>>>x+y
      3000
>>>Quit
>>>x+y
c:/users/sailu>python
Error: name ‘X’ not defined

Batch Mode:
In the concept of writing the group of python statements in a file, save the file with extension .py and submit that entire file to the python interpreter is known as Batch Mode.
In Order to develop the python files we use editors or IDE’s
Different editors are notepad, notepad++, edit+,nano, VI, gedil and so on.
Open the notepad and write the following code
Example: 
X=1000
Y=2000
Print(x+y, x-y, x*y)
Save the file in D drive mindmajix python folder with the demo.py
Open command prompt and execute following commands
Python D:/mindmajix python/Demo.py
3000
-1000
2000.000
Save another method if we correctly set the path
D:
D:/>d mindmajix python
D:/mindmajix Python>python Demo.py
3000
-1000
2000.000

Q47. What  Are The Data Types Supports in Python Language?

    Python Int
    Python Float
    Python Complex
    Python Boolean
    Python Dictionary
    Python List
    Python Tuple
    Python Strings
    Python Set

Every data type in python language is internally implemented as a class
Python language data types are categorized into two types.
They are::

    Fundamental Types
    Collection Types

Q48. What Are The Types of Objects Support in Python Language?

Python supports are two types are of objects. They are

    Immutable Objects
     Mutable Objects

Immutable Objects

    The objects which doesn’t allow to modify the contents of those objects are known as ‘Immutable Objects’
    Before creating immutable objects with some content python interpreter verifies is already any object is available. In memory location with same content or not.
    If already object is not available then python interpreter creates new objects with that content and store that object address two reference variable.
    If already object is present in memory location with the same content creating new objects already existing object address will be given to the reference variable.

Program:
i=1000
print(i)
print(type(i))
print(id(i))
j=2000
print(j)
print(type(j))
print(id(j))
x=3000
print(x)
print(type(x))
print(id(x))
y=3000
print(y)
print(type(y))
print(id(y))

Int, float, complex, bool, str, tuple are immutable objects
Immutable objects performance is high
Applying iterations on Immutable objects takes less time
All fundamentals types represented classes objects and tuple class objects are immutable objects.

Mutable Objects:
1. The Objects which allows to modify the contents of those objects are known as ‘Mutable Objects’
2. We can create two different mutable objects with same content
Program:
x=[10,20,30]
print(x)
print(type(x))
print(id(x))
y=[10,20,30]
print(y)
print(type(y))
print(id(y))
Output:

List, set, dict classes objects are mutable objects
Mutable objects performance is low when compared to immutable objects
Applying Iterations mutable objects takes huge time

Q49. Control flow statements?

By default python program execution starts from first line, execute each and every statements only once and transactions the program if the last statement of the program execution is over.
Control flow statements are used to disturb the normal flow of the execution of the program.

Q50. What is a Tuple?

    Tuple Objects can be created by using parenthesis or by calling tuple function or by assigning multiple values to a single variable
    Tuple objects are immutable objects
    Incision order is preserved
    Duplicate elements are allowed
    Heterogeneous elements are allowed
    Tuple supports both positive and negative indexing
    The elements of the tuple can be mutable or immutable

Example:
x=()
print(x)
print(type(x))
print(len(x))
y-tuple()
print(y)
print(type(y))
print(len(y))
z=10,20
print(z)
print(type(z))
print(len(z))
p=(10,20,30,40,50,10,20,10) Insertion & duplicate
print(p)
q=(100, 123.123, True, “mindmajix”) Heterogeneous
print(q)
Output:

Q51. What is the difference Between List And Tuple?
List 	Tuple
List objects are mutable objects 	Tuple objects are immutable Objects
Applying iterations on list objects takes longer time 	Applying iterations on tuple Objects takes less time
If the frequent operation is insertion or deletion of the elements then it is recommended to use list 	If the frequent operation is retrieval of the elements then it is recommended to use tuple
List can’t be used as a ‘key’ for the dictionary 	Tuple can be used as a key for the dictionary if the tuple is storing only immutable elements

Q52. What is the Dictionary?

Dictionary objects can be created by using curly braces {} or by calling dictionary function
Dictionary objects are mutable objects
Dictionary represents key value base
Each key value pair of Dictionary  is known as a item
Dictionary keys must be immutable
Dictionary values can be mutable or immutable
Duplicate keys are not allowed but values can be duplicate
Insertion order is not preserved
Heterogeneous keys and heterogeneous values are allowed

Q53. What is Anonymous Function or Lambda Function?

A function which doesn’t contain any name is known as a anonymous function lambda function
Syntax:
Lambda arguments:expression
Lambda function we can assign to the variable & we can call the lambda function through the variable
Example:
myfunction=lambda x:x*x
a=myfunction(10)
print(a)

Output: 100
>>>

Q54. Modules Search Path?

By default python interpreter search for the imported modules in the following locations:
Current directory (main module location)
Environment variable path
Installation dependent directory
If the imported module is not found in the any one of the above locations. Then python interpreter gives error.
Built-in attributes of a module:
By default for each and every python module some properties are added internally and we call those properties as a built-in-attribute of a module

Q55. What are the Packages?

Package is nothing but a folder or dictionary which represents collection of modules
A package can also contain sub packages
We can import the modules of the package by using package name.module name
We can import the modules of the package by using package name.subpackage name.module name

Q56. What is File Handling?

File is a named location on the disk, which stores the data in permanent manner.
Python language provides various functions and methods to provide the communication between python programs and files.
Python programs can open the file, perform the read or write operations on the file and close the file
We can open the files by calling open function of built-in-modules
At the time of opening the file, we have to specify the mode of the file
Mode of the file indicates for what purpose the file is going to be opened(r,w,a,b)

Q57. What are the Runtime Errors?

The errors which occurs after starting the execution of the programs are known as runtime errors.
Runtime errors can occur because of

    Invalid Input
    Invalid Logic
    Memory issues
    Hardware failures and so on

With respect to every reason which causes to runtime error correspoing runtime error representation class is available
Runtime error representation classes technically we call as a exception classes.
While executing the program if any runtime error is occur corresponding runtime error representation class object is created
Creating runtime error representation class object is technically known as a rising exception
While executing the program if any exception is raised, then internally python interpreter verify any code is implemented to handle raised exception or not
If code is not implemented to handle raised exception then program will be terminated abnormally

Q58. What is Abnormal Termination?

The concept of terminating the program in the middle of its execution without executing last statement of the main module is known as a abnormal termination
Abnormal termination is undesirable situation in programming languages.

Q59. What is Try Block?

A block which is preceded by the try keyword is known as a try block
Syntax:
try{
   //statements that may cause an exception
}

The statements which causes to run time errors and other statements which depends on the execution of run time errors statements are recommended to represent in try block
While executing try block statement if any exception is raised then immediately try block identifies that exception, receive that exception and forward that exception to except block without executing remaining statements to try block.

Q60. What is the Difference Between Methods & Constructors?
Methods 	Constructor
Method name can be any name 	Constructor name should be
Method will be executed whenever we call a method 	Constructor will be executed automatically whenever we create a object
With respect to one object one method can be called for ‘n’ members of lines 	

With respect to one object one constructor can be executed only once
Methods are used to represent business logic to perform the operations 	Constructors are used to define & initialize the non static variable

Q61. What is the Encapsulation?

The concept of binding or grouping related data members along with its related functionalities is known as a Encapsulation.

Q62. What is Garbage Collection?

The concept of removing unused or unreferenced objects from the memory location is known as a Garbage Collection.
While executing the program, if garbage collection takes place then more memory space is available for the program and rest of the program execution becomes faster.
Garbage collector is a predefined program, which removes the unused or unreferenced objects from the memory location
Any object reference count becomes zero then we call that object as a unused or unreferenced object
Then no.of reference variables which are pointing the object is known as a reference count of the object.
While executing the python program if any object reference count becomes zero, then internally python interpreter calls the garbage collector and garbage collector will remove that object from memory location.

Q63. Executing DML Commands Through Python Programs?

DML Commands are used to modify the data of the database objects
Whenever we execute DML Commands the records are going to be modified temporarily
Whenever we run “rollback” command the modified records will come back to its original state
To modify the records of the database objects permanently we use “commit” command
After executing the commit command even though we execute “rollback” command, the modified records will not come back to its original state
Create the emp1 table in the database by using following command
Create table emp1 as select * from emp;
Whenever we run the DML commands through the python program, then the no.of records which are modified because of that command will be stored into the rowcount attribute of cursor object
After executing the DML Command through the python program we have to call commit method of cursor object.

Q64. What is Multithreading?

Thread Is a functionality or logic which can execute simultaneously along with the other part of the program
Thread is a light weight process
Any program which is under execution is known as process 
We can define the threads in python by overwriting run method of thread class
Thread class is a predefined class which is defined in threading module
Thread in module is a predefined module
If we call the run method directly the logic of the run method will be executed as a normal method logic
In order to execute the logic of the run method as a we use start method of thread class.
Example
Import threading
Class x(threading.Thread):
      Def run(self):
         For p in range(1, 101):
              print(p)
Class y(threading.Thread):
      Def run(self):
           For q in range(1, 101):
              print(q)
x1=x()
y1=y()
x1.start()
y1.start()

Q65. What is scheduling?

Among multiple threads which thread as to start the execution first, how much time the thread as to execute after allocated time is over, which thread as to continue the execution next this comes under scheduling
Scheduling is highly dynamic

Q66. What is Threads Life Cycle?

Threads Life Cycle

Creating the object of a class which is overwriting run method of thread class is known as a creating thread
Whenever thread is created then we call thread is in new state or birth state thread.
Whenever we call the start method on the new state threads then those threads will be forwarded for scheduling
The threads which are forwarded for scheduling are known as ready state threads
Whenever scheduling time occurs, ready state thread starts execution
The threads which are executing are known as running state threads
Whenever sleep fun or join methods are called on the running state threads then immediately those threads will wait.
The threads which are waiting are known as waiting state threads
Whenever waiting time is over or specified thread execution is over then immediately waiting state threads are forwarded for scheduling.
If running state threads execution is over then immediately those threads execution will be terminated
The threads which execution is terminated are known as dead state threads.

Q67. For loop is implemented in python language as follows?

For element in iterable:
iter-obj=iter(iterable)
While true;
Try:
element=next(iter_obj)
except(slop iteration)
Break

For loop takes the given object, convert that object in the form of iterable object & gets the one by one element form the iterable object.
While getting the one by value element from the iterable object if stop iteration exception is raised then for loop internally handle that exception

Q68. OS Module

OS Module is a predefined module and which provides various functions and methods to perform the operating system related activities, such as creating the files, removing the files, creating the directories removing the directories, executing the operating system related commands, etc.
Example:
Import os
cwd=os.getwd()
print(“1”, cwd)
os.chdir(“samples”)
print(“2”, os.getcwd())
os.chdir(os.pardir)
print(“3”,os.getcwd())

Output:

Q69. What is Hierarchical Inheritance?

The concept of inheriting the properties from one class into multiple classes separately is known as hierarchical inheritance.
Example:
Class x(object):
Def m1(self):
print(“in m1 of x”)
Class y(x):
Def m2(self):
print(“in m2 of y”)
Class z(x):
Def m3(self):
print(“in m3 of z”)
y1=y()
y1.m1()
y1.m2()
a=y1.--hash--()
print(a)
z1=z()
z1.m1()
z1.m3()
b=z1.hash--()
print(b)

Output:
M m1 of X
In m2 of Y
2337815
In m1 of X
In m3 of Z
2099735
>>>

Q70. What Are Applications of Python?
Applications of Python
Applications of Python 	Java 	.Net
Automation App 	NO 	NO
Data Analytics 	NO 	NO
Scientific App 	NO 	NO
Web App 	Yes 	Yes
Web Scrapping 	NO 	NO
Test Cases 	Yes 	Yes
Network with JOT 	Yes 	NO
Admin Script 	NO 	NO
GUI 	Yes 	Yes
Gaming 	Yes 	Yes
Animation 	NO 	NO


1) What is Python? What are the benefits of using Python?

Python is a programming language with objects, modules, threads, exceptions and automatic memory management. The benefits of pythons are that it is simple and easy, portable, extensible, build-in data structure and it is an open source.

2) What is PEP 8?

PEP 8 is a coding convention, a set of recommendation, about how to write your Python code more readable.

3) What is pickling and unpickling?

Pickle module accepts any Python object and converts it into a string representation and dumps it into a file by using dump function, this process is called pickling. While the process of retrieving original Python objects from the stored string representation is called unpickling.

4) How Python is interpreted?

Python language is an interpreted language. Python program runs directly from the source code. It converts the source code that is written by the programmer into an intermediate language, which is again translated into machine language that has to be executed.

5) How memory is managed in Python?

    Python memory is managed by Python private heap space. All Python objects and data structures are located in a private heap. The programmer does not have an access to this private heap and interpreter takes care of this Python private heap.
    The allocation of Python heap space for Python objects is done by Python memory manager. The core API gives access to some tools for the programmer to code.
    Python also have an inbuilt garbage collector, which recycle all the unused memory and frees the memory and makes it available to the heap space.

6) What are the tools that help to find bugs or perform static analysis?

PyChecker is a static analysis tool that detects the bugs in Python source code and warns about the style and complexity of the bug. Pylint is another tool that verifies whether the module meets the coding standard.

7) What are Python decorators?

A Python decorator is a specific change that we make in Python syntax to alter functions easily.

8) What is the difference between list and tuple?

The difference between list and tuple is that list is mutable while tuple is not. Tuple can be hashed for e.g as a key for dictionaries.

9) How are arguments passed by value or by reference?

Everything in Python is an object and all variables hold references to the objects. The references values are according to the functions; as a result you cannot change the value of the references. However, you can change the objects if it is mutable.

10) What is Dict and List comprehensions are?

They are syntax constructions to ease the creation of a Dictionary or List based on existing iterable.

11) What are the built-in type does python provides?

There are mutable and Immutable types of Pythons built in types Mutable built-in types

    List
    Sets
    Dictionaries

Immutable built-in types

    Strings
    Tuples
    Numbers

12) What is namespace in Python?

In Python, every name introduced has a place where it lives and can be hooked for. This is known as namespace. It is like a box where a variable name is mapped to the object placed. Whenever the variable is searched out, this box will be searched, to get corresponding object.

13) What is lambda in Python?

It is a single expression anonymous function often used as inline function.

14) Why lambda forms in python does not have statements?

A lambda form in python does not have statements as it is used to make new function object and then return them at runtime.

15) What is pass in Python?

Pass means, no-operation Python statement, or in other words it is a place holder in compound statement, where there should be a blank left and nothing has to be written there.

16) In Python what are iterators?

In Python, iterators are used to iterate a group of elements, containers like list.

17) What is unittest in Python?

A unit testing framework in Python is known as unittest. It supports sharing of setups, automation testing, shutdown code for tests, aggregation of tests into collections etc.

18) In Python what is slicing?

A mechanism to select a range of items from sequence types like list, tuple, strings etc. is known as slicing.

19) What are generators in Python?

The way of implementing iterators are known as generators. It is a normal function except that it yields expression in the function.

20) What is docstring in Python?

A Python documentation string is known as docstring, it is a way of documenting Python functions, modules and classes.

21) How can you copy an object in Python?

To copy an object in Python, you can try copy.copy () or copy.deepcopy() for the general case. You cannot copy all objects but most of them.

22) What is negative index in Python?

Python sequences can be index in positive and negative numbers. For positive index, 0 is the first index, 1 is the second index and so forth. For negative index, (-1) is the last index and (-2) is the second last index and so forth.

23) How you can convert a number to a string?

In order to convert a number into a string, use the inbuilt function str(). If you want a octal or hexadecimal representation, use the inbuilt function oct() or hex().

24) What is the difference between Xrange and range?

Xrange returns the xrange object while range returns the list, and uses the same memory and no matter what the range size is.

25) What is module and package in Python?

In Python, module is the way to structure program. Each Python program file is a module, which imports other modules like objects and attributes.

The folder of Python program is a package of modules. A package can have modules or subfolders.

26) Mention what are the rules for local and global variables in Python?

Local variables: If a variable is assigned a new value anywhere within the function's body, it's assumed to be local.

Global variables: Those variables that are only referenced inside a function are implicitly global.

27) How can you share global variables across modules?

To share global variables across modules within a single program, create a special module. Import the config module in all modules of your application. The module will be available as a global variable across modules.

28) Explain how can you make a Python Script executable on Unix?

To make a Python Script executable on Unix, you need to do two things,

    Script file's mode must be executable and
    the first line must begin with # ( #!/usr/local/bin/python)

29) Explain how to delete a file in Python?

By using a command os.remove (filename) or os.unlink(filename)

30) Explain how can you generate random numbers in Python?

To generate random numbers in Python, you need to import command as

import random

random.random()

This returns a random floating point number in the range (0,1)

31) Explain how can you access a module written in Python from C?

You can access a module written in Python from C by following method,

Module = =PyImport_ImportModule("<modulename>");

32) Mention the use of // operator in Python?

It is a Floor Divisionoperator , which is used for dividing two operands with the result as quotient showing only digits before the decimal point. For instance, 10//5 = 2 and 10.0//5.0 = 2.0.

33) Mention five benefits of using Python?

    Python comprises of a huge standard library for most Internet platforms like Email, HTML, etc.
    Python does not require explicit memory management as the interpreter itself allocates the memory to new variables and free them automatically
    Provide easy readability due to use of square brackets
    Easy-to-learn for beginners
    Having the built-in data types saves programming time and effort from declaring variables

34) Mention the use of the split function in Python?

The use of the split function in Python is that it breaks a string into shorter strings using the defined separator. It gives a list of all words present in the string.

35) Explain what is Flask & its benefits?

Flask is a web micro framework for Python based on "Werkzeug, Jinja 2 and good intentions" BSD licensed. Werkzeug and jingja are two of its dependencies.

Flask is part of the micro-framework. Which means it will have little to no dependencies on external libraries. It makes the framework light while there is little dependency to update and less security bugs.

36) Mention what is the difference between Django, Pyramid, and Flask?

Flask is a "microframework" primarily build for a small application with simpler requirements. In flask, you have to use external libraries. Flask is ready to use.

Pyramid are build for larger applications. It provides flexibility and lets the developer use the right tools for their project. The developer can choose the database, URL structure, templating style and more. Pyramid is heavy configurable.

Like Pyramid, Django can also used for larger applications. It includes an ORM.

37) Mention what is Flask-WTF and what are their features?

Flask-WTF offers simple integration with WTForms. Features include for Flask WTF are

    Integration with wtforms
    Secure form with csrf token
    Global csrf protection
    Internationalization integration
    Recaptcha supporting
    File upload that works with Flask Uploads

38) Explain what is the common way for the Flask script to work?

The common way for the flask script to work is

    Either it should be the import path for your application
    Or the path to a Python file

39) Explain how you can access sessions in Flask?

A session basically allows you to remember information from one request to another. In a flask, it uses a signed cookie so the user can look at the session contents and modify. The user can modify the session if only it has the secret key Flask.secret_key.

40) Is Flask an MVC model and if yes give an example showing MVC pattern for your application?

Basically, Flask is a minimalistic framework which behaves same as MVC framework. So MVC is a perfect fit for Flask, and the pattern for MVC we will consider for the following example

from flask import Flask

app = Flask(_name_)

@app.route("/")

Def hello():

return "Hello World"

app.run(debug = True)
	

In this code your,

    Configuration part will be

from flask import Flask

app = Flask(_name_)

    View part will be

@app.route("/")

Def hello():

return "Hello World"

    While you model or main part will be

app.run(debug = True)

41) Explain database connection in Python Flask?

Flask supports database powered application (RDBS). Such system requires creating a schema, which requires piping the shema.sql file into a sqlite3 command. So you need to install sqlite3 command in order to create or initiate the database in Flask.

Flask allows to request database in three ways

    before_request() : They are called before a request and pass no arguments
    after_request() : They are called after a request and pass the response that will be sent to the client
    teardown_request(): They are called in situation when exception is raised, and response are not guaranteed. They are called after the response been constructed. They are not allowed to modify the request, and their values are ignored.

42) You are having multiple Memcache servers running Python, in which one of the memcacher server fails, and it has your data, will it ever try to get key data from that one failed server?

The data in the failed server won't get removed, but there is a provision for auto-failure, which you can configure for multiple nodes. Fail-over can be triggered during any kind of socket or Memcached server level errors and not during normal client errors like adding an existing key, etc.

43) Explain how you can minimize the Memcached server outages in your Python Development?

    When one instance fails, several of them goes down, this will put larger load on the database server when lost data is reloaded as client make a request. To avoid this, if your code has been written to minimize cache stampedes then it will leave a minimal impact
    Another way is to bring up an instance of Memcached on a new machine using the lost machines IP address
    Code is another option to minimize server outages as it gives you the liberty to change the Memcached server list with minimal work
    Setting timeout value is another option that some Memcached clients implement for Memcached server outage. When your Memcached server goes down, the client will keep trying to send a request till the time-out limit is reached

44) Explain what is Dogpile effect? How can you prevent this effect?

Dogpile effect is referred to the event when cache expires, and websites are hit by the multiple requests made by the client at the same time. This effect can be prevented by using semaphore lock. In this system when value expires, first process acquires the lock and starts generating new value.

45) Explain how Memcached should not be used in your Python project?

    Memcached common misuse is to use it as a data store, and not as a cache
    Never use Memcached as the only source of the information you need to run your application. Data should always be available through another source as well
    Memcached is just a key or value store and cannot perform query over the data or iterate over the contents to extract information
    Memcached does not offer any form of security either in encryption or authentication


[Mind Boggling Python FAQ](https://docs.python.org/3/faq/programming.html)
