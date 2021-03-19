Expressions
===========

Expressions comprise of the expected list of operators.

Reference
---------

The reference operator (&) casts an lvalue object reference to an explicit reference. Explicit references are implicitly convertible to pointers.

.. code-block:: zaalang

  fn foo(int &i)
  {
    return &i; // the return type is an int &
  }

Explicit references also allow references to be re-bindable.

.. code-block:: zaalang

  fn foo(int &i, int &j)
  {
    if (j < i)
      &i = &j; // re-bind &i to &j
  
    return i; // will return the smaller of i and j
  }

Member
------

The member operator (.) will will access a field or call a method on an object. If the object is a pointer, it will automatically be dereferenced first.

.. code-block:: zaalang

  fn foo(object *ptr)
  {
    ptr.intfield = 99; // ptr will be dereferenced
    ptr.foobar(1.1, false); // call foobar with an object &, a float and a bool
  }
  
In the above, foobar may be a method on object or a free function in the scope of object.
  
Literal
-------

The literal operator (#) will evaluate the sub-expression at compile time to form a literal value. All parameters must be available at compile time.

.. code-block:: zaalang

  fn main()
  {
    return #calc(7, 11); // main will compile to a simple return of a constant, whatever calc evaluates to at compile time.
  }
  
Forward
-------

The forwarding operator (&&) forwards the properties of a qualified reference or the result of a call expression.

Call
----

Function calls may use named parameters, specify explicit type arguments, and ellide parenthesis when no parameters are provided.

.. code-block:: zaalang

  fn main()
  {
    foo(i: 15, j: 0); // named parameters
    bar<int>();       // explicit type argument
  }

Lambdas
-------

Lambda expressions declare a callable object of lambda type. Non capturing lambdas may be converted to a function pointer.

.. code-block:: zaalang

  fn main()
  {
    fn foo(int i)          // foo is a lambda
    {
      return i;
    }
   
    var bar = fn(int i) {  // bar is also a lambda
      return 2*i;
    };
    
    foo(2); // call foo
    bar(3); // call bar
    
    var k = 99;
    
    fn baz[k](int i)       // baz is a lambda, captures k by reference
    {
      return k * i;
    }
  }
