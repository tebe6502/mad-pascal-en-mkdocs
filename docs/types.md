#

## [ordinal](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Range                    |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|BYTE    |0 .. 255                 |1            |
|SHORTINT|-128 .. 127              |1            |
|WORD    |0 .. 65535               |2            |
|SMALLINT|-32768 .. 32767          |2            |
|CARDINAL|0 .. 4294967295          |4            |
|LONGWORD|0 .. 4294967295          |4            |
|DWORD   |0 .. 4294967295          |4            |
|UINT32  |0 .. 4294967295          |4            |
|INTEGER |-2147483648 .. 2147483647|4            |
|LONGINT |-2147483648 .. 2147483647|4            |

---

## [boolean](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Ord(True)                |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|BYTE    |1                        |1            |

---

## [enumeration](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-280003.1.1)

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

---

## [real](https://www.freepascal.org/docs-html/ref/refsu5.html#x27-300003.1.2)

|Type             |Range                   |Size in bytes|
|:----------------|:----------------------:|:-----------:|
|SHORTREAL (Q8.8) |-128..127               |2            |
|REAL (Q24.8)     |-8388607..8388608       |4            |
|SINGLE (IEEE-754)|1.5E-45 .. 3.4E38       |4            |
|FLOAT (IEEE-754) |1.5E-45 .. 3.4E38       |4            |

Conversion of `FLOAT` `SINGLE` to `INTEGER` type is only available in the range `NTEGER`. The `INTEGER` type will not allow to present the maximum value of `3.4E38` of  `FLOAT` `SINGLE` type.

---

## [char](https://www.freepascal.org/docs-html/ref/refsu6.html#x29-320003.2.1)

|Type    |Range                    |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|CHAR    |ATASCII (0 .. 255)       |1            |
|STRING  |1 .. 255                 |256          |
|PCHAR   |0 .. 65535               |2            |

 The `STRING` is represented as an array with a possible maximum size `[0..255]`. The first byte of such an array `[0]` is the string length from the range `0..255`. The actual character string begins from the byte `[1..]`.

A pointer to the `CHAR` type represents the `PCHAR` string. The terminator of the `PCHAR` string is the `#0` character.

It is allowed to use additional characters after the final apostrophe, such as `*`, `~`. The character `*` means a string in the inverse; the tilde `~` means a string in **ANTIC** codes.

Another way to modify the output characters is to use the system variable `TextAttr`, each character output to the screen is increased by the value `TextAttr` (default = 0).

```delphi
a: string = 'Atari'*;         // a character string in the inverse
b: string = 'Spectrum'~;      // a character string in ANTIC codes
c: char = 'X'~*;              // a character in inverted ANTIC codes
```

---

## [pointers](https://www.freepascal.org/docs-html/ref/refse15.html)

|Type    |Range                    |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|POINTER |0 .. 65535               |2            |

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

---

## [arrays](https://www.freepascal.org/docs-html/ref/refsu14.html#x38-500003.3.1)

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

---

## [records](https://www.freepascal.org/docs-html/ref/refsu15.html#x39-550003.3.2)

In the memory the record is represented by a pointer `POINTER`.

    type
        TPoint = record x,y: byte end;
    var px: TPoint;

By default, records in **MP** are of type `PACKED`.

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

---

## [objects](https://www.freepascal.org/docs-html/ref/refse28.html#x60-780005.1)

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

---

## [files](https://www.freepascal.org/docs-html/ref/refsu17.html#x41-590003.3.4)

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

