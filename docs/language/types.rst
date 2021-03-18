Types
=====

The primitive types are
 - void
 - bool
 - char (32-bit type)
 - i8, i16, i32, i64
 - u8, u16, u32, u64
 - f32, f64
 - isize, usize (i64 and u64 respectivly, distinct types)
 - int, float (i32 and f64 respectivly, aliased types)
 
Type composition includes the usual pointer (*), array ([]), reference (&) and tuple (()).

Pointers and References are const by default, use "mut" for mutability (eg int mut *)
