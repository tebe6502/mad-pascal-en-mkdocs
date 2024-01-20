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

Funkcja zwraca rozmiar podanej zmiennej (lub typu) w bajtach.

---

#### `Str`

```delphi
    procedure Str(var X: TNumericType; var S: string);
```

Procedura zamienia liczbę `X` na łańcuch znaków `S`.

---

#### `StringOfChar`

```delphi
    procedure StringOfChar(ch: Char; len: byte): ^char;
```

Funkcja generuje nowy ciąg znakowy o długości `len` wypełniony znakami `ch`.

---

#### `Sqr`

```delphi
    function Sqr(x: real): real;
    function Sqr(x: integer): integer;
```

Funkcja obliczająca kwadrat podanej liczby (ang. **Square**).

---

#### `Sqrt`

```delphi
    function Sqrt(x: real): real;
    function Sqrt(x: single): single;
    function Sqrt(x: integer): single;
```

Funkcja obliczająca pierwiastek kwadratowy podanej liczby (ang. **Square root**).

---

#### `Trunc`

```delphi
    function Trunc(x: real): integer;
```

Funkcja zwraca część całkowitą liczby rzeczywistej w postaci liczby całkowitej.

---

#### `UpCase`

```delphi
    function UpCase(a: char): char;
```

Funkcja zmieniająca znaki `'a'..'z'` na odpowiednie duże znaki `'A'..'Z'`.

---

#### `Val`

```delphi
    procedure Val(const S: string; var V; var Code: Byte);
```

Procedura przekształca ciąg znaków `S` na liczbę `V`. Code przyjmie wartość `0` jeśli nie było błędnych znaków, w przeciwnym wypadku przyjmie numer znaku który spowodował błąd konwersji.

---

#### `WriteSector`

```delphi
    procedure WriteSector(devnum: byte; sector: word; var buf);
```

Procedura zapisuje sektora `sector` dyskietki w stacji `devnum` na podstawie bufora `buf`.

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

Zmienna zwraca kod naciśniętego klawisza/klawiszy konsoli.

---

#### `TextAttr`

```delphi
    TextAttr: byte = 0
```

Zmienna przechowuje wartość jaka jest dodawana do każdego wyświetlanego znaku, np. `TextAttr = $80` spowoduje że znaki będą wyświetlane w inwersie.

---

#### `WhereX`

```delphi
    WhereX: byte absolute $54;
```

Zmienna przechowuje aktualną poziomą pozycję kursora.

---

#### `WhereY`

```delphi
    WhereY: byte absolute $55;
```

Zmienna przechowuje aktualną pionową pozycję kursora.

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

Procedura czyści wiersz od aktualnej pozycji kursora do prawej strony krawędzi ekranu. Pozycja kursora nie ulega zmianie.

---

#### `ClrScr`

```delphi
    procedure ClrScr;
```

Procedura czyści ekran edytora, wykonuje kod znaku `CH_CLR`.

---

#### `CursorOff`

```delphi
    procedure CursorOff;
```

Procedura wyłącza kursor.

---

#### `CursorOn`

```delphi
    procedure CursorOn;
```

Procedura włącza kursor.

---

#### `Delay`

```delphi
    procedure Delay(MS: Word);
```

Procedura czeka zadaną ilość milisekund `MS`. W przybliżeniu `Delay(1000)` generuje opóźnienie jednej sekundy.

---

#### `DelLine`

```delphi
    procedure DelLine;
```

Procedura kasuje wiersz na aktualnej pozycji kursora, wykonuje kod znaku `CH_DELLINE`.

---

#### `GotoXY`

```delphi
    procedure GotoXY(x, y: byte);
```

Procedura ustawia nową pozycję kursora.

---

#### `InsLine`

```delphi
    procedure InsLine;
```

Procedura wstawia pusty wiersz na aktualnej pozycji kursora, wykonuje kod znaku `CH_INSLINE`.

---

#### `Keypressed`

```delphi
    function Keypressed: Boolean;
```

Funkcja zwraca `TRUE` gdy został naciśnięty jakiś klawisz klawiatury, w przeciwnym razie zwraca `FALSE`.

---

#### `NoSound`

```delphi
    procedure NoSound;
```

Procedura wycisza kanały obu **POKEY-i** `$D200` `$D210)`.

---

#### `ReadKey`

```delphi
    function ReadKey: char;
```

Funkcja zwraca kod naciśniętego klawisza klawiatury.

---

#### `Sound`

```delphi
    procedure Sound(Chan,Freq,Dist,Vol: byte);
```

Procedura odtwarza dźwięk na kanale **POKEY-a** `CHAN (0..3, 4..7)`, o częstotliwości `FREQ (0..255)`, filtrach `DIST (0..7)`, głośności `VOL (0..15)`.

---

#### `TextBackground`

```delphi
    procedure TextBackground(a: byte);
```

Procedura ustawia nowy kolor tła znaków (działa najlepiej z włączonym **VBXE**).

---

#### `TextColor`

```delphi
    procedure TextColor(a: byte);
```

Procedura ustawia nowy kolor znaków (działa najlepiej z włączonym **VBXE**).

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

Prostokąt, np. dla wykresów słupkowych.

---

#### `Bar3D`

```delphi
    procedure Bar3D(x1, y1, x2, y2: smallint; depth: word; top: boolean);
```

Słupek dla wykresów trójwymiarowych.

---

#### `Circle`

```delphi
    procedure Circle(x0,y0,radius: word);
```

Okrąg.

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

Elipsa.

---

#### `FillEllipse`

```delphi
    procedure FillEllipse(x0, y0, a, b: word);
```

Elipsa wypełniona wewnątrz.

---

#### `FillRect`

```delphi
    procedure FillRect(Rect: TRect);
```

Prostokąt wypełniony wewnątrz.

---

#### `FloodFill`

```delphi
    procedure FloodFill(x, y: smallint; color: byte);
```

Wypełnienie zamkniętego obszaru ekranu.

---

#### `GetColor`

```delphi
    function GetColor: byte; assembler;
```

Podaj bieżący kolor rysowania.

---

#### `GetMaxX`

```delphi
    function GetMaxX: word;
```

Podaj najwyższą wartość współrzędnej X na ekranie.

---

#### `GetMaxY`

```delphi
    function GetMaxY: word;
```

Podaj najwyższą wartość współrzędnej Y na ekranie.

---

#### `GetPixel`

```delphi
    function GetPixel(x,y: smallint): byte;
```

Podaj kolor danego punktu na ekranie.

---

#### `GetX`

```delphi
    function GetX: smallint;
```

Podaj bieżącą współrzędną X kursora graficznego.

---

#### `GetY`

```delphi
    function GetY: smallint;
```

Podaj bieżącą współrzędną Y kursora graficznego.

---

#### `InitGraph`

```delphi
    procedure InitGraph(mode: byte);
    procedure InitGraph(driver, mode: byte; pth: TString);
```

Zainicjuj tryb graficzny.

---

#### `Line`

```delphi
    procedure Line(x0, y0, x1, y1: smallint);
```

Linia prosta.

---

#### `LineTo`

```delphi
    procedure LineTo(x, y: smallint);
```

Linia od bieżącej pozycji kursora do wskazanego punktu.

---

#### `MoveRel`

```delphi
    procedure MoveRel(Dx, Dy: smallint);
```

Przesuń kursor graficzny.

---

#### `MoveTo`

```delphi
    procedure MoveTo(x, y: smallint);
```

Przesuń kursor graficzny do wskazanego punktu.

---

#### `PutPixel`

```delphi
    procedure PutPixel(x,y: smallint);
    procedure PutPixel(x,y: smallint; color: byte);
```

Zapal punkt na ekranie.

---

#### `Rectangle`

```delphi
    procedure Rectangle(x1, y1, x2, y2: smallint);
    procedure Rectangle(Rect: TRect);
```

Prostokąt.

---

#### `SetBkColor`

```delphi
    procedure SetBkColor(color: byte);
```

Ustaw kolor tła.

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

Ustaw kolor pisaka.

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

Funkcja konwertuje znaki z łańcucha `a` na wielkie.

---

#### `Beep`

```delphi
    procedure Beep;
```

Sygnał brzęczka (buzzer).

---

#### `Click`

```delphi
    procedure Click;
```

Sygnał klawiatury.

---

#### `DeleteFile`

```delphi
    function DeleteFile(var FileName: TString): Boolean;
```

Funkcja kasuje plik określony w parametrze `FileName`, zwraca `TRUE` gdy operacja się powiodła.

---

#### `ExtractFileExt`

```delphi
    function ExtractFileExt(const FileName: string): TString;
```

Na podstawie nazwy pliku lub pełnej ścieżki do pliku określonej w parametrze `FileName`, funkcja zwraca rozszerzenie (poprzedzone kropką - np. `.txt`).

---

#### `FileExists`

```delphi
    function FileExists(const FileName: string): Boolean;
```

Funkcja sprawdza czy plik określony w parametrze `FileName`, istnieje `True` czy też nie `False`.

---

#### `FindFirst`

```delphi
    function FindFirst(const FileMask: TString; Attributes: Byte; var SearchResult: TSearchRec): byte;
```

Funkcja wyszukuje pliki pasujące do wzorca `FileMask` i posiadające atrybuty określone w `Attributes`. Jeśli zostały znalezione pliki pasujące do szablonu to pierwszy z nich jest zwracany w zmiennej `SerchResult`.

---

#### `FindNext`

```delphi
    function FindNext(var f: TSearchRec): byte;
```

Funkcja przechodzi do następnego rekordu znalezionego wcześniej przy pomocy `FindFirst`. W parametrze musi zostać przekazane wskazanie na rekord, który wcześniej został użyty w funkcji `FindFirst`.

---

#### `FindClose`

```delphi
    procedure FindClose(var f: TSearchRec);
```

Procedura zwalnia zasoby (pamięć) zaalokowaną przez funkcję `FindFirst`. Procedura ta powinna być wywoływana za każdym razem po zakończeniu procesu wyszukiwania.

---

#### `GetTickCount`

```delphi
    function GetTickCount: cardinal;
```

GetTickCount zwraca 24-bitowy licznik czasu `(PEEK(RTCLOK+2) + PEEK(RTCLOK+1)*256 + PEEK(RTCLOK)*65536)`. Jest to przydatne do pomiaru czasu.

---

#### `IntToHex`

```delphi
    function IntToHex(Value: cardinal; Digits: byte): TString;
```

Funkcja konwertuje wartość liczbową na jej odpowiednik łańcuchowy w systemie szesnastkowym.

---

#### `IntToStr`

```delphi
    function IntToStr(a: integer): ^char;
```

Funkcja służy do konwersji liczby całkowitej podanej w parametrze do postaci łańcuchowej.

---

#### `RenameFile`

```delphi
    function RenameFile(var OldName,NewName: TString): Boolean;
```

Funkcja próbuje zmienić nazwę pliku określonego w parametrze `OldName` na `NewName`. Jeżeli operacja się powiedzie, funkcja zwróci wartość `True` w przeciwnym wypadku `False`. Może się zdarzyć, że funkcja nie będzie mogła zmienić nazwy (np. gdy aplikacja nie ma prawa do tego) - wówczas funkcja zwróci `False`.

---

#### `StrToFloat`

```delphi
    function StrToFloat(var s: TString): real;
```

Funkcja konwertuje łańcuch do postaci zmiennoprzenkowej typu `Real`.

---

#### `StrToInt`

```delphi
    function StrToInt(const S: char): byte;
    function StrToInt (const S: TString): integer;
```

Funkcja służy do konwersji tekstu zapisanego w zmiennej S na liczbę całkowitą - o ile to możliwe.

## [VBXE](http://mads.atari8.info/library/doc/vbxe.html)

Mapa pamięci dla VBXE zdefiniowana jest w module `SYSTEM`.

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

Typ 24-bitowy wykorzystywany do definicji adresów pamięci **VBXE**.

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

Typ `TXDL` wykorzystywany przez procedury `GetXDL` i `SetXDL`. Pozwala na modyfikację programu dla **VBXE** wykorzystywanego przez **MP**.

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

Typ `TBCB` (21 bajtów), **Blitter Code Block**. Definicja typu bloku programu dla Blittera **VBXE**.

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

Obiekt `TVBXEMemoryStream` pozwala na liniowy dostęp do pamięci **VBXE**.

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

Funkcja zwraca `TRUE` jeśli blitter **VBXE** zajęty jest wykonywaniem programu blittera.

---

#### `ColorMapOff`

```delphi
    procedure ColorMapOff; assembler;
```

Wyłączenie mapy kolorów w programie `XDLIST` dla **VBXE**.

---

#### `ColorMapOn`

```delphi
    procedure ColorMapOn; assembler;
```

Włączenie mapy kolorów w programie `XDLIST` dla **VBXE**.

---

#### `DstBCB`

```delphi
    procedure DstBCB(var a: TBCB; dst: cardinal);
```

Procedura zmieniająca adres docelowy `dst_adr` w programie blittera `A`.

---

#### `GetXDL`

```delphi
    procedure GetXDL(var a: txdl); register; assembler;
```

Procedura przepisuje do zmiennej `A` program `XDLIST` spod adresu `VBXE_XDLADR` w pamięci **VBXE**.

---

#### `IniBCB`

```delphi
    procedure IniBCB(var a: TBCB; src,dst: cardinal; w0, w1: smallint; w: word; h: byte; ctrl: byte);
```

Procedura pozwala zaincjować pamięć dla programu blittera pod adresem `A`. Dodatkowe parametry określają adres spod którego będą kopiowane dane `SRC`, adres docelowy kopiowanych danych `DST`, szerokość okna danych źródłowych `W0`, docelowych `W1`, rozmiar okna wynikowego, jego szerokość `W`, wysokość `H`, oraz określić parametry końcowe bloku programu blittera `CTRL` (ustawiony bit 3 `CTRL` nakazuje blitterowi odczyt kolejnego programu i jego wykonanie).

---

#### `OverlayOff`

```delphi
    procedure OverlayOff; assembler;
```

Wyłączenie trybu overlay w programie `XDLIST`.

---

#### `RunBCB`

```delphi
    procedure RunBCB(var a: TBCB); assembler;
```

Wystartowanie blittera **VBXE** na podstawie adresu programu `A`.

---

#### `SetHorizontalRes`

```delphi
    procedure SetHorizontalRes(a: byte); assembler;
    procedure SetHRes(a: byte); assembler;
```

Ustanowienie trybu overlay w programie `XDLIST`.

---

#### `VBXEMemoryBank`

```delphi
    procedure VBXEMemoryBank(b: byte); assembler;
```

Włączenie 4K banku **VBXE** w okno pamięci **XE/XL** `$B000..$BCFF`.

---

#### `SetXDL`

```delphi
    procedure SetXDL(var a: txdl); register; assembler;
```

Procedura przepisuje program `A` pod adres `VBXE_XDLADR` w pamięci **VBXE**.

---

#### `SrcBCB`

```delphi
    procedure SrcBCB(var a: TBCB; src: cardinal);
```

Procedura zmieniająca adres źródłowy `src_adr` w programie blittera `A`.

---

#### `VBXEControl`

```delphi
    procedure VBXEControl(a: byte); assembler;
```

Procedura ustawia wartośc `FX_VIDEO_CONTROL`.

---

#### `VBXEOff`

```delphi
    procedure VBXEOff
```

Wyłączenie, reset **VBXE**.

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

`ArcCos` jest funkcją odwrotną do funkcji `Cos`. Wartość parametru `X` musi należeć do przedziału obustronnie domkniętego `<-1; 1>`. Wartością zwracaną przez funkcję jest kąt z przedziału `<0; ?>` wyrażony w mierze łukowej (radianach).

---

#### `ArcSin`

```delphi
    function ArcSin(x: real): real;
```

Funkcja służy do obliczenia funkcji matematycznej arcus sinus z liczby `X`. Jest to funkcja odwrotna do funkcji sinus, tzn. `sin(arcsin(x)) = x`.

---

#### `ArcTan2`

```delphi
    function ArcTan2(y, x: real) : real;
```

Funkcja oblicza arcus tangens (odwrotność tangensa) z liczby `Y/X` i zwraca wartość w radianach.

---

#### `Ceil`

```delphi
    function Ceil(a: real): smallint;
```

Funkcja zwraca najmniejszą liczbę całkowitą większą lub równą od tej podanej w parametrze.

---

#### `CycleToRad`

```delphi
    function CycleToRad(cycle : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w cyklach (obrotach) na kąt wyrażony w radianach.

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

Funkcja przelicza wartość kąta wyrażonego w stopniach na kąt wyrażony w gradach.

---

#### `DegToRad`

```delphi
    function DegToRad(deg : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w stopniach na kąt wyrażony w mierze łukowej, czyli radianach.

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

Funkcja zwraca najbliższą liczbę całkowitą mniejszą lub równą od tej podanej w parametrze.

---

#### `FMod`

```delphi
    function FMod(a, b: real): real;
```

Funkcja zwraca resztę z dzielenia dwóch liczb rzeczywistych.

---

#### `GradToDeg`

```delphi
    function GradToDeg(grad : real) : real;
```

Funkcja przelicza wartość kąta wyrażonego w gradach na kąt wyrażony w stopniach.

---

#### `GradToRad`

```delphi
    function GradToRad(grad : real) : real;
```

Funkcja GradToRad przelicza wartość kąta wyrażonego w gradach na kąt wyrażony w radianach.

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