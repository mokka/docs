Source code representation
==========================

Mokka source code is Unicode text encoded in UTF-8. The text is not canonicalized. This document will use the unqualified term "character" to refer to a Unicode code point in the source text.

Every code point is entirely distinct. Upper and lower case letters are treated as different characters.

### Characters

The following terms are used to denote specific Unicode character classes:

```
newline           = /* a newline character, Unicode code point U+000A */
unicode_character = /* any arbitrary Unicode character that is not a newline */
unicode_letter    = /* any arbitrary Unicode code point classified as "Letter" */
unicode_digit     = /* any arbitrary Unicode code point clssified as "Number, decimal digit" */
```
