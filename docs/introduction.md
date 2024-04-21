#

## Foreword

**Mad-Pascal** (MP) is a 32-bit **Turbo Pascal** compiler for **Atari XE/XL**. By design, it is compatible with the **Free Pascal Compilator** (FPC) (the `-MDelphi` switch should be active), which means the possibility of obtaining executable code for **XE/XL**, **PC** and every other platform for which **FPC** exists. **MP** is not a port of **FPC**; it has been written based on of **SUB-Pascal** (2009), **XD-Pascal** (2010), the author of which is [Vasiliy Tereshkov](mailto:vtereshkov@mail.ru).

A program that works on Atari might have problems on **PC** if, for example, the pointers have not been initialized with the address of a variable and the program attempts to write to the address `$0000` (memory protection fault). The strengths of **MP** include fast and convenient possibility of inclusion of inline assembly. A program using inline **ASM** does not work on platforms other than **XE/XL**. **MP** uses 64KB of primary memory; `TMemoryStream` provides usage of extended memory.
Variable allocation is static; there is no dynamic memory management. Parameters are passed to functions by value, variable or constant.

The available features are:

* `If` `Case` `For` `While` `Repeat` statements
* Compound statements
* `Label` `Goto` statements
* Arithmetic and boolean operators
* Procedures and functions with up to 8 parameters. Returned value of a function is assigned to a predefined `RESULT` variable
* Static local variables
* Primitive data types, all types except the `ShortReal`/`Real` type are compatible. Pointers are dereferenced as pointers to `Word`:
    * `Cardinal` `Word` `Byte` `Boolean`
    * `String` `PChar` `Char`
    * `Integer` `SmallInt` `ShortInt`
    * `Pointer` `File` `Text`
    * `ShortReal` `Real` [`fixed-point`](https://en.wikipedia.org/wiki/Fixed-point_arithmetic)
    * `Float` [`Single`](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)
    * [`Float16`](https://en.wikipedia.org/wiki/Half-precision_floating-point_format)
* One-dimensional and Two-dimensional arrays (with zero lower bound) of any primitive type. Arrays are treated as pointers to their origins (like in C) and can be passed to subroutines as parameters
* Predefined type string `[N]` which is equivalent to `array [0..N] of Char`
* `Type` aliases.
* `Records`
* `Objects`
* Separate program modules
* Recursion

## Folder Structure

In the folder **mp**, the follding files and subfolders are required:

```
  mp\
  mp.exe
     base\
     rtl_default.asm
     rtl6502_a8.asm
     rtl6502_c4p.asm
     rtl6502_c64.asm
     rtl6502_neo.asm
     rtl6502_raw.asm
          atari\
	  c4p\
	  c64\
	  common\
	  neo\
	  raw\
	  runtime\
     lib\
     aplib.pas
     atari.pas
     blowfish.pas
     c64.pas
     ...
     src\
         targets\
         crt.inc
         graph.inc
         system.inc
```

## Compilation

To compile the sources of **Mad-Pascal**, one may use **Delphi**, provided they happen to have installed **Delphi 7.0** or a later version.

A more cross-platform way is to use the Free Pascal Compiler (FPC), which can be downloaded from [freepascal.org](http://www.freepascal.org/).

Launch the installer and choose the folder for the installation of **FP**. It is crucial not to use the exclamation mark `!` or other nonstandard characters in the folder name. If it fails to compile any file, most probably, it is the fault of a nonstandard pathname. The command-line launching the compilation may look as follows (letter case in parameter names matters):

    fpc -Mdelphi -v -O3 mp.pas

* `-Mdelphi`     allows for Delphi format file compilation
* `-v`           shows all error and warning diagnostics
* `-O3`          performs code optimization

## Libraries

* [LIB](http://mads.atari8.info/library/doc/index.html)
* [BLIBS](https://bocianu.atari.pl/blog/blibs)

## Links

1. [Free Pascal Reference Guide](http://www.freepascal.org/docs-html/ref/ref.html#refch14.html)
2. [MadPascal AtariAge forum](http://atariage.com/forums/topic/240919-mad-pascal/)
3. [MadPascal examples](http://atariage.com/forums/topic/243658-mad-pascal-examples/)
4. [Atari XE/XL Pascal Compilers](https://atariwiki.org/wiki/Wiki.jsp?page=Pascal)
