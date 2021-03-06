Structs
=======

Structs implement composite types.

.. code-block:: zaalang

  struct Pixel
  {
    int x,
    int y,
    f32 intensity,
    
    Pixel() = default;
    Pixel(Pixel &&) = default;
    ~Pixel() = default;
  }

Every struct that wants to be instantiated needs a constructor and a destructor. These are not implicitly provided but may be defaulted.
 
Methods
-------
 
Functions may be declared within struct scope. These are then callable via scoped lookup and by member operator (.).
  
.. code-block:: zaalang

  struct Pixel
  {
    int x,
    int y,
    
    fn move_to(this mut &, int x, int y) -> void
    {
      this.x = x;
      this.y = y;
    }
  }
  
A struct method must explicitly declare a this parameter for access to member fields. (the "this mut &" is equivalent to "Pixel mut &this")

Using the member operator (.), this function may be called as px.move_to(3, 4).

Templates
---------

Structs may be generic over type arguments.

.. code-block:: zaalang

  struct Pixel<T>
  {
    int x,
    int y,
    T intensity,
    
    Pixel() = default;
    Pixel(Pixel &&) = default;
    ~Pixel() = default;
  }

Properties
----------

Since a method without parameters may be called without the parenthesis, a getter can naturally be defined. A method with the same name ending in '=' can 
also be defined which will act as a setter function.

.. code-block:: zaalang

  struct Pixel
  {
    int _x,
    int _y,
    
    fn x(this &) { return &this._x; }
    fn x=(this mut &, int x) { this._x = x; }
  }

Inheritance
-----------

A struct may derive from a single other type. Methods and fields of the base object will be available within scope or via an implicit "super" field.

.. code-block:: zaalang

  struct Pixel : Point
  {
    ...
  }
