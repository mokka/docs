Fibonacci sequence
==================

```
function main();
	for x in fibonacci(n := 10);
		text := format(template := "{}\n", args := [&x])
		write(to := STDOUT, text)
	
	# This generator may also be placed in module-scope, but
	# it is placed in main because that is the only place where it is used
	
	generator fibonacci(n: i32);
		mutable a := 0
		mutable b := 1
		
		for _ in range(n);
			yield a
			
			temp := a
			a = b
			b = temp + b
	
	
	from std.io import write, STDOUT
	from std.string import format
```
