#

## [Ordinal types](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type               |Range                    |Size in bytes|
|:------------------|:-----------------------:|:-----------:|
|BYTE               |0 .. 255                 |1            |
|SHORTINT           |-128 .. 127              |1            |
|WORD               |0 .. 65535               |2            |
|SMALLINT           |-32768 .. 32767          |2            |
|CARDINAL           |0 .. 4294967295          |4            |
|LONGWORD           |0 .. 4294967295          |4            |
|DWORD              |0 .. 4294967295          |4            |
|UINT32             |0 .. 4294967295          |4            |
|INTEGER            |-2147483648 .. 2147483647|4            |
|LONGINT            |-2147483648 .. 2147483647|4            |

<br/>
## [Boolean types](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type               |Ord(True)                |Size in bytes|
|:------------------|:-----------------------:|:-----------:|
|BOOLEAN            |1                        |1            |

<br/>
## [Enumeration types](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-280003.1.1)

The enumeration type in **MP** has been implemented in its basic form, i.e.:

```delphi
Type
  Days = (monday,tuesday,wednesday,thursday,friday,
          saturday,sunday);

  Joy = (right_down = 5, right_up, right, left_down = 9, left_up, left, down = 13, up, none);
```
The enumeration type is stored only in the memory of the **MP** compiler, no information about the enumeration type fields will be stored in the result file. It is permissible to use the `ORD`, `SIZEOF` and casts on the enumeration type.

```delphi
var
   d: Days;

   d:=friday;
   writeln(ord(d));
   writeln(ord(sunday));
   writeln(sizeof(days));
   writeln(sizeof(monday));

   d:=days(20);

   case d of
    sunday: writeln('sunday');
   end;
```

Currently, the **MP** compiler does not check the correctness of enumeration types for `IF ELSE` operations.

## [Real types](https://www.freepascal.org/docs-html/ref/refsu5.html#x27-300003.1.2)

|Type               |Range                    |Size in bytes|
|:------------------|:-----------------------:|:-----------:|
|SHORTREAL (Q8.8)   |-128..127                |2            |
|REAL (Q24.8)       |-8388608..8388607        |4            |
|SINGLE (IEEE-754)  |1.5E-45 .. 3.4E38        |4            |
|FLOAT (IEEE-754)   |1.5E-45 .. 3.4E38        |4            |
|FLOAT16 (IEEE-754) |65504 .. -65504          |2            |

<br/>
Conversion of `FLOAT` `SINGLE` to `INTEGER` type is only available in the range `INTEGER`. The `INTEGER` type will not allow to present the maximum value `3.4E38` of  `FLOAT` `SINGLE` type.

## [Char types](https://www.freepascal.org/docs-html/ref/refsu6.html#x29-320003.2.1)

|Type               |Range                    |Size in bytes|
|:------------------|:-----------------------:|:-----------:|
|CHAR               |ATASCII (0 .. 255)       |1            |
|STRING             |1 .. 255                 |256          |
|PCHAR              |0 .. 65535               |2            |

<br/>
The `STRING` is represented as an array with a possible maximum size `[0..255]`. The first byte of such an array `[0]` is the string length from the range `0..255`. The actual character string begins from the byte `[1..]`.

A pointer to the `CHAR` type represents the `PCHAR` string. The terminator of the `PCHAR` string is the `#0` character.

It is allowed to use additional characters after the final apostrophe, such as `*`, `~`.

The character `*` means a string in the inverse; the tilde `~` means a string in **ANTIC** codes.

Another way to modify the output characters is to use the system variable `TextAttr`, each character output to the screen is increased by the value `TextAttr` (default = 0).

```delphi
a: string = 'Atari'*;         // a character string in the inverse
b: string = 'Spectrum'~;      // a character string in ANTIC codes
c: char = 'X'~*;              // a character in inverted ANTIC codes
```

## [Pointers](https://www.freepascal.org/docs-html/ref/refse15.html)

|Type               |Range                    |Size in bytes|
|:------------------|:-----------------------:|:-----------:|
|POINTER            |0 .. 65535               |2            |

<br/>
Indicators in **MP** can be typed and without a specific type, e.g.:

```delphi
a: ^word;         // a typed pointer to a word
b: pointer;       // an untyped pointer
```

An uninitialized pointer will most often have the address of `$0000`, you should make sure that before you use it, you will have initialized it with the address of the appropriate variable, e.g.:

```delphi
a := @tmp;         // pointer A is assigned the address of the TMP variable
```

 If you don't do this, if you run such a program on a **PC**, you may cause a memory protection fault **Access Violation**.

Increasing the pointer using `INC` increases it by the size of the type it indicates. Decreasing the pointer using `DEC` reduces it by the size of the type it indicates. If the type is unspecified, the default step for increase/decrease is `1`.

For pointers, relation operations `=`, `<>`, `<`, `<=`, `>`, `>=`, and arithmetic operations `+` and `-` are allowed.

Using a pointer, we can cast a variable to another type:

```delphi
var
   s: single;
   d: cardinal;

begin

 s := 3.14;

 d:=PCardinal(@s)^;	// d = $4048F5C3

end;
```

## [Static arrays](https://www.freepascal.org/docs-html/ref/refsu14.html#x38-500003.3.1)

Tables in **MP** are only static, one-dimensional or two-dimensional with an initial index equal to `0`, e.g:

```delphi
var tb: array [0..100] of word;
var tb2: array [0..15, 0..31] of Boolean;
```

For an initial index other than zero, an error **Error Array lower bound is not zero** is generated.

In the memory the array is represented by the pointer `POINTER`, the pointer is the address of the array in memory (WORD). The quickest way to refer to the table from the assembler level is to use the prefix `ADR`, e.g.:

    asm
    { lda adr.tb,y   ; direct reference to the TB array
      lda tb         ; reference to the TB array pointer
    };

The compiler generates code for the arrays depending on their declaration:

* when the number of bytes does not exceed 256 bytes

```delphi
array [0..255] of byte
array [0..127] of word
array [0..63] of cardinal
```

When the number of bytes occupied by the array does not exceed 256 bytes, the fastest code referring directly to the address of the array (prefix `ADR.`) is generated without the pointer. It is not possible to change the address for such an array.

    ldy #118
    lda adr.tb,y

* when the number of elements of an array is `1`

```delphi
array [0..0] of type
```

When the number of elements of an array is `1` it is treated specifically. The code generated refers to the array through the pointer. It is possible to set a new address for such a table.

    lda TB
    add I
    tay
    lda TB+1
    adc #$00
    sta bp+1
    lda (bp),y

* when the number of bytes exceeds 256 bytes

```delphi
array [0..255+1] of byte
array [0..127+1] of word
array [0..63+1] of cardinal
```

When the number of bytes occupied by the array exceeds 256 bytes, the generated code refers to the array via an pointer. When the number of bytes occupied by the array exceeds 256 bytes, the generated code refers to the array through a pointer.

    lda TB
    add I
    tay
    lda TB+1
    adc #$00
    sta bp+1
    lda (bp),y

### Array initialization

Initialization of an array `CONST` or `VAR` follows the same procedure. After the word specifying the data type of the array, we place the `=` character and the subsequent elements of the array between the round brackets `( val0, val1, ... )` :
```
const
   PBox : array [0..1] of word = (12,10);

var
   PBox : array [0..1] of word = (12,10);
```
In the case of a two-dimensional array:
```
   PBox : array [0..1, 0..1] of word = ( (12,10) , (1,6) );
```
We can instantiate an array of type `CHAR` by `STRING`:
```
   PBox : array [0..4] of char = 'Hello';
```
It is possible to initialize an array without specifying its size, we then use square brackets `[ ]` :
```
   PBox : array of char = ['H', 'e', 'l', 'l', 'o'];

   PBox : array of word = [1,2,3,4,5];
	
   PBox : array of char = 'Hello';        // bez nawiasów [ ]
```
It is possible to instantiate an array of type `BYTE` with a binary file, we then use the compiler directive `{$bin2csv filename}` :
```
   tb: array of byte = [ {$bin2csv filename} ];

   tb: array [0..11] of byte = ( 1,2,3, {$bin2csv filename} );
```


## [Record types](https://www.freepascal.org/docs-html/ref/refsu15.html#x39-550003.3.2)

In the memory the record is represented by a pointer `POINTER`.

    type
        TPoint = record x,y: byte end;
    var px: TPoint;

By default, records in **MP** are of type `PACKED`. The total size of the record fields is limited to 256 bytes.

If you want to maintain **FPC** compatibility, you should additionally precede the word `record` with the word `packed`.

Without this, the size of the memory that the record takes varies, it occupies less memory on **Atari XE/XL**, potentially several bytes more on the **PC**.

```delphi
type
    TPoint = packed record x,y: byte end;

    var px: TPoint;
```

Access to record fields from the assembly:

    mwa px bp2
    ldy #px.x-DATAORIGIN
    lda (bp2),y


### Table of records

**MP** only supports arrays of record pointers.

```Delphi
    type
        TPoint = record x,y: byte end;    

    var 
        tab: array [0..3] of ^TPoint;
```

Such an array must be instantiated with the corresponding record addresses, by default all fields of such an array are zeroed at the beginning.

The first way to instantiate an array of record indicators:
```Delphi
    var
       a1,a2,a3,a4: TPoint;       

    begin
     tab[0] := @a1;
     tab[1] := @a2;
     tab[2] := @a3;
     tab[3] := @a4;   
    end.
```
Second way:
```Delphi
    begin
     GetMem(tab[0], sizeof(TPoint));
     GetMem(tab[1], sizeof(TPoint));
     GetMem(tab[2], sizeof(TPoint));
     GetMem(tab[3], sizeof(TPoint));
    end.
```
Access record fields from such an array:
```Delphi
  writeln(tab[1].x);
  writeln(tab[1].y);
```

## [Object types](https://www.freepascal.org/docs-html/ref/refse28.html#x60-780005.1)

Objects are records with additional methods. In the memory, the object is represented by a pointer `POINTER`.

```delphi
type
    TRMT = Object

    player: pointer;
    modul: pointer;

    procedure Init(a: byte); assembler;
    procedure Play; assembler;
    procedure Stop; assembler;

    end;
```

It is possible to use the `CONSTRUCTOR` and `DESTRUCTOR` procedures in objects. Such procedures can only be called manually.  


## [Procedural](https://www.freepascal.org/docs-html/ref/refse17.html)

In memory, procedural type variables are represented by the `POINTER` type.

```delphi
type
    tprc = procedure (a: byte; c: word);
    tfun = function (a:smallint; x: single): byte;
 
var
    fn: function (a,b,c: byte): word;
```

For the procedural type, procedures/functions with arguments require the `STDCALL` modifier, which will force the use of the program stack.

```delphi
var
   fn: function (a,b: word): word;

function test(a,b,c,d: word): word; stdcall;
begin

end;

begin

fn := @test;

fn(1,2);

end;
```

For procedures with arguments instead of the `STDCALL` modifier, the `REGISTER` modifier is allowed, provided there are up to three arguments.

```delphi
var
   prc: procedure (a,b: word);

procedure test(a,b,c: cardinal); register;
begin

// a -> EDX
// b -> ECX
// c -> EAX
 
end;

begin

prc := @test;

prc(3,6);

end;
```

When no arguments are passed to the procedure/function, the use of modifier is not necessary.


## [File types](https://www.freepascal.org/docs-html/ref/refsu17.html#x41-590003.3.4)

The `FILE` type represents the file handle and defines the record size.

```delphi
type
  ftype = array [0..63] of cardinal;

var
  f: file;               // default record =128 bytes
  f: file of byte;       // 1 byte record
  f: file of ftype;      // 256 byte record (ftype = 64 * 4)
```

In the **XE/XL** memory, the FILE holder is represented by a pointer `POINTER` to an array of structure (size 12 bytes):

```
.struct s@file
pfname   .word      ; pointer to string with filename
record   .word      ; record size
chanel   .byte      ; channel *$10
eof      .byte      ; EOF status
buffer   .word      ; load/write buffer
nrecord  .word      ; number of records for load/write
numread  .word      ; pointer to variable, length of loaded data
.ends
```

For procedures and functions, the `FILE `type can only be passed as a variable `VAR`.


## [Untyped](https://www.freepascal.org/docs-html/ref/refsu70.html)

```Delphi
 procedure Something (var Data);
 procedure Something (const Data);
```

Failure to specify the type of the parameter means that only the address of the parameter without the type designation will be passed to the procedure/function.

This is equivalent to the following C/C++ declaration:

```Delphi
 void Something(void* Data);
```

Inside a procedure/function with an unsigned parameter, if an unsigned parameter is used in an expression or a value must be assigned to it, always use type casting.


    var x: word;
 
    procedure test(var a);
    begin
 
      writeln(PWord(@a)^);  // = 95

      PWord(@a)^ := 11;
 
    end;
 
    begin
    
      x:=95;
 
      test(x);              // = 11
 
    end.
 