# Mad-Pascal

**Mad-Pascal** (MP) is a 32-bit **Turbo Pascal** compiler for **Atari XE/XL**. By design, it is compatible with the **Free Pascal Compilator** (FPC) (the `-MDelphi` switch should be active), which means the possibility of obtaining executable code for **XE/XL**, **PC** and every other platform for which **FPC** exists. **MP** is not a port of **FPC**; it has been written based on of **SUB-Pascal** (2009), **XD-Pascal** (2010), the author of which is [Vasiliy Tereshkov](mailto:vtereshkov@mail.ru).

Sources are on [GitHub](https://github.com/tebe6502/Mad-Pascal) with [release](https://github.com/tebe6502/Mad-Pascal/releases) for Windows operating system.

# History

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

