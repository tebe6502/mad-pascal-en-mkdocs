## Foreword

**Mad-Pascal** (MP) is a 32-bit **Turbo Pascal** compiler for **Atari 8-Bit** and other **MOS 6502 CPU**-based computers. By design, it is compatible with the **Free Pascal Compiler** (FPC) (the `-MDelphi` switch should be active). This means the possibility of obtaining executable code for **Atari 8-bit**, **Windows**, and every other platform for which **FPC** exists. **Mad-Pascal** is not a port of **FPC**. It has been written based on **SUB-Pascal** (2009) and **XD-Pascal** (2010), the author of which is [Vasiliy Tereshkov](mailto:vtereshkov@mail.ru).

**Mad-Pascal** uses 64KB of primary memory. The class `TMemoryStream` provides access to extended memory. A program that works on **Atari 8-Bit** might have problems on **Windows** and other platforms if, for example, the pointers have not been initialized with the address of a variable. Writing via an uninitialized pointer results in an attempt to write to the address `0x0` and causes a memory protection fault.

The strengths of **Mad-Pascal** include the fast and convenient possibility of including inline assembly. A program using inline **ASM** only works on platforms with **MOS 6502 CPU**.

Variable allocation is static. There is no dynamic memory management. Parameters are passed to functions by value, variable, or constant.

The available features are:

* `If` `Case` `For` `While` `Repeat` statements
* Compound statements
* `Label` `Goto` statements
* Arithmetic and boolean operators
* Procedures and functions with up to 8 parameters. The returned value of a function is assigned to a predefined `RESULT` variable
* Static local variables
* Primitive data types, all types except the `ShortReal`/`Real` type, are compatible. Pointers are dereferenced as pointers to `Word`:
    * `Cardinal` `Word` `Byte` `Boolean`
    * `String` `PChar` `Char`
    * `Integer` `SmallInt` `ShortInt`
    * `Pointer` `File` `Text`
    * `ShortReal` `Real` [`fixed-point`](https://en.wikipedia.org/wiki/Fixed-point_arithmetic)
    * `Float` [`Single`](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)
    * [`Float16`](https://en.wikipedia.org/wiki/Half-precision_floating-point_format)
* One-dimensional and Two-dimensional arrays (with zero lower bound) of any primitive type. Arrays are treated as pointers to their origins (like in C) and can be passed to subroutines as parameters
* Predefined type string `[N]`, which is equivalent to `array [0..N] of Char`
* `Type` aliases.
* `Records`
* `Objects`
* Separate program modules
* Separate library modules
* Recursion

## Folder Structure

In the folder **Mad-Pascal**, the following files and subfolders are required:

```
  MP\
    mp.exe
    base\
      atari\
      c4p\
      c64\
      common\
      neo\
      raw\
      runtime\    
      rtl_default.asm
      rtl6502_a8.asm
      rtl6502_c4p.asm
      rtl6502_c64.asm
      rtl6502_neo.asm
      rtl6502_raw.asm
    blibs\
    dlibs\
    include\
    lib\
    src\
    targets\
    wblibs\
```

## Compiling

To compile the sources of **Mad-Pascal** use the Free Pascal Compiler (FPC), which can be downloaded from [freepascal.org](http://www.freepascal.org/).

Launch the installer and choose the folder for the installation of **FPC**. It is crucial not to use the exclamation mark `!` or other nonstandard characters in the folder name. If it fails to compile any file, it is probably the fault of a nonstandard pathname. The command line launching the compilation may look as follows (letter case in parameter names matters):

    fpc -Mdelphi -v -O3 mp.pas

* `-Mdelphi`     allows for Delphi format file compilation
* `-v`           shows all error and warning diagnostics
* `-O3`          performs code optimization

## Libraries

* [LIB](http://mads.atari8.info/library/doc/index.html)
* [BLIBS](https://bocianu.atari.pl/blog/blibs)
* [WLIBS](https://github.com/Ripjetski6502/A8MadPascalLibrary)

## Links

1. [Free Pascal Reference Guide](http://www.freepascal.org/docs-html/ref/ref.html#refch14.html)
2. [MadPascal AtariAge forum](http://atariage.com/forums/topic/240919-mad-pascal/)
3. [MadPascal Examples](http://atariage.com/forums/topic/243658-mad-pascal-examples/)
4. [Atari 8-bit Pascal Compilers](https://atariwiki.org/wiki/Wiki.jsp?page=Pascal)
