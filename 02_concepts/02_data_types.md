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
Mathematically speaking, an integer is *any* whole number, but computers only have a finite amount of memory, meaning we cannot store arbirarily large numbers. Instead, a fixed number of bits is used to store each integer, ranging from 8 to 128 bits. 

In Mokka, the number of bits that gets allocated for an integer variable binding is explicitly given. The table below lists the datatypes for storing integers in Mokka.

|  Length  | Signed | Unsigned |
|:--------:|:------:|:--------:|
|  8 bits  |   i8   |    u8    |
|  16 bits |   i16  |    u16   |
|  32 bits |   i32  |    u32   |
|  64 bits |   i64  |    u64   |
| 128 bits |  i128  |   u128   |

Each datatype is either signed or unsigned and has an explicit size. Signed integers reserve the first bit to indicate whether the number is positive or negative; unsigned integers do not reserve this bit, and can not be negative.






