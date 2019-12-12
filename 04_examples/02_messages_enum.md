Messages enumeration
====================

```
function main();
    counter := Counter { value := 0 }
    message := CounterMessage.Increase { by := 5 }
    inverse := invert(&message)

    # Add 5 to the counter
    update(&mutable counter, message)

    # Revert adding 5
    update(&mutable counter, inverse)

    # counter.value is now 0 again


function invert(message: &CounterMessage) -> CounterMessage;
    match message;
        CounterMessage.Increase by;
	    return CounterMessage.Decrease { by }

	CounterMessage.Decrease by;
	    return CounterMessage.Increase { by }


function update(counter: &mutable Counter, message: CounterMessage);
    match message;
        CounterMessage.Increase by;
	    counter.value += by

	CounterMessage.Decrease by;
	    counter.value -= by


enumeration CounterMessage;
    Increase;
        by: i64

    Decrease;
        by: i64


structure Counter;
    value: i64
```