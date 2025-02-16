#

## [VAR](https://www.freepascal.org/docs-html/ref/refse22.html#x53-730004.2)

The word `VAR` begins the variable declaration section.

```delphi
var
    label: type;
    label: type = value;
```

```delphi
var
    a: word;
    b: byte = 1;
    c: Boolean = true;

    s: string = 'Atari';

    tb: array [0..3] of byte = (0,1,2,3);
```

## [VOLATILE](https://en.wikipedia.org/wiki/Volatile_(computer_programming))

The `VOLATILE` modifier marks a variable as so-called volatile. Marking it as `VOLATILE` disables optimization of the resulting code for that variable. Every read access to the variable will read from the memory location and will not re-use values that were already read by previous instructions. This is useful for hardware registers whose values may change with each successive read and for variables that are modified in parallel by other code the is not known to the compiler, for example by interrupt handlers.

```delphi
var
  [volatile] joy   : byte absolute $ff08;
  pio              : byte absolute $fd30;

begin
  repeat
    pio := $ff;
    joy := 2;
    if (joy xor $ff) = 1 then writeln('UP');
  until false;
end.
```

## [ABSOLUTE]()

The `ABSOLUTE` modifier allows you to set the address in memory for `VAR` variables.

```delphi
var
   a: byte absolute $0600;
   tb: array [0..255] of byte absolute $a000;

   tab: array [0..3] of byte;
   v: integer absolute tab;

   procedure test(var buf);
   var ptr: PByte absolute buf;
```

## [REGISTER]()

The `REGISTER` modifier sets the memory address for `VAR` variables on the zero page (a maximum of 16 bytes can be allocated).

```delphi
var
   a: byte register;
   c: integer register;
```

> **WARNING:**  
> _The same 16-byte area of the zero page is used by the compiler allocating its `EDX` `ECX` `EAX` registers there, so using the `REGISTER` modifier is not possible when a procedure or function also uses `REGISTER`._


```delphi
procedure test(a,b,c: integer); register;
```

## [Initialization](https://www.freepascal.org/docs-html/ref/refse24.html)

**Mad Pascal** initializes all global and local variables once upon program start to the equivalent of zero or the explicitly specifed values.
Note that this is different from the **FPC** behavior where only global variables are guranteed to be initialized.
Because initialization only takes place upon program start and because it is not guranteed in **FPC** you should always explicitly assign values to local variables when a procedure or functions is entered.
The syntax for specifying the initialization values in `CONST` and `VAR` declarations is identical.
After the word specifying the data type, place the `=` character and the initial value.

### Array initialization

After the word specifying the data type of the array, place the `=` character and the subsequent elements of the array between the round brackets `( val0, val1, ... )` :
```
const
   pbox : array [0..1] of word = (12,10);

var
   pbox : array [0..1] of word = (12,10);
```
In the case of a two-dimensional array:
```
   pbox : array [0..1, 0..1] of word = ( (12,10) , (1,6) );
```
We can instantiate an array of type `CHAR` by `STRING`:
```
   pbox : array [0..4] of char = 'Hello';
```
It is possible to initialize an array without specifying its size using square brackets `[ ]` :
```
   pbox : array of char = ['H', 'e', 'l', 'l', 'o'];

   pbox : array of word = [1,2,3,4,5];
	
   pbox : array of char = 'Hello';        // char arry without square brackets [ ]
```
It is possible to initialize an array of type `BYTE` from a binary file, using the directive `{$bin2csv filename}` :
```
   tb: array of byte = [ {$bin2csv filename} ];

   tb: array [0..11] of byte = ( 1,2,3, {$bin2csv filename} );
```