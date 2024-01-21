#

In the **Mad-Pascal** `LIB` there are basic `UNIT` modules needed for compilation, such as `SYSTEM` `CRT` `GRAPH` `SYSUTILS` `MATH` `DOS`. The module is selected by the `USES` instructions, e.g.:

    uses crt, sysutils;

The 'SYSTEM' module is added to the 'USES' list by default and compiled first.

## [SYSTEM](http://mads.atari8.info/library/doc/system.html)

### Constants

```delphi
M_PI_2           = 6.283285;  // pi * 2
D_PI_2           = 1.570796;  // pi / 2
D_PI_180         = 0.017453;  // pi / 180

mGTIA            = 0;
mVBXE            = $80;
WINDOW           = $10;
NARROW           = $20;


VBXE_XDLADR      = $0000;     // XDLIST
VBXE_MAPADR      = $1000;     // COLOR MAP ADDRESS
VBXE_BCBADR      = $0100;     // BLITTER LIST ADDRESS
VBXE_OVRADR      = $5000;     // OVERLAY ADDRESS
VBXE_WINDOW      = $B000;     // 4K WINDOW $B000..$BFFF

iDLI             = 0;
iVBL             = 1;

CH_DELCHR        = $FE;
CH_ENTER         = $9B;
CH_ESC           = $1B;
CH_CURS_UP       = 28;
CH_CURS_DOWN     = 29;
CH_CURS_LEFT     = 30;
CH_CURS_RIGHT    = 31;

CH_TAB           = $7F;
CH_EOL           = $9B;
CH_CLR           = $7D;
CH_BEL           = $FD;
CH_DEL           = $7E;
CH_DELLINE       = $9C;
CH_INSLINE       = $9D;

COLOR_BLACK      = $00;
COLOR_WHITE      = $0e;
COLOR_RED        = $32;
COLOR_CYAN       = $96;
COLOR_VIOLET     = $68;
COLOR_GREEN      = $c4;
COLOR_BLUE       = $74;
COLOR_YELLOW     = $ee;
COLOR_ORANGE     = $4a;
COLOR_BROWN      = $e4;
COLOR_LIGHTRED   = $3c;
COLOR_GRAY1      = $04;
COLOR_GRAY2      = $06;
COLOR_GRAY3      = $0a;
COLOR_LIGHTGREEN = $cc;
COLOR_LIGHTBLUE  = $7c;
```

### Types

#### `TPoint`

```delphi
    TPoint = record x,y: SmallInt end;
```

Definition of coordinates (X, Y).

---

#### `TRect`

```delphi
    TRect = record left, top, right, bottom: smallint end;
```

Definition of the position and size of a quadrangle with parameters (left, top) - upper-left  corner, (right, bottom) - lower-right corner.

---

#### `TString`

```delphi
    TString = string[32];
```

Definition of a short character string used to pass file names, etc.

---

### Variables

#### `IOResult`

```delphi
    IOResult: byte;
```

Variable stores the last I/O operation error. [Error codes I/O](http://atariki.krap.pl/index.php/Kody_statusowe_Atari_OS).

---

#### `ScreenWidth`

```delphi
    ScreenWidth: word = 40
```

Variable storing the current width of the screen. By default, this is a value of 40 for the editor screen.

```delphi
    ScreenHeight: word = 24;
```

---

#### `ScreenHeight`

Variable storing the current height of the screen. By default, this is a value of 24 for the editor screen.

### Procedures and functions

```delphi
Abs                ArcTan              Assign             BinStr            Concat
Blockread          Blockwrite          Chr                Cos               Close
Dec                DeleteFile          DPeek              DPoke             Eof
Exit               Exp                 FilePos            FileSize          FillChar
Frac               GetIntVec           Halt               Hi                HexStr
Inc                Ln                  Lo                 LowerCase         Move
OctStr             Odd                 Ord                ParamCount        ParamStr
Pause              Peek                Point              PointsEqual       Poke
Pred               Random              ReadConfig         ReadSecto         Rect
RenameFile         Reset               Rewrite            Round             Seek
SetLength          SetIntVec           Sin                Succ              Space
SizeOf             Str                 StringOfChar       Sqr               Sqrt
Trunc              UpCase              Val                WriteSector
```

#### `Abs`

```delphi
    function Abs(x: real): real;
    function Abs(x: integer): integer;
```

A function that calculates the absolute value of the given number (ang. **Absolute value**). The absolute value of a non-negative number is the same number, and the negative number is the opposite. The function, when given its total argument, returns the result of the total type.

---

#### `ArcTan`

```delphi
    function ArcTan(x: real): real;
```

Function (arcus tangents) returns the value of the angle whose tangent is `x`.

---

#### `Assign`

```delphi
    procedure Assign(var F:File; FileName:string)
```

The procedure assigns a file variable `F` with a name `FileName`. To be able to refer to a file, you should always first use the `Assign` procedure. For further operations, the file is identified by the file variable, not the name.

---

#### `BinStr`

```delphi
    function BinStr(Value: cardinal; Digits: byte): TString;
```

Function returns character string with binary representation of value `Value`. `Digits` specifies the length of the string, which can number a maximum of 32 characters.

---

#### `Concat`

```delphi
    function Concat(a,b: string): string; assembler
    function Concat(a: string; b: char): string; assembler;
    function Concat(a: char; b: string): string; assembler;
    function Concat(a,b: char): string;
```

The function combines two text strings into a new character string.

---

#### `Blockread`

```delphi
    procedure BlockRead(var f: file; var Buf; Count: word; var Result: word);
```

The procedure reads from file `f` into variable `Buf`, not more than `Count` bytes, and places the number of actual bytes read into variable `Result` (which may be smaller than expected, for example, due to the actual length of the file).

---

#### `Blockwrite`

```delphi
    procedure BlockWrite(var f: file; var Buf; Count: word; var Result: word);
```

The procedure saves to a file from the variable `Buf` not more than `Count` bytes.

---

#### `Chr`

```delphi
    Chr(65); // Returns the char 'A'
    Chr(90); // Returns the char 'Z'
    Chr(32); // Returns the char ' '
```

```delphi
    Writeln(#65);       // Character 'A'
    Writeln(#65#32#65); // Will write 'A Z'
```

Function returns the character `Char` with the corresponding **ATASCII** code specified in the parameter. Alternatively with the function `Chr`, if you want to get the right character, we can use its **ATASCII** code with a preceding `#`.

---

#### `Cos`

```delphi
    function Cos(x: real): real;
```

Cosinus angle, `x` in Radians.

---

#### `Close`

```delphi
    procedure Close(var f: file);
```

The procedure for closing the open file of any type. Each file open with the 'Reset' or 'Rewrite' should be closed with procedure 'Close'.

---

#### `Dec`

```delphi
    procedure Dec(var X [, N: int]);
```

The procedure reduces the value of the parameter `X`...`1` or the parameter value `N`...`X`. Parameter can be the type `CHAR` `BYTE` `WORD` `CARDINAL`. The `Dec` procedure generates optimal code, it is recommended for use in loops instead of the subtraction operator '-'.

```delphi
    dec(tmp);
    dec(tmp[2]);
```

---

#### `DeleteFile`

```delphi
    function DeleteFile(FileName: string): Boolean;
```

The function allows you to delete the file from the disk called `Filename`, returns `TRUE` when the operation was successful, `FALSE` in the event of an error (most often due to the protection against saving or erroneous file name).

---

#### `DPeek`

```delphi
    function DPeek(a: word): word;
```

This function returns the word from address `a`.

---

#### `DPoke`

```delphi
    procedure DPoke(a: word; value: word);
```

This procedure saves the word `value` to address `a`.

---

#### `Eof`

```delphi
    function Eof(var f: file): Boolean;
```

The function returns the logical value `True` if the end of the file has been reached.

---

#### `Exit`

Calling of the procedure `Exit` it immediately leaves the program block where the call occurred. It can be used to leave the loop, exit the **procedure/function** or the main program.

---

#### `Exp`

```delphi
    function Exp(x: real): real;
```

Function increasing the number e (=2.71) to the power given by the argument `x`.

---

#### `FilePos`

```delphi
    function FilePos(var f: file): cardinal;
```

The function returns the current position of the file. The file cannot be textual and must be open (e.g. command `Reset`). The Bits `0..15` returned value is the number of the disk sector, bits `16..23` position in the sector `[0..255]`. This is the equivalent of instructions `NOTE`.

---

#### `FileSize`

```delphi
    function FileSize(var f: file): cardinal;
```

The function returns the length of the file in bytes (**Sparta DOS X**). The file cannot be textual and must be open (e.g. command `Reset`).

---

#### `FillChar`

```delphi
    procedure FillChar(x: pointer; count: word; value: char);
```

The procedure fills in the buffer specified in the parameter `x` with identical chars or bytes. Parameter `value` specifies the data, by `count` - the amount of data that will be assigned to the buffer.

```delphi
    var
      Buffer : array[0..100] of Char;
    begin
      FillChar(Buffer, SizeOf(Buffer), 'A');
    end.
```

---

#### `Frac`

```delphi
    function Frac(x: real): real;
```

Returns the fractional part of the number `x` in the real form.

---

#### `GetIntVec`

```delphi
    procedure GetIntVec(intno: byte; var vector: pointer);
```

The procedure reads the address of the interrupt vector according to the **INTNO** code. Currently, the permissible codes are: `iDLI` Display List interrupt, `iVBL` Vertical Blank interrupt.

---

#### `Halt`

```delphi
    procedure halt;
```

Calling causes an immediate exit from the program. You can (optionally) enter an error code, in the case of MP it is ignored.


---

#### `Hi`

```delphi
    function Hi(x): byte
```

Function returning the high-byte of parameter `x`.

---

#### `HexStr`

```delphi
    function HexStr(Value: cardinal; Digits: byte): TString;
```

The function returns the character string with the hexadecimal representation of `Value`. `Digits` determines the length of the string, which can have a maximum of 32 characters.

---

#### ` Inc`

```delphi
    Inc procedure Inc(var X [, N: int]);
```

The procedure increases the value of the parameter `X` by `1` or by the value of parameter `N`. The value of the `X` parameter can be the type `CHAR` `BYTE` `WORD` `CARDINAL`. The `Inc` procedure generates optimal code, so it is recommended for use in loops instead of adding `+`.


```delphi
    inc(tmp);
    inc(tmp[2]);
```

---

#### `Int`

```delphi
    function Int(x: real): real;
```

The function returns the total part of the argument that is a real number.

---

#### `Ln`

```delphi
    function Ln(x: real): real;
```

Natural logarithm function (based on e) from the given number. The argument of the function must be ** positive **!

---

#### `Lo`

```delphi
    function Lo(x): byte;
```

Function returning the low-byte of parameter `x`.

---

#### `LowerCase`

```delphi
    function LowerCase(a: char): char;
```

Function changing the characters 'A'..'Z' to the corresponding lowercase characters 'a'..'z'.

---

#### `Move`

```delphi
    procedure Move(source, dest: pointer; count: word);
```

The procedure is used to copy data from the source, `Source`, to the specified buffer, `Dest`. The amount of copied data is determined by the `Count` parameter.

---

#### `OctStr`

```delphi
    function OctStr(Value: cardinal; Digits: byte): TString;
```

The function returns the character string with the octal representation of `value`. `Digits` determines the length of the string, which can have a maximum of 32 characters.

---

#### `Odd`

```delphi
    function Odd(x: cardinal): Boolean;
    function Odd(x: integer): Boolean;
```

The function returns the value of `True` if the number specified in the `X` parameter is odd, `false` if it is even.

---

#### `Ord`

```delphi
    function Ord(X);
```

This function works inversely to `Chr`. From the given character parameter, its **ATASCII** value is returned.

```delphi
    Ord('A'); // Zwraca 65
    Ord('Z'); // Zwraca 90
    Ord(' '); // Zwraca 32
```

---

#### `ParamCount`

```delphi
    function ParamCount: byte;
```

The function returns the number of available arguments (**Sparta Dos X**, **BWDos**), i.e. the maximum index for the `ParamStr` procedure. `ParamCount` determines the number of parameters transferred to the program from the command line.

---

#### `ParamStr`

```delphi
    function ParamStr(Index: byte): TString;
```

The function returns the program parameters (**Sparta Dos X**, **BWDos**). `Index` is the parameter number, i.e. the sequence of characters separated by a space.

If we run the `TEST.EXE` program in this way:


```delphi
    TEST.EXE parametr1 parametr2 parametr3
```

To get a `parameter3`, enter `Index=3`, and to get the `parameter1` you need `Index=1`. `Index=0` is a special argument, then the function returns the drive from which the program was launched, e.g.`D1:`.

---

#### `Pause`

```delphi
    procedure Pause;
    procedure Pause(n: word);
```

The procedure stops the program operation on `N * 1.50` seconds.

---

#### `Peek`

```delphi
    function Peek(a: word): byte;
```

The function returns a byte from the address `a`.

---

#### `Point`

```delphi
    function Point(AX, AY: smallint): TPoint;
```

Function uses the parameters `AX` and `AY` to create a `TPOINT` record.

---

#### `PointsEqual`

```delphi
    function PointsEqual(const P1, P2: TPoint): Boolean;
```

The function checks whether the coordinate values specified in the parameters `P1` and `P2` are equal. In this case, the function returns the value of `True`.

---

#### `Poke`

```delphi
    procedure Poke(a: word; value: byte);
```

The procedure writes `value` into address `a`.

---

#### `Pred`

```delphi
    function Pred(X: TOrdinal): TOrdinal;
```

Predecessor of the `X` element.

---

#### `Random`

```delphi
    function Random: Real; assembler;
```

The function returns random value between `<0..1>`.

```delphi
    function Random(range: byte): byte; assembler;
```

The function returns random value between `<0 .. range-1>`, in the case of Range=0 returns the random value from between `<0 .. 255>`.

```delphi
    function Random(range: smallint): smallint;
```

The function returns a random value between `<0 .. range-1>`.

---

#### `ReadConfig`

```delphi
    function ReadConfig(devnum: byte): cardinal;
```

Reading the status of device `devnum`. The result is four bytes `DVSTAT ($02EA..$02ED)`.

```
    Byte 0 ($02ea):
    Bit 0:Indicates the last command frame had an error.
    Bit 1:Checksum, indicates that there was a checksum error in the last command or data frame
    Bit 2:Indicates that the last operation by the drive was in error.
    Bit 3:Indicates a write protected diskette. 1=Write protect
    Bit 4:Indicates the drive motor is on. 1=motor on
    Bit 5:A one indicates MFM format (double density)
    Bit 6:Not used
    Bit 7:Indicates Density and a Half if 1

    Byte 1 ($02eb):
    Bit 0:FDC Busy should always be a 1
    Bit 1:FDC Data Request should always be 1
    Bit 2:FDC Lost data should always be 1
    Bit 3:FDC CRC error, a 0 indicates the last sector read had a CRC error
    Bit 4:FDC Record not found, a 0 indicates last sector not found
    Bit 5:FDC record type, a 0 indicates deleted data mark
    Bit 6:FDC write protect, indicates write protected disk
    Bit 7:FDC door is open, 0 indicates door is open

    Byte 2 ($2ec):
    Timeout value for doing a format.

    Byte 3 ($2ed):
    not used, should be zero
```

---

#### `ReadSector`

```delphi
    procedure ReadSector(devnum: byte; sector: word; var buf);
```

The procedure reads the `Sector` sector of disk `devnum` and saves it into `buf` buffer.

---

#### `Rect`

```delphi
    function Rect(ALeft, ATop, ARight, ABottom: smallint): TRect;
```

The function creates a `TRect' record based on parameters.

---

#### `RenameFile`

```delphi
    function RenameFile(OldName, NewName: string): Boolean;
```

The function allows you to change the name of the `Oldname` file to the new name `Newname`, returns `TRUE` when the operation was successful, `FALSE` in the event of an error (most often due to protection against saving or erroneous file name).


```delphi
    RenameFile('D:OLDNAME.TMP', 'NEWNAME.TMP');
```

---

#### `Reset`


```delphi
    procedure Reset(var f: file; l: Word);
```

The procedure opens an existing file with the name transferred to the `f` command `Assign`. Optionally, we can provide the size of the record in bytes `l`, by default it is 128.

---

#### `Rewrite`

```delphi
    procedure Rewrite(var f: file; l: Word);
```

The procedure creates and opens a new file. `f` is the name transferred by means of the `Assign` command. Optionally, we can provide the size of the record in bytes `l`, by default it is 128.

---

#### `Round`

```delphi
    function Round(x: real): integer;
```

The function rounds the given number to the nearest integer.

---

#### `Seek`

```delphi
    procedure Seek(var f: file; N: cardinal);
```

The procedure sets the position in the file to `N`. `N` should be a value returned by `FilePos`. This is the equivalent of the instructions `POINT`.

---

#### `SetLength`

```delphi
    procedure SetLength(var S: string; Len: byte);
```

The procedure sets the length of the sequence `S` to `LEN`.

---

#### `SetIntVec`

```delphi
    procedure SetIntVec(intno: Byte; vector: pointer);
```

The procedure sets the interrupt vector address according to code **INTNO**. Currently, the permissible codes are: `iDLI` interrupt DLI, `iVBL` interrupt VBL.

---

#### `Sin`

```delphi
    function Sin(x: real): real;
```

Sinus angle `x` in radians.

---

#### `Succ`

```delphi
    function Succ(X: TOrdinal): TOrdinal;
```

The successor of the `X` element.

---

#### `Space`

```delphi
    function Space(Len: Byte): ^char;
```

The function generates a new character string with a length of `Len` filled with spaces.

---

#### `SizeOf`

```delphi
    function SizeOf(X: AnyType): byte;
```

The function returns the size of the given variable (or type) in bytes.

---

#### `Str`

```delphi
    procedure Str(var X: TNumericType; var S: string);
```

The procedure converts the number `X` into a string of `S`.

---

#### `StringOfChar`

```delphi
    procedure StringOfChar(ch: Char; len: byte): ^char;
```

The function generates a new character string with the length of `len` filled with `ch`.

---

#### `Sqr`

```delphi
    function Sqr(x: real): real;
    function Sqr(x: integer): integer;
```

Function calculating the square of the given number.

---

#### `Sqrt`

```delphi
    function Sqrt(x: real): real;
    function Sqrt(x: single): single;
    function Sqrt(x: integer): single;
```

Function calculating the square element given number (English **Square root**).

---

#### `Trunc`

```delphi
    function Trunc(x: real): integer;
```

The function returns the whole part of the number in the form of an integer.

---

#### `UpCase`

```delphi
    function UpCase(a: char): char;
```

A function changes the characters `a`..`z` to the corresponding large characters `A`..`Z`.

---

#### `Val`

```delphi
    procedure Val(const S: string; var V; var Code: Byte);
```

The procedure converts the string `S` into the number `V`. Code will take the value of `0` if there were no erroneous characters, otherwise it will take the signed number that caused a conversion error.

---

#### `WriteSector`

```delphi
    procedure WriteSector(devnum: byte; sector: word; var buf);
```

The procedure saves the sector `sector` floppy disks at the `Devnum` station based on the `buff` buffer.

## [CRT](http://mads.atari8.info/library/doc/crt.html)

### Constants

```delphi
CN_START_SELECT_OPTION  = 0;
CN_SELECT_OPTION        = 1;
CN_START_OPTION         = 2;
CN_OPTION               = 3;
CN_START_SELECT         = 4;
CN_SELECT               = 5;
CN_START                = 6;
CN_NONE                 = 7;
```

### Variables

#### `Consol`

```delphi
    Consol: byte absolute $d01f
```

The variable returns the code of the pressed key/keys.

---

#### `TextAttr`

```delphi
    TextAttr: byte = 0
```

The variable stores the value that is added to each displayed sign, e.g. `Textattr = $80` will cause the characters to be displayed in inverse.

---

#### `WhereX`

```delphi
    WhereX: byte absolute $54;
```

The variable stores the current horizontal position of the cursor.

---

#### `WhereY`

```delphi
    WhereY: byte absolute $55;
```

The variable stores the current vertical position of the cursor.

### Procedures and functions

```delphi
ClrEol             ClrScr              CursorOff          CursorOn          Delay
DelLine            GotoXY              InsLine            Keypressed        NoSound
ReadKey            Sound               TextBackground     TextColor
```

#### `ClrEol`

```delphi
    procedure ClrEol;
```

The procedure cleans the line from the current cursor position to the right side of the screen edge. The cursor position does not change.

---

#### `ClrScr`

```delphi
    procedure ClrScr;
```

The procedure clears the editor screen, performs the `CH_CLR` sign code.

---

#### `CursorOff`

```delphi
    procedure CursorOff;
```

The procedure turns off the cursor.

---

#### `CursorOn`

```delphi
    procedure CursorOn;
```

The procedure turns on the cursor.

---

#### `Delay`

```delphi
    procedure Delay(MS: Word);
```

The procedure awaits the given amount of miliseconds `MS`. Approximately `Delay (1000)` generates a delay of one second.

---

#### `DelLine`

```delphi
    procedure DelLine;
```

The procedure deletes the line at the current cursor position, performs the `CH_DELLINE` character code.

---

#### `GotoXY`

```delphi
    procedure GotoXY(x, y: byte);
```

The procedure sets the new cursor position.

---

#### `InsLine`

```delphi
    procedure InsLine;
```

The procedure inserts an empty line in the current cursor position, performs the `CH_INSLIN` sign code.

---

#### `Keypressed`

```delphi
    function Keypressed: Boolean;
```

The function returns the `TRUE` when a keyboard key has been pressed, otherwise it returns `FALSE`.

---

#### `NoSound`

```delphi
    procedure NoSound;
```

The procedure silences the channels of both **POKEY-i** `$D200` `$D210)`.

---

#### `ReadKey`

```delphi
    function ReadKey: char;
```

The function returns the code of the keyboard key.

---

#### `Sound`

```delphi
    procedure Sound(Chan,Freq,Dist,Vol: byte);
```

The procedure reproduces the sound on the **POKEY-a** `CHAN (0..3, 4..7)`, with a frequency of `FREQ (0..255)`, filters `DIST (0..7)`,volume `VOL (0..15)`.

---

#### `TextBackground`

```delphi
    procedure TextBackground(a: byte);
```

The procedure sets a new color background color (works best with **VBXE**).

---

#### `TextColor`

```delphi
    procedure TextColor(a: byte);
```

The procedure sets a new text color (works best with **VBXE**).

## [GRAPH](http://mads.atari8.info/library/doc/graph.html)

### Constants

```delphi
{ graphic drivers }
D1bit   = 11;
D2bit   = 12;
D4bit   = 13;
D6bit   = 14;       // 64 colors Half-brite mode - Amiga
D8bit   = 15;
D12bit  = 16;       // 4096 color modes HAM mode - Amiga

m640x480 = 8 + 16;

{ error codes }
grOK             = 0;
grNoInitGraph    = -1;
grNotDetected    = -2;
grFileNotFound   = -3;
grInvalidDriver  = -4;
grNoLoadMem      = -5;
grNoScanMem      = -6;
grNoFloodMem     = -7;
grFontNotFound   = -8;
grNoFontMem      = -9;
grInvalidMode    = -10;
grError          = -11;
grIOerror        = -12;
grInvalidFont    = -13;
grInvalidFontNum = -14;
grInvalidVersion = -18;
```

### Variables

#### `GraphResult`

```delphi
    GraphResult : byte
```

### Procedures and functions

```delphi
Bar                Bar3D               Circle             ClipLine          Ellipse
FillEllipse        FillRect            FloodFill          GetColor          GetMaxX
GetMaxY            GetPixel            GetX               GetY              InitGraph
Line               LineTo              MoveRel            MoveTo            PutPixel
Rectangle          SetBkColor          SetClipRect        SetColor          SetColorMapEntry
SetColorMapDimensions
```

#### `Bar`

```delphi
    procedure Bar(x1, y1, x2, y2: Smallint);
```

A rectangle, e.g. for bolts.

---

#### `Bar3D`

```delphi
    procedure Bar3D(x1, y1, x2, y2: smallint; depth: word; top: boolean);
```

Post for three-dimensional charts.

---

#### `Circle`

```delphi
    procedure Circle(x0,y0,radius: word);
```

Circle.

---

#### `ClipLine`

```delphi
    procedure ClipLine(x1, y1, x2, y2: smallint);
```

---

#### `Ellipse`

```delphi
    procedure Ellipse(x0, y0, a, b: word);
```

Ellipse.

---

#### `FillEllipse`

```delphi
    procedure FillEllipse(x0, y0, a, b: word);
```

Ellipse filled inside.

---

#### `FillRect`

```delphi
    procedure FillRect(Rect: TRect);
```

A rectangle filled inside.

---

#### `FloodFill`

```delphi
    procedure FloodFill(x, y: smallint; color: byte);
```

Filling the closed area of the screen.

---

#### `GetColor`

```delphi
    function GetColor: byte; assembler;
```

Specify the current drawing color.

---

#### `GetMaxX`

```delphi
    function GetMaxX: word;
```

Fetch the highest X coordinate value on the screen.

---

#### `GetMaxY`

```delphi
    function GetMaxY: word;
```

Fetch the highest Y coordinate value on the screen.

---

#### `GetPixel`

```delphi
    function GetPixel(x,y: smallint): byte;
```

Fetch the color of a given point on the screen.

---

#### `GetX`

```delphi
    function GetX: smallint;
```

Get the current X coordinate of the graphic cursor.

---

#### `GetY`

```delphi
    function GetY: smallint;
```

Get the current Y coordinate of the graphic cursor.

---

#### `InitGraph`

```delphi
    procedure InitGraph(mode: byte);
    procedure InitGraph(driver, mode: byte; pth: TString);
```

Initiate graphic mode.

---

#### `Line`

```delphi
    procedure Line(x0, y0, x1, y1: smallint);
```

A straight line.

---

#### `LineTo`

```delphi
    procedure LineTo(x, y: smallint);
```

The line from the current position of the cursor to the indicated point.

---

#### `MoveRel`

```delphi
    procedure MoveRel(Dx, Dy: smallint);
```

Move the graphic cursor by a relative distance.

---

#### `MoveTo`

```delphi
    procedure MoveTo(x, y: smallint);
```

Move the graphic cursor to the indicated point.

---

#### `PutPixel`

```delphi
    procedure PutPixel(x,y: smallint);
    procedure PutPixel(x,y: smallint; color: byte);
```

Light the point on the screen.

---

#### `Rectangle`

```delphi
    procedure Rectangle(x1, y1, x2, y2: smallint);
    procedure Rectangle(Rect: TRect);
```

Rectangle.

---

#### `SetBkColor`

```delphi
    procedure SetBkColor(color: byte);
```

Set the background color.

---

#### `SetClipRect`

```delphi
    procedure SetClipRect(x0,y0,x1,y1: smallint);
    procedure SetClipRect(Rect: TRect);
```

---

#### `SetColor`

```delphi
    procedure SetColor(color: byte);
```

Set the pen color.

---

#### `SetColorMapEntry`

```delphi
    procedure SetColorMapEntry;
    procedure SetColorMapEntry(a,b,c: byte);
```

---

#### `SetColorMapDimensions`

```delphi
    procedure SetColorMapDimensions(w,h: byte);
```

## [SYSUTILS](http://mads.atari8.info/library/doc/strutils.html)

### Constants

```delphi
faReadOnly  = $01;
faHidden    = $02;
faSysFile   = $04;
faVolumeID  = $08;
faDirectory = $10;
faArchive   = $20;
faAnyFile   = $3f;
```

### Types

#### `TSearchRec`

```delphi
    TSearchRec = record
            Attr: Byte;
            Name: TString;
            FindHandle: Pointer;
    end;
```

### Procedures and functions

```delphi
AnsiUpperCase      Beep                Click              DeleteFile        ExtractFileExt
FileExists         FindFirst           FindNext           FindClose         GetTickCount
IntToHex           IntToStr            RenameFile         StrToFloat        StrToInt
```

#### `AnsiUpperCase`

```delphi
    function AnsiUpperCase(const a: string): string;
```

The function converts the characters from the `a` string.

---

#### `Beep`

```delphi
    procedure Beep;
```

Beep signal (Buzzer).

---

#### `Click`

```delphi
    procedure Click;
```

Keyboard signal.

---

#### `DeleteFile`

```delphi
    function DeleteFile(var FileName: TString): Boolean;
```

The function will delete the file specified in the `FileName` parameter, returns `True` when the operation was successful.

---

#### `ExtractFileExt`

```delphi
    function ExtractFileExt(const FileName: string): TString;
```

Based on the file name or full path to the file specified in the `FileName` parameter, the function returns the extension (preceded by a dot - e.g. `.txt`).

---

#### `FileExists`

```delphi
    function FileExists(const FileName: string): Boolean;
```

The function checks that the file specified in the `FileName` parameter exists or not.

---

#### `FindFirst`

```delphi
    function FindFirst(const FileMask: TString; Attributes: Byte; var SearchResult: TSearchRec): byte;
```

The function searches for files matching the `FileMask` pattern and with attributes specified in `Attributes`. If files that match the template were found, the first of them is returned in the variable `SerchResult`.

---

#### `FindNext`

```delphi
    function FindNext(var f: TSearchRec): byte;
```

The function goes to the next record found earlier with the help of `FindFirst`. The parameter must be provided with a record that was previously used in the `FindFirst` function.

---

#### `FindClose`

```delphi
    procedure FindClose(var f: TSearchRec);
```

The procedure releases resources (memory) utilized by the `FindFirst` function. This procedure should be called each time after the search process is completed.

---

#### `GetTickCount`

```delphi
    function GetTickCount: cardinal;
```

GetTickCount returns the 24-bit time counter `(PEEK(RTCLOK+2) + PEEK(RTCLOK+1)*256 + PEEK(RTCLOK)*65536)`. This is useful for measuring time.

---

#### `IntToHex`

```delphi
    function IntToHex(Value: cardinal; Digits: byte): TString;
```

The function converts the numerical value to its hexadecimal string equivalent.

---

#### `IntToStr`

```delphi
    function IntToStr(a: integer): ^char;
```

The function is used to convert the whole number given in the parameter to string format.

---

#### `RenameFile`

```delphi
    function RenameFile(var OldName,NewName: TString): Boolean;
```

The function tries to change the file name specified in the `OldName` parameter to `NewName`. If the operation is succeeded, the function will return the value of `True` otherwise `False`. It may happen that the function will not be able to change the name (e.g. when the application has no right to it) - then the function will return `False`.

---

#### `StrToFloat`

```delphi
    function StrToFloat(var s: TString): real;
```

The function converts the string to the `Real` floating point form.

---

#### `StrToInt`

```delphi
    function StrToInt(const S: char): byte;
    function StrToInt (const S: TString): integer;
```

The function is used to convert the text saved in the `S` variable to an integer - if possible.

## [VBXE](http://mads.atari8.info/library/doc/vbxe.html)

The memory map for VBXE is defined in the `SYSTEM` module.

```delphi
VBXE_XDLADR = $0000;    // XDLIST
VBXE_MAPADR = $1000;    // COLOR MAP ADDRESS
VBXE_BCBADR = $0100;    // BLITTER LIST ADDRESS
VBXE_OVRADR = $5000;    // OVERLAY ADDRESS
VBXE_WINDOW = $B000;    // 4K WINDOW $B000..$BFFF
```

### Constants

```delphi
LoRes  = 1;  // 160x240x256c
MedRes = 2;  // 320x240x256c
HiRes  = 3;  // 640x240x16c
```

### Types

#### `TUInt24`

```delphi
    record
        byte0: byte;
        byte1: byte;
        byte2: byte;
    end;
```

24-bit type used to define memory addresses **VBXE**.

---

#### `TXDL`

```delphi
    record
        xdlc_: word;
        rptl_: byte;
        xdlc: word;
        rptl: byte;
        ov_adr: TUInt24;
        ov_step: word;
        mp_adr: TUInt24;
        mp_step: word;
        mp_hscrol: byte;
        mp_vscrol: byte;
        mp_width: byte;
        mp_height: byte;
        ov_width: byte;
        ov_prior: byte;
    end;
```

Type `TXDL` used by the procedures `GetXDL` and `SetXDL`. It allows you to modify the program for **VBXE** used by **MP**.

---

#### `TBCB`

```delphi
    record
        src_adr: TUInt24;
        src_step_y: smallint;
        src_step_x: shortint;
        dst_adr: TUInt24;
        dst_step_y: smallint;
        dst_step_x: shortint;
        blt_width: word;
        blt_height: byte;
        blt_and_mask: byte;
        blt_xor_mask: byte;
        blt_collision_mask: byte;
        blt_zoom: byte;
        pattern_feature: byte;
        blt_control: byte;
    end;
```

Type `TBCB` (21 bytes), **Blitter Code Block**. Definition of the Blitter block type Blitter **VBXE**.

---

#### `TVBXEMemoryStream`

```delphi
    Object
        Position: cardinal;
        Size: cardinal;         // 0..Size-1

        procedure Create;

        procedure Clear;
        procedure SetBank;

        procedure ReadBuffer(var Buffer; Count: word);
        procedure WriteBuffer(var Buffer; Count: word);

        function ReadByte: Byte;
        function ReadWord: Word;
        function ReadDWord: Cardinal;

        procedure WriteByte(b: Byte);
        procedure WriteWord(w: Word);
        procedure WriteDWord(d: Cardinal);
    end;
```

The `TVBXEMemoryStream` object allows for linear access to memory **VBXE**.

### Procedures and functions

```delphi
BlitterBusy        ColorMapOff         ColorMapOn         DstBCB            ExtractFileExt
GetXDL             IniBCB              OverlayOff         RunBCB            SetHorizontalRes
VBXEMemoryBank     SetXDL              SrcBCB             VBXEControl       VBXEOff
```

#### `BlitterBusy`

```delphi
    function BlitterBusy: Boolean; assembler;
```

The function returns `True` if Blitter **VBXE** is occupied by performing a Blitter program.

---

#### `ColorMapOff`

```delphi
    procedure ColorMapOff; assembler;
```

Turning off the color map in the `XDLIST` for **VBXE**.

---

#### `ColorMapOn`

```delphi
    procedure ColorMapOn; assembler;
```

Turning on the color map in the `XDLIST` for **VBXE**.

---

#### `DstBCB`

```delphi
    procedure DstBCB(var a: TBCB; dst: cardinal);
```

The procedure amending the target address `dst` in the Blitter program `a`.

---

#### `GetXDL`

```delphi
    procedure GetXDL(var a: txdl); register; assembler;
```

The procedure prescribes to the variable `A` program` XDLIST` from the address `VBXE_XDLADR` in memory **VBXE**.

---

#### `IniBCB`

```delphi
    procedure IniBCB(var a: TBCB; src,dst: cardinal; w0, w1: smallint; w: word; h: byte; ctrl: byte);
```

The procedure allows you to initiate memory for the Blitter program at `A`. Additional parameters specify the address from which the `SRC` data will be copied, the target address of the copied data `DST`, width of `W0`, target `W1` target window, size of the result window, its width `W`, height `H`, and to specify the final parameters of the Blitter block `CTRL` (Bit 3 `CTRL` is set up to the Blitter reading of the next program and its implementation).

---

#### `OverlayOff`

```delphi
    procedure OverlayOff; assembler;
```

Disabling overlay mode in the `XDLIST`.

---

#### `RunBCB`

```delphi
    procedure RunBCB(var a: TBCB); assembler;
```

Blitter starting **VBXE** based on the `A` program.

---

#### `SetHorizontalRes`

```delphi
    procedure SetHorizontalRes(a: byte); assembler;
    procedure SetHRes(a: byte); assembler;
```

Establishment of overlay mode in the `XDLIST` program.

---

#### `VBXEMemoryBank`

```delphi
    procedure VBXEMemoryBank(b: byte); assembler;
```

Turning on 4K Bank **VBXE** in the memory window **XE/XL** `$B000..$BCFF`.

---

#### `SetXDL`

```delphi
    procedure SetXDL(var a: txdl); register; assembler;
```

The procedure rewrites the `A` program to `VBXE_XDLADR` in memory **VBXE**.

---

#### `SrcBCB`

```delphi
    procedure SrcBCB(var a: TBCB; src: cardinal);
```

Procedure amending the source address `SRC_ADR` in the Blitter program `A`.

---

#### `VBXEControl`

```delphi
    procedure VBXEControl(a: byte); assembler;
```

The procedure sets the value of `FX_VIDEO_CONTROL`.

---

#### `VBXEOff`

```delphi
    procedure VBXEOff
```

Disable, reset **VBXE**.

## [MATH](http://mads.atari8.info/library/doc/math.html)

### Procedures and functions

```delphi
ArcCos             ArcSin              ArcTan2            Ceil              CycleToRad
DegNormalize       DegToGrad           DegToRad           DivMod            EnsureRange
Floor              FMod                GradToDeg          GradToRad         InRange
IsNan              Log2                Log10              LogN              Max
Min                Power               RadToCycle         RadToDeg          RadToGrad
RandG              RandomRange         RandomRangeF       Tan
```

#### `ArcCos`

```delphi
    function ArcCos(x: real): real;
```

`Arccos` is the opposite function for the `COS` function. The value of the parameter `X` must belong to the interval of both sides of the range `<-1; 1>`. The value returned by the function is the angle from `<0; ?>` expressed in the radians.

---

#### `ArcSin`

```delphi
    function ArcSin(x: real): real;
```

The function is used to calculate the mathematical function of the Arcus Sinus with the number `X`. This is the opposite function to the sine function, i.e. `sin(arcsin(x)) = x`.

---

#### `ArcTan2`

```delphi
    function ArcTan2(y, x: real) : real;
```

The function calculates Arcus Tangens (the opposite of Tangens) from the number `Y/X` and returns the value in radians.

---

#### `Ceil`

```delphi
    function Ceil(a: real): smallint;
```

The function returns the smallest integer larger than or equal to the one given in the parameter.

---

#### `CycleToRad`

```delphi
    function CycleToRad(cycle : real) : real;
```

The function converts the value of the angle expressed in cycles (revolutions) into an angle expressed in radians.

---

#### `DegNormalize`

```delphi
    function DegNormalize(deg : real) : real;
```

---

#### `DegToGrad`

```delphi
    function DegToGrad(deg : real) : real;
```

The function converts the value of the angle expressed in the degree of angle expressed in gradians.

---

#### `DegToRad`

```delphi
    function DegToRad(deg : real) : real;
```

The function converts the value of the angle expressed in the degree of angle expressed in the arc, i.e. radians.

---

#### `DivMod`

```delphi
    procedure DivMod(Dividend: integer; Divisor: Word; var r, Remainder: Word);
    procedure DivMod(Dividend: integer; Divisor: Word; var r, Remainder: smallint);
```

---

#### `EnsureRange`

```delphi
    function EnsureRange(const AValue, AMin, AMax: byte): Integer;
    function EnsureRange(const AValue, AMin, AMax: Integer): Integer;
```

---

#### `Floor`

```delphi
    function Floor(a: real): smallint;
```

The function returns the nearest integers less or equal to the one given in the parameter.

---

#### `FMod`

```delphi
    function FMod(a, b: real): real;
```

The function returns the rest of the division of two real numbers.

---

#### `GradToDeg`

```delphi
    function GradToDeg(grad : real) : real;
```

The function converts the value of the angle expressed in gradians into the angle expressed in the degrees.

---

#### `GradToRad`

```delphi
    function GradToRad(grad : real) : real;
```

The `GradToRad` function converts the value of the angle expressed in gradians into the angle expressed in radians.

---

#### `InRange`

```delphi
    function InRange(const AValue, AMin, AMax: byte): Boolean;
    function InRange(const AValue, AMin, AMax: Integer): Boolean;
```

---

#### `IsNan`

```delphi
    function IsNan(const d : Single): Boolean;
```

Funkcja sprawdza czy wartość parametru `d` jest poprawną liczbą.

---

#### `Log2`

```delphi
    function log2(x : single): single;
```

Funkcja zwraca wartość logarytmu przy podstawie 2 dla parametru rzeczywistego X>0.

---

#### `Log10`

```delphi
    function log10(x : single): single;
```

Funkcja zwraca wartość logarytmu dziesiętnego (logarytmu przy podstawie 10) dla parametru rzeczywistego X>0.

---

#### `LogN`

```delphi
    function logN(n,x : single): single;
```

Funkcja zwraca wartość logarytmu przy podstawie N>0 dla parametru rzeczywistego X>0.

---

#### `Max`

```delphi
    function Max(a, b: real): real;
    function Max(a, b: integer): integer;
```

Przeciążona funkcja porównuje wartości dwóch parametrów: `a` i `b`, oraz zwraca ten, który jest większy.

---

#### `Min`

```delphi
    function Min(a, b: real): real;
    function Min(a, b: integer): integer;
```

Przeciążona funkcja porównuje wartości dwóch parametrów `a` i `b`, oraz zwraca wartość tego który jest mniejszy.

---

#### `Power`

```delphi
    function Power(base : real; const exponent : shortint): real;
    power(base : integer; const exponent : shortint): integer;
```

Funkcja podnosi liczbę A do dowolnej potęgi N, potęga może być ułamkiem.

---

#### `RadToCycle`

```delphi
    function RadToCycle(rad : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w radianach na kąt wyrażony w cyklach (obrotach).

---

#### `RadToDeg`

```delphi
    function RadToDeg(rad : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w radianach na kąt wyrażony w stopniach (deg).

---

#### `RadToGrad`

```delphi
    function RadToGrad(rad : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w radianach na kąt wyrażony w gradach.

---

#### `RandG`

```delphi
    function RandG(mean, StdDev : single) : single;
```

`RandG` reprezentuje generator liczb pseudolosowych o rozkładzie **Gaussa** wokół średniej `mean`. Parametr `StdDev` jest odchyleniem standardowym generowanych liczb od wartości średniej `mean`.

---

#### `RandomRange`

```delphi
    function RandomRange(const aFrom, aTo: smallint): smallint;
```

Funkcja zwraca losową liczbę z przedziału `AFrom - ATo`, łącznie z wartością `ATo`.

---

#### `RandomRangeF`

```delphi
    function RandomRangeF(const min, max: single): single;
```

---

#### `Tan`

```delphi
    function Tan(x: Real): Real;
```

Funkcja zwraca wartość tangensa kąta podanego w parametrze `x`.