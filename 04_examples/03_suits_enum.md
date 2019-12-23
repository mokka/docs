Card suits
==========

```
function main();
    suit := CardSuit.Clubs

    match suit;
	CardSuit.Clubs;
	    write(to := STDOUT, text := "The suit is clubs")
	CardSuit.Diamonds;
	    write(to := STDOUT, text := "The suit is diamonds")
	CardSuit.Hearts;
	    write(to := STDOUT, text := "The suit is hearts")
	CardSuit.Spades;
	    write(to := STDOUT, text := "The suit is spades")
	*;
	    write(to := STDOUT, text := "I do not know this suit")


from std.io import write, STDOUT


enumeration CardSuit;
    Clubs
    Diamonds
    Hearts
    Spades
```
