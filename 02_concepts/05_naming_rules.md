Naming rules in Mokka
=====================

In contrast to most other languages, naming conventions are enforced by the compiler of Mokka. In other words, naming is part of the syntax.

This is similar to how written natural languages use capitalization as part of their syntax. For example, the capitalization of nouns in the German language.

The rules for names are as follows:

-	`snake_case` for local bindings
-	`lowerCamelCase` for functions and generators
-	`UpperCamelCase` for structures

Grammar
-------

### Bindings

Binding names must consist of only lowercase letters, numbers and underscores. The name of a binding must start with a lowercase letter.

### Functions and generators

A function or generator name must consist of only uppercase and lowercase letters. It must also start with a lowercase letter.

### Structures

The name of a structure must only consist of uppercase and lowercase letters. It must also start with an uppercase letter.

Examples
--------

The following code does not compile:

```
function main();
	x := AddTwo(val := 3)


function AddTwo(val: i32) -> i32;
	return val + 2
```

The function `AddTwo` has an invalid name, since it does not start with a lowercase letter.
