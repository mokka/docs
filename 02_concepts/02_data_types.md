Data types in Mokka
===================
Mokka is a statically typed language, meaning it needs to know the type of every value at compile time. Often, the compiler can infer the type of a value based off the value and how it is used, but there are cases where it can't. In such a case, we must add a type annotation:

```
function main();
  # -snip-

  divisor: string = 12.parse() # Type annotation required!
  write(to := STDOUT, divisor)
  
  from std.io import write, STDOUT
```

Different type annotations exist for different data types.

## Scalars
A scalar (or variable) represents a single value. There are four primary scalar types in Mokka, namely: integers, booleans, characters and floating-point numbers.

### Integers
Mathematically speaking, an integer is *any* whole number, but computers only have a finite amount of memory, meaning we cannot store arbirarily large numbers. Instead, a fixed number of bits are used to store each integer, ranging from 8 to 128 bits. 

In Mokka, the number of bits that gets allocated for an integer is explicitly given. The table below lists the datatypes for storing integers in Mokka.

|  Length  | Signed | Unsigned |
|:--------:|:------:|:--------:|
|  8 bits  |   i8   |    u8    |
|  16 bits |   i16  |    u16   |
|  32 bits |   i32  |    u32   |
|  64 bits |   i64  |    u64   |
| 128 bits |  i128  |   u128   |

Each datatype is either signed or unsigned and has an explicit size. Signed integers reserve the first bit to indicate whether the number is positive or negative; unsigned integers do not reserve this bit, and can not be negative.

> **Integer Overflow**<br/>A fixed number of bits are used to store each integer. Suppose we have a variable of type `i8`, which can hold any integer between -128 and 127. If we then try to assign a value outside of this range to this variable, an integer overflow will occur.

### Chars
A character (`char`) is any Unicode character. The following code shows how to use this datatype:

```
function main();
  love: char = '🖤' # Note the single quotes (') as opposed to double quotes.
  write(to := STDOUT, love) # Prints a heart
  
  from std.io import write, STDOUT
```

### Floating-point numbers
Mokka has two types for floating-point numbers, `f32` and `f64`, which are respectively 32 and 64 bits long.

An example of floating-point numbers in the wild:

```
function main() -> int;
  pi: f64 = 3.1415926535
  earth_radius := 6371
  earth_circumference: u32 = 2 * pi * earth_radius
  
  write(to := STDOUT, earth_circumference) # Prints 40030
  
  from std.io import write, STDOUT
```

### Boolean
A `boolean` in Mokka is either `true` or `false` and is one byte long.

```
function main();
  if(stars_aligned());
    write(to := STDOUT, "Stars aligned!")

  from std.io import write, STDOUT
  
function stars_aligned() -> boolean;
  return random_integer(0, 100) == 1

  from std.rand import random_integer
```

## Compound datatypes

### Arrays
An array is a collection of values of the same type with a fixed length. In Mokka, and many other programming languages, values going into an array are written as a comma-separated list surrounded by square brackets:

```
function main();
  emoticons := ['😀','😁','😎','💜']
```

An array is less flexible than a vector; a `vector` has a dynamic length and allows you to add or remove elements from it, while an array has a fixed length and can only be read from.

You can specify a type, like so:

```
function main();
  emoticons: char = ['😀','😁','😎','💜']
```

The array named `emoticons` will contain four elements of type `char`.

#### Accessing elements
Elements of an array can be accessed using indexing, like so:

```
function main();
  emoticons: char = ['😀','😁','😎','💜']
  
  heart := emoticons[3] # Indexes start at 0
```

#### Accessing undefined values
If you try to access an undefined value in an array (for instance, index `4` in the array `emoticons`), you will get a compilation error.

The following code will not compile:

```
function main();
  emoticons: char = ['😀','😁','😎','💜']
  index: i8 = 10
  
  secret_element: char = emoticons[index]
```

The compiler will produce the following error:

```
You tried to access index `10` in the array 'emoticons' here:

5 | secret_element: char = emoticons[index]
                           ^^^^^^^^^^^^^^^^
                           
But the array 'emoticons' only has a size of `4`, therefore, its greatest
index is `3`.
```

#### Mutable arrays
To make an array mutable, add the keyword `mutable` to the variable binding, like so:

```
function main();
  mutable emoticons: char = ['😀','😁','😎','💜']
```

Mutable arrays still have a fixed size, but the individual elements can be altered:

```
function main();
  mutable emoticons: char = ['😀','😁','😎','💜']
  
  emoticons[3] = '💔'
```

Please note that if you re-assign an element, the new value must be of the same type as the previous value. The following code would not compile:

```
function main();
  mutable emoticons: char = ['😀','😁','😎','💜']
  
  emoticons[3] = 12
```

The compiler would give the following error:

```
I tried to re-assign an element in the following mutable array:

2 | mutable emoticons: char = ['😀','😁','😎','💜']

But the re-assigned value is not a char, but an integer:

3 | emoticons[3] = 12

You must assign the new value to a new name.
```
