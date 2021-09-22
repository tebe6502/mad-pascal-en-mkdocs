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

## [VOLATILE](https://pl.wikipedia.org/wiki/Zmienna_ulotna)

The `VOLATILE` modifier marks a variable as so-called transient. Marking it as `VOLATILE` disables optimization of the resulting code for that variable,
This is useful for hardware registers whose values may change with each successive read.

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
> _The same 16 byte area of the zero page is used by the compiler allocating its `EDX` `ECX` `EAX` registers there, so using the `REGISTER` modifier is not possible when a procedure or function also uses `REGISTER`._


```delphi
procedure test(a,b,c: integer); register;
```