Scope of variables in Mokka
===========================

The scope of a variable refers to the places where that variable can be accessed. Since Mokka uses indentation to define code blocks, the scope of a variable can very easily be recognized.

A variable binding at the top of a function is available to that entire function, since everything else in that function is below the binding and in the same or a deeper nesting level.

```
function main();
    x: int = 5      
                    
    if x == 5;       
        y: int = 6
        
        print y
    
    # 'y' is no longer bound here
    print x
```

If we want to access `y` outside of the `if`-statement, we must bind the variable before it:

```
function main();
    x: int = 5      
            
    mutable y: int = 6;
    if x == 5;
        print y // 6
        
        y += 1
    
    print y // 7
    print x
```
