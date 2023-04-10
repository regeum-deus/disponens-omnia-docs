Variables
===================
In disponens omnia variables are declared as so:
::
  int x(0);

this is what it would look like in c:
::
  int x = 0;

why not use =? Well, in disponens omnia, ``"(<params>)"`` is the push operator. The push operator takes whatever is placed in it and pushes it into whatever is operated on. We also have the pull operator ``"[<params>]"`` which we will talk about more later.

In disponens omnia variables are immutable by default:
::
  int x(0);
  x(10);
will return an error, to make a variable mutable write it as so:
::
  mut int x(0);

This is because you should think about whether or not your variable needs to be mutable.
There are four datatypes in disponens omnia:

1. char, 1 byte
2. int, 4 bytes
3. float, 4 bytes
4. double, 8 bytes

A char is simply a one byte integer interpereted as an ascii value whenever possible, a char literal looks like this: ``' '``

An int is simply a four byte integer, an int literal looks like this: ``0``

A float is simply a four bit floating point number that can represent decimals, a float literal looks like this: ``0.0``

A double is simply an eight bit double precision floating point number that can reprecent decimals with twice as much precision as a float, a double literal looks like this: ``0.0``

There are two datatype operators:

* signed
* unsigned

signed simply lets you use negative values whilst unsigned does not. Using unsigned will effectively double the maximum value. Of an int.

You cannot sign/unsign doubles or floats

Arrays
============
As you may know C generally handles arrays like so:
::
  int arr[10];

or as soL:
::
  int *arr = malloc(10 * sizeof(int));

which needs pointers, and given we dont like mutability pointers are a little to free for us. So instead what we will do is just simplify pointers to arrays. As so:
::
  int *arr(10);

what does this mean? Well its simply the equivalent to this:
::
  int arr[10];

we use the array operator ``*`` to signify we are setting the length of the array and use the push operator ``(<parameter>)`` to set the size.

We operate on arrays using the pull operator ``[<parameter>]`` i.e:
::
  int *arr(10);
  *arr[5];

will get the 5fth value of ``arr`` it is equivalent to so:
::
  int arr[10];
  arr[5];

Structs
==============
structs are simply a way of making a datatype composed of multiple others. You can define one like so:
::
  struct vec(int x, int y, int z);
the equivalent c:
  struct vec {
    int x;
    int y;
    int z;
  };

structs in disponens omnia can be instanced like so:
::
  vec pos(0, 0, 0);
the equivalent c:
  struct vec pos;
  pos.x = 0;
  pos.y = 0;
  pos.z = 0;
to set properties of our struct we use the pull operation
::
  mut vec pos(0, 0, 0);
  pos[0](10);
the equivalent c:
  struct vec pos;
  pos.x = 0;
  pos.y = 0;
  pos.z = 0;
  pos.x = 10;

*note: mut is still important here*

and thats it for structs.

Enums
==========
Enums are simply a way to get rid of magic numbers. Lets say we have a set of statements as so:
::
  if(x == 120) {
    code you cant see here
  }

tell me what this if statement is looking for, you cant tell me can you. No because magic numbers, magic numbers are random numbers that have zero meaning outside of the context they are in. You could instead use an enum like so:
::
  enum constants {
    MAX_SPEED = 120,
    MONSTER_HEALTH = 10,
  }
and change our if statement to:
::
  if(x == MAX_SPEED) {
  }

now you can tell at a glance what is going on. Enums are simply a set of integers put under a common banner, enums also can be used as so:
::
  enum types {
    integer,
    character,
    floating_point,
  }
  types t(integer);

Which sets a variable t to enum types.

enums are not strongly typed meaning that an enum and an int are the same type and can be compared.

Conditional code
================================
all coding languages hafve an if/else:
::
  if(condition) {
  } else {
  }

the if statement simply takes a condition operator and runc the code in its block if true, else it runs the block in the else statement. The conditional operators are as follows:

is equal to, uses the pull operator while passing in a literal:
::
  x[10]

is not equal to:
::
  !x[10]

greater than:
::
  x > 10

less than:
::
  x < 10

and:
::
  x && b

or:
::
  x || b

Math operators
============================
the math operators are as follows:

add:
::
  x + b

subtract:
::
  x - b

multiply:
::
  x * b

division:
::
  x / b

modulo division:
::
  x % b

Functions
==================
Well, we're here. Functions are variables and can be treated as such, they are declared the same way other than the fact that you give them a block like so:
::
  int f(int x) {
    return x * 2;
  }

You cannot mutate parameters of functions so this:
::
  int f(int x) {
    x(x * 2);
  }

is invalid.

You may have also noticed that disponens omnia contains no loops, we achieve loops with recursion:
::
  int f(int x, int c) {
    if(c > 0) return f(x, c - 1) + 1;
    else return x + 1;
  }
would be equivalent to:
::
  for(int i = 0; i < c; i++)
    x += 1;

this is simply because loops require alot of mutation while recursion does not.


To start a program \:MAIN\: is the entry point
::
  :MAIN: {
    ...
  }

To close off here is a fibonacci in disponens omnia:
::
  int fibonacci(int x) {
    if(x < 1 || x[1]) return 1;
    return fibonacci(x - 1) + fibonacci(x - 2);
  }
  :MAIN: {
    fibonacci(100);
  }
