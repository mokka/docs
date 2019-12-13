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
Mathematically speaking, an integer is *any* whole number.
