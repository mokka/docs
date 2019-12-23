Vectors
=======

```
function main();
    a := Vector { x := 5.0, y := -1.0 }
    b := Vector { x := 2.1, y := 4.21 }
    c := Vector { x := -2.52, y := -2.0 }

    d := a*b + c

    line := format(
	template := "a = {}, b = {}, c = {}, d = {}\n",
	args := [&a, &b, &c, &d]
    )
    write(to := STDOUT, text := line)


from std.io import STDOUT
from std.string import format


generator __format__(a: &Vector) -> can __format__;
    yield "("
    yield a.x
    yield ", "
    yield a.y
    yield ")"


function __multiply__(left: &Vector, right: &Vector) -> Vector;
    x := left.x * right.x
    y := left.y * right.y

    return Vector { x, y }


function __subtract__(left: &Vector, right: &Vector) -> Vector;
    return left + (-right)


function __add__(left: &Vector, right: &Vector) -> Vector;
    x := left.x + right.x
    y := left.y + right.y

    return Vector { x, y }


function __negate__(a: &Vector) -> Vector;
    return Vector {
        x := -a.x,
        y := -a.y
    }


structure Vector;
    x: f32
    y: f32
```
