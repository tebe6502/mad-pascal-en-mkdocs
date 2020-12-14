#

## [Ordinary constants](https://www.freepascal.org/docs-html/ref/refse9.html)

The character `=` is used for the CONST constant declarations. The use of operators:

`+` `-` `*` `/` `not` `and` `or` `div` `mod` `ord` `chr` `sizeof` `pi`


```delphi
const
  e = 2.7182818;       { Real type constant }
  f : single = 3.14;   { Single type constant }
  a = 2;               { Ordinal BYTE type constant }
  c = '4';             { Character type constant }
  s = 'atari';         { String type constant }
  sc = chr(32);
  ls = SizeOf(cardinal);

  x: word = 5;         { forcing the type of constant }
```