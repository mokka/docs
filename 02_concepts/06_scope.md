Scope of bindings in Mokka
==========================

The scope of a binding refers to the places where that binding can be accessed.

A binding at the top of a function is available in that entire function, since everything else in that function is below the binding and in the same or a deeper nesting level.

```
function main();
	x := 5

	if x == 5;
		y := 6
	
	# the following line causes a compilation error,
	# because 'y' is no longer bound here
	
	foo(bar := y)
```

If we want to access `y` outside of the `if`-statement, we must bind the variable in the scope above it:

```
function main();
	mutable y: i32 = 6
	x := 5

	if x == 5;
		y += 1

	# y equals 7
```

Functions never have access to other variables than those that are provided as parameters. This also holds for subfunctions:

```
function main();
	x := 5
	x_plus_two := addTwo(val := x)

	function addTwo(val: i32) -> i32;
		# x and x_plus_two cannot be accessed here
		return val + 2
```

Scope of functions
------------------

A function is only available in the scope it is defined in and the scopes below it:

```
function main();
	x := 5
	x_plus_two := addTwo(val := x)

	function addTwo(val: i32) -> i32;
		return addOne(addOne(val))
    
function addOne(val: i32) -> i32;
    return val + 1
```

In the example above, `addOne` is available throughout the file, while `addTwo` is only available in the scope it is defined in (namely `main()`'s scope and all the scopes below it.
