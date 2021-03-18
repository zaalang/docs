========
Overview
========

Welcome to the reference documentation for the zaalang programming language.

Zaalang is a compiled language in the vein of c++, nothing groung breaking, just a done from scratch 
compiler with familiar usage and base functionality. 

Features include :
- basic types
- arrays and structs
- built-in tuples
- built-in tagged unions
- usual array of statements (if, while, for, rof, switch)
- modules
- templates & concepts
- lambdas & captures
- compile time execution

Example
-------

.. code-block:: zaalang

   import std.stdio;
   
   fn main() -> void
   {
     std::print("Hello World!");
   }


YMMV
----

Now I can say with some certainty that anything I haven't personally tested likely won't work. And if you do manage 
to get the compiler to not crash, the error messages will be completely useless. So, yes... there is more work to do.

