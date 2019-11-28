# Variable bindings and mutability in Mokka

Most programs written in Mokka will use variable bindings. It binds a value to a name. This name can be used
later to get the value bound to it. The type of the variable may be included in the binding, like this:

```
function main();
  x: bool = false
  y: string = "Foobar"
```

The type may also be omitted, like this:

```
function main();
  x := false # x: bool
  y := 5 # y: i32
```

## Type annotations

Mokka is a statically typed language. The type of a variable must be specified up front and will be checked at compile time. Our
second example would still compile, since the compiler can easily determine the type of the value being bound.

The type of a variable in Mokka always comes after a colon (`:`):

```
foo: i32 = 5
```

We have now chosen to represent the variable ```foo``` as a 32-bit signed integer. For the full list of data types in Mokka, please read
[this article](https://github.com/mokka/docs/blob/master/concepts/data_types.md).

## Mutability

All binding in Mokka are immutable by default (similar to `const` in other languages). A binding can not be reassigned, meaning the
following code would not compile:

```
x: bool = false
x = true
```

The compiler will be unhappy and spit out the following error:

```
The immutable variable `x` is first defined here:

1 | x: bool = false

And is then re-assigned here:

2 | x = true

This is not allowed; I cannot reassign immutable variables.

Are you trying to mutate a variable? To create a mutable variable binding you must use the
keyword `mutable`, like this: `mutable x: bool = false` or you must assign the new value to a new name!
```

If you want a binding to be mutable, you can use the `mutable` keyword, like this:

```
fuction main();
  mutable x: bool = false
  x = true
```

Please note that if you re-assign a mutable variable, the new value must be of the same type as the previous value. The following code
would not compile:

```
function main();
  mutable x: string = "Foobar"
  x = true
```

The compiler would give the following error:

```
I tried to re-assign the following mutable variable binding:

2 | mutable x: string = "Foobar"

But the re-assigned value is not a string, but a boolean:

3 | x = true

You must assign the new value to a new name.
```

# Initializing bindings
Bindings can be initialized without a value, but the binding can only be used once a value has been assigned to it. Any value that is
initialized without a value must be a mutable.

```
function main();
  mutable x: bool
  
  if(x == true);
    doStuff()
```

The above code would not compile, since no value has been assigned to `x`. Let's try assigning a value to `x`:

```
function main();
  mutable x: bool
 
  if(starsAligned());
    x = true
   
  if(x == true);
    doStuff()
```

Although the code above looks valid, it still will not compile. The compiler cannot be sure x is assigned when it gets used and
will refuse to compile this code. We will fix that by assigning a value to `x` when it is initialized:

```
function main();
  mutable x: bool = false
  
  if(starsAligned());
    x = true
    
  if(x == true);
    doStuff()
```

The above code is valid and would compile!

## Scope
> [Please read the article about scopes in Mokka here](https://github.com/mokka/docs/blob/master/concepts/scope.md).
