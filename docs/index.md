# Mad-Pascal

**Mad-Pascal** (MP) is a 32-bit **Turbo Pascal** compiler for **Atari 8-Bit** and other **MOS 6502 CPU**-based computers. By design, it is compatible with the **Free Pascal Compiler** (FPC) (the `-MDelphi` switch should be active). This means the possibility of obtaining executable code for **Atari 8-bit**, **Windows** and every other platform for which **FPC** exists. **Mad-Pascal** is not a port of **FPC**. It has been written based on of **SUB-Pascal** (2009), **XD-Pascal** (2010), the author of which is [Vasiliy Tereshkov](https://github.com/vtereshkov).

Sources are on [GitHub](https://github.com/tebe6502/Mad-Pascal) with [release](https://github.com/tebe6502/Mad-Pascal/releases) for Windows operating system.

# History

## [1.7.2](https://github.com/tebe6502/Mad-Pascal/releases/tag/v1.7.2)
- optimizations, bugfixes
- faster code for ABSOLUTE arrays
- unit SYSTEM added array 'mem: array [0..0] of byte absolute $0000'
- optimization for CASE (tail optimize)
- INC/DEC optimization for [striped] arrays
- new unit E80, handler E: in HiRes mode, 80 columns.
- new unit RC4, encryption with RC4 algorithm

## [1.7.0](https://github.com/tebe6502/Mad-Pascal/releases/tag/v1.7.0)
- [STRIPED] for arrays with a maximum range of 0..255
- new target, neo6502 (-t neo)
- GRAPH.INC: Circle (faster version)
- fixes lib/aplib.pas
- fixes lib/zx0.pas
- improved CASE optimization
- added directive {$UNITPATH filename} as equivalent to {$LIBRARYPATH filename}
- added ability to specify a path for a module declared by USES, e.g:
```
uses crt, vector in '...\3d_vector.pas';
```
- added support for LIBRARY modules
- added EXTERNAL modifier for variables, procedures, functions
- added ability to set compilation address on source code level, e.g.:
```
program name : address;
library name : address;
```

## [1.6.9](https://github.com/tebe6502/Mad-Pascal/releases/tag/v1.6.9)
- improved memory allocation for arrays [0..0], 'ABSOLUTE $0000' is enforced initially, save 1 byte of memory
- added possibility to declare arrays without specifying their size, e.g.:
```
var tab: array of byte = [1,3,4,3,1];
var tb: array of char = 'abcdefghij';
```
- new compiler directive `{$bin2csv filename}` allows to initialize arrays e.g.:
```
var tb: array of byte = [ {$bin2csv filename} ];
```
- new compiler directive `{$optimization loopunroll}`, `{$optimization noloopunroll}`, performs `FOR` loop unrolling with fixed parameters
- new BLOWFISH module allowing to encrypt, decrypt character strings according to specified key
- new example a8\AES-Rijndeal

## [1.6.7-1.6.8](https://github.com/tebe6502/Mad-Pascal/releases/tag/v1.6.7-1.6.8)
- Resignation of type expansion for expressions with SHR
- new SAPR resource type, SAPRPLAY
- for RMTPLAY, you can specify the address for variables on the null page as the second parameter
- SizeOfResource(variable, name)
- unit SAPLZSS
- unit SHANTI
- unit SHA1
- unit xSFX
- unit SYSTEM: NtoBE, RorByte, RorWord, RorDWord, RolByte, RolWord, RolDWord, SarShortint, SarSmallint, SarLongint
- possibility to instantiate an array of CHAR type by STRING (if string is shorter spaces will be inserted), e.g.:
```
    tab: array [0..15] of char = '0123456789ABCDEF';
```
- fixed passing function values through arrays
- added support for VBLKI interrupts (immediate) via SetIntVec, GetIntVec (https://mads.atari8.info/doc/pl/przerwania/)
- rewritten compiler code for mod separable modules
- rewritten code for handling arrays with pointers to records `tab: array [0..x] of record^`
- added optimization 'Common head/tail Sequence coalescing'

## [1.6.6](https://github.com/tebe6502/Mad-Pascal/releases/tag/1.6.6)
- improved implementation of EXIT
- added ability to generate code for RAW (-target)
- added support for the INLINE modifier for procedures and functions
- added ability to declare a variable on the null page by using the REGISTER modifier
- added support for TEXTFILE (TEXT) type
- unit INIFILES
- unit ZX2
- unit SYSUTILS: CompareMem, TryStrToInt
- unit SYSTEM: CompareByte, Pos, Delete
- improved passing of parameters to objects (OBJECT) without participation of the :STACKORIGIN program stack (in most cases)
- added possibility to mark a variable as transient [volatile].
- for OBJECT added methods CONSTRUCTOR, DESTRUCTOR
- added support for macros {$define label (parameters) := expression}
- added 'FOR element IN array' construction for arrays not exceeding 256 bytes
- more free memory on zero page, FXPTR, PSPTR pointers are now allocated depending on whether they are used
- added support for FLOAT16 type
- added support for procedural type

## [1.6.5](https://github.com/tebe6502/Mad-Pascal/releases/tag/1.6.5)
- rewritten handling of CASE OF
- rewritten code optimization for arrays not exceeding 256 bytes
- optimization for conditions '>', '<='
- added memory allocation for STRING-type arrays (so far only the pointer was put away, it worked like 'array of ^string')
- new platform added, Commodore C4 Plus
- unit GRAPHICS: procedure Font(charset: pointer);
- unit STRINGUTILS
- unit MISC, RMT, CMC, MPT: DetectAntic
- unit SYSTEM revised to include ATARI, C64, C4Plus platforms
- unit ZX0
- unit HCM2
- added support of $resource (RCDATA, RCASM) for C64, C4Plus platforms, resources are sorted by ascending addresses
- extended RCDATA resource with possibility to specify ofset for read file
- added support for Pascal compliant syntax for ASM block, no { } brackets required
- added new directive {$codealign proc = value}, {$codealign loop = value} allowing to align generated code

## [1.6.4](https://github.com/tebe6502/Mad-Pascal/releases/tag/1.6.4)
- multiplying procedures u8x8, u16x16 replaced by code from CC65
- adding the POKEY reset code at the beginning of the program launch
- optimization of conditional IF expressions () and () and ... IF () or () or ...
- CMP_SHORTINT, CMP_SMALLINT optimization
- GRAPH, FASTGRAPH: SetActiveBuffer, SetDisplayBuffer, NewDisplayBuffer, SwitchDisplayBuffer, example demoeffects\lines2.pas, line3.pas, line4.pas
- GRAPH: Ellipse procedure (X, Y, StAngle, EndAngle, xRadius,yRadius: Word);
- MATH: Hypot
- SYSTEM: Length(string_array[element])
- SYSTEM: GetMem, FreeMem
- SYSTEM: IntToStr(CARDINAL), Str(CARDINAL, STRING)
- SYSUTILS: ByteToStr(BYTE): STRING
- SYSUTILS: corrected FindFirst, StrToFloat
- SYSTEM: corrected Val(string, real, code) ; Val(string, single, code)
- new CIO unit: Opn, Cls, Get, Put, BGet, BPut, XIO
- new SIODISK unit, separated from the SYSTEM
- new S2 unit, integrated with handler installer VBXE-S2: (S_VBXE.SYS)
- new DEFLATE unit, which performs DEFLATE decompression (procedure unDEF), example compression\undef.pas
- new LZ4 unit, implementing LZ4 decompression (procedure unLZ4), example compression\unlz4.pas, unlz4_stream.pas
- new APLIB unit, which performs apLib decompression (procedure unApl), example compression\unapl.pas, unapl_stream.pas
- new CRC unit: function crc32(crc: cardinal; buf: Pbyte; len: word)
- a new PASCAL procedure/function modifier, causing a new memory block to be assigned/released for variables each time a procedure/function is called, example 'math\evaluate.pas'.
- added ability to disable ROM while maintaining system operation, {$DEFINE ROMOFF}
- shorter names of the switch -zpage (-z), -stack (-s), -data (-d), -code (-c), -define (-d), -ipath (-i)
- added possibility to generate code for C64 (-t c64)

## [1.6.3](https://github.com/tebe6502/Mad-Pascal/releases/tag/v1.6.3)
- fixes, optimizations
- SYSUTILS: Trim
- SYSTEM: PByte, PByteArray, PWord
- GRAPH, FASTGRAPH: TFrameBuffer, DisplayBuffer, FrameBuffer, SwitchBuffer, Scanline
- BLIBS: unit GR10PP
- LIB: unit GR4PP

## 1.6.0 - 1.6.2
- new EFAST unit for speeding up character output to E device:
- SYSTEM: function Copy(var S: String; Index: Byte; Count: Byte): String;
- SYSTEM: Palette, HPalette
- added support for one-dimensional arrays of type ^RECORD (pointer to a record)
- optimization of conditional blocks, the shortest, fastest possible resulting code is generated
- added PChar type, [link]https://www.freepascal.org/docs-html/rtl/system/pchar.html
- added ability to return function value by enumeration type
- added new switch -define:symbol
- added new switch -ipath:includepath

## 1.5.9 - 1.6.0
- SYSTEM: TDateTime
- GRAPH, FASTGRAPH: Arc, PieSlice, TLastArcCoords, LastArcCoords
- SYSUTILS: Now, Date, DateToStr, DecodeDate, DecodeDateTime, DecodeTime, EncodeDate, EncodeDateTime, EncodeTime, IsLeapYear, BoolToStr, StrToBool
- STRUTILS: AddChar, AddCharR, PadLeft, PadRight
- Added support for {$INCLUDE %DATE%}, {$INCLUDE %TIME%}, [link]https://www.freepascal.org/docs-html/prog/progsu41.html
- switches -CODE:, -DATE:, -STACK:, -ZPAGE: by default require HEX value without initial '$' character.
