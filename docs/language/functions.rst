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

Templates
---------

Functions may be templated by supplying a type argument or by using a concept as the type specifier.

.. code-block:: zaalang

  fn foo(var k); // var is a builtin concept without constraints
  fn bar<T>(T mut &k); // T is a type argument
