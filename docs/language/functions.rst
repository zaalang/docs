Functions
=========

Functions are introduced with the 'fn' keyword and use trailing return types.

Parameters are specified as type then name and may include a default expression.

.. code-block:: zaalang

  fn foo(int i, f64 j = 11.4) -> bool;

The return type may be ommitted, in which case the result type may be deduced.

Parameters are passed by value unless specified as reference parameters.

.. code-block:: zaalang

  fn foo(int &i, f64 mut &j); // i is const reference, j is mutable

Const
-----

A function maked 'const' will be evaluated at compile time if all of it's parameters are compile time literals.

Parameters types preceeded with the hash (#) symbol are required to be literals. Hence will always be known at compile time.

.. code-block:: zaalang

  const fn baz(u8 i) { return i*i; } // may be evaluated at compile time
  const fn baz(#u8 i) { return i*i; } // *will* be evaluated at compile time
  
Expressions may also be required to execute at compile time using the literal operator (#). eg. #bar(99);

Templates
---------

Functions may be templated by supplying a type argument or by using a concept as the type specifier.

.. code-block:: zaalang

  fn foo(var k); // var is a builtin concept without constraints
  fn bar<T>(T mut &k); // T is a type argument
  
Literal parameters, types preceeded with the hash (#) symbol, are a form of type argument (non-type template argument)

.. code-block:: zaalang

  fn foo(#f32 x); // essentially the same as fn foo<X>() where X is a float literal 

Qualifiers
----------

To match a type that may be const, or may be mutable, a qualified reference is required.

.. code-block:: zaalang

  fn foo(int &x);     // x is a const reference to an int
  fn foo(int mut &x); // x is a mutable reference to an int
  fn foo(int &&x);    // x is a qualified reference to an int, accepting both const and non const objects
  
Further, qualified references capture whether the passed object is an rvalue. Note that using a qualified reference generates a templated function.

The forwarding operator (&&) can be used to "pass along" the rvalue-ness of a qualified reference. eg. &&x

Packs
-----

Parameter packs allow a function to accept many parameters. All the parameters will be packed up into a tuple at the calling site.

.. code-block:: zaalang

  fn foo<Args>(Args ...args);
  fn bar<Args>(Args && ...args);
  
Here, the args parameter will be a tuple, Args type will be the tuple type. For function bar, the tuple will contain qualified references.

Match
-----

A function may specify a match clause. This clause generates constraints on the template parameters and may be used to infer literal types.

.. code-block:: zaalang

  fn foo<T>(T x)
    match (T x) { u16(x); }
  {
  }

Here, T is being constrained to a type for which the body "{ u16(x); }" compiles. If foo is called with an integer literal, eg. foo(42), 
which has no runtime type, this will coerce the literal to a u16.

Where
-----

A function may specify a where clause. This clause generates constraints on the functions viability. Must be a compile time expression.

.. code-block:: zaalang

  fn foo(#int x)
    where x == 2 // known at compile time since x is a literal type (#)
  {
  }
