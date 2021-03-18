Unions
======

Unions implement a tag and common storage composite type.

.. code-block:: zaalang

  union OptionalInteger
  {
    None,
    Some(i64),
    
   ~OptionalInteger() = default;
  }

The union may contain only one of it's fields at any given time. Each field also acts as a constructor. The implicit first field, named "kind" 
provides an enum representing the active element.

Unions may contain methods in a similar fashion to structs.
