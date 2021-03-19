Statements
==========

Statements may occur in function bodies.

Constants
---------

Constants may be declared within a function body. They must be compile time expressions.

.. code-block:: zaalang

  fn main()
  {
    const PI = 3.14;
  }

Variables
---------

Variables may be declared with the 'var' or 'let' keywords. The type of a variable is always inferred. 

.. code-block:: zaalang

  fn main()
  {
    var i = 9;          // will default to i32 if no other inference occurs
    let j = f32(3.14);  // let means j may not be modified (but is still a runtime expression)
    
    var &x = foo();     // const reference to the result of foo
    var mut &y = bar(); // mutable reference to the result of bar
  }
  
Conditionals
------------

.. code-block:: zaalang

  fn main()
  {
    var x = baz();
    
    if (x == 0)
      foo();
  }

Loops
-----

.. code-block:: zaalang

  fn main()
  {
    while(foo())                  // a while loop
      bar();
    
    for(var x = 0; x != 10; ++x)  // for loop, iterates x = 0 through x = 9
      bar();
      
    rof(var x = 10; x == 0; --x)  // rof loop, iterates x = 9 through x = 0
      bar();
  }
  
Switch
------

Switch statement will disptch based on an integer, an enum or a tagged union.

.. code-block:: zaalang

  fn main()
  {
    var x = OptionalInteger::Some(11);
    
    switch(x)
    {
      case None:
        foo();
        
      case Some(i):
        bar(i);
    }
  }
