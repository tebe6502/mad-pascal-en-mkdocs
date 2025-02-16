#

## [Ordinary constants](https://www.freepascal.org/docs-html/ref/refse9.html)

The character `=` is used for the CONST constant declarations. The use of operators:

`+` `-` `*` `/` `not` `and` `or` `div` `mod` `ord` `chr` `sizeof` `pi`

is possible in the constant expression to compute the constant value at compile time.
Ordinary constants have a variable type and the compiler will convert them to the required type at when they are used.

```delphi
const
  e = 2.7182818;       { Real type constant }
  a = 2;               { Ordinal BYTE type constant }
  c = '4';             { Character type constant }
  s = 'atari';         { String type constant }
  sc = chr(32);
  ls = SizeOf(cardinal);
```

## [Typed constants](https://www.freepascal.org/docs-html/ref/refse10.html)

You can also specify the fixed type of a constant explicitly.

```delphi
const
  f : single = 3.14;
  x : word = 5;
  pbox : array [0..1] of word = (12,10);
```

The syntax for specifying the initialization in `CONST` arrays is the same as `VAR` arrays. See section [Initialization](variables.md#array-initialization) for details.