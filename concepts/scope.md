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
function main();
    x: i32 = 5
    
    mutable y: i32 = 6
    
    if x == 5;
        y += 1
    
    # y equals 7
```

Functions never have access to other variables than those that are provided as parameters. This also holds for subfunctions:

```
function main();
    x := 5
    x_plus_two := add_two(val := x)

    function add_two(val: i32);
        # x and x_plus_two cannot be accessed here
        return x + 2
```
