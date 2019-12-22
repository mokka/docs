Control flow statements in Mokka
================================

Whether or not to execute some piece of code based on a condition or run code while a condition is true are some of the fundamental building blocks of computer programming.

## `if`
An `if` statement evaluates a condition and executes the block of code immediately proceding it, based on that condition.

```
function main();
  guess: int = 4
  
  if guess > 3;
    write(to := STDOUT, guess)
```

Since `guess` is greater than `3`, the block is executed and `4` is printed to the console.

### `else`
An `else` statement always directly proceeds an `if` statement and gets executed if the condition in the preceeding `if` statement evaluates to `false`.

```
function main();
  guess: int = 4
  
  if guess > 5;
    write(to := STDOUT, guess)
  else;
    write(to := STDOUT, "Incorrect guess")
```

### `else if`
An `else if` statement always directly proceeds an `if` or `else if` statement and gets executed if the condition in the preceeding `if` or `else if` statements evaluate to `false` and its condition evaluates to `true`.

```
function main();
  guess: int = 4
  
  if guess > 5;
    write(to := STDOUT, guess)
  else if guess > 4;
    write(to := STDOUT, "Incorrect guess")
```

Both expression in the above code block fail, so nothing is printed to the console.
