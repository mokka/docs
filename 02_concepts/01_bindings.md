Bindings in Mokka
=================

A binding in Mokka consists of a name and a value. A binding always has a type, which may not change. The type can be explicitly specified when a binding is created, like this:

```
function main();
	x: boolean = false
	y: string = "Foobar"
```

The type may sometimes also be omitted, like this:

```
function main();
	x := false  # x is a boolean
	y := 5  # y is an integer
```

Type annotations
----------------

Mokka is a statically typed language. The type of a variable must be specified up front and will be checked at compile time. Our second example would still compile, since the compiler can easily determine the type of the value being bound.

The type of a variable in Mokka always proceeds a colon (`:`\):

```
foo: i32 = 5
```

We have now chosen to represent the variable `foo` as a 32-bit signed integer. [this article](https://github.com/mokka/docs/blob/master/02_concepts/02_data_types.md) describes all data types.

Mutability
----------

Bindings in Mokka are immutable by default. This means that the following code does not compile:

```
x: bool = false
x = true
```

The compiler will show the following error:

```
The immutable variable `x` is first defined here:

1 | x: bool = false

And is then re-assigned here:

2 | x = true

This is not allowed; I cannot reassign immutable variables.

Are you trying to mutate a variable? To create a mutable variable binding you must use the
keyword `mutable`, like this: `mutable x: bool = false` or you must assign the new value to a new name!
```

If you want a binding to be mutable, you can use the `mutable` keyword:

```
function main();
	mutable x: bool = false
	x = true
```

Please note that if you re-assign a mutable variable, the new value must be of the same type as the previous value. The following code would not compile:

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

Initializing bindings
---------------------

Bindings can be initialized without a value, but the binding can only be used once a value has been assigned to it. Any value that is initialized without a value must be a mutable.

```
function main();
	mutable x: bool
	
	if x;
		doStuff()
```

The above code would not compile, since no value has been assigned to `x`. Let's try assigning a value to `x`:

```
function main();
	mutable x: bool
	
	if starsAligned();
		x = true
   
	if x;
		doStuff()
```

Although the code above looks valid, it still will not compile. The compiler cannot be sure x is assigned when it gets used and will refuse to compile this code. We will fix that by assigning a value to `x` when it is initialized:

```
function main();
	mutable x: bool = false
	
	if starsAligned();
	x = true
	
	if x;
	doStuff()
```

The above code is valid and compiles!

Scope
-----

> [Please read the article about scopes in Mokka here](https://github.com/mokka/docs/blob/master/concepts/scope.md).
