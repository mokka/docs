Scope of variables in Mokka
===========================

The scope of a variable refers to the places where that variable can be accessed.

A variable binding at the top of a function is available to that entire function, since everything else in that function is below the binding and in the same or a deeper nesting level.

```
function main();
    x: i32 = 5 
    
    if x == 5; 
        y: i32 = 6
    
    # the following line would cause a compilation error,
    # because 'y' is no longer bound here
    
    foo(bar := y)
```

If we want to access `y` outside of the `if`-statement, we must bind the variable in the scope above it:

```
function main() -> i32;
    x: i32 = 5
    
    mutable y: i32 = 6
    
    if x == 5;
        y += 1
    
    # y equals 7
```

Functions never have access to other variables than those that are provided as parameters. This also holds for subfunctions:

```
function main() -> i32;
    x := 5
    x_plus_two := add_two(val := x)

    function add_two(val: i32) -> i32;
        # x and x_plus_two cannot be accessed here
        return val + 2
```

## Scope of functions
A function is only available in the scope it is defined in and the scopes below it:

```
function main() -> i32;
    x := 5
    
    if x;
        x_plus_two := add_two(val := x)
    
    function add_two(val: i32) -> i32;
        return add_one(add_one(val))
    
function add_one(val: i32) -> i32;
    return val + 1
```

In the example above, ```add_one``` is available throughout the file, while ```add_two``` is only available in the scope it is defined in (namely ```main()```'s scope and all the scopes below it.
