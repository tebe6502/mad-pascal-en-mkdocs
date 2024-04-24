## Compiler Options

```bash
Syntax: mp <inputfile>.pas [options]

-ipath:<folder>    Add the folder <folder> to the unit include path
-define:<symbol>   Define the symbol <symbol>
-cpu:<cpu>         Specify the CPU mode: 6502 (default), 65c02, 65816
-target:<platform> Specify the target platform: a8 (default), c4p, c64, neo, raw, x16
-code:<address>    Specify the memory start address for the code
-data:<address>    Specify the memory start address for variables and arrays
-stack:<address>   Specify the memory start address for the software stack (64 bytes required)
-zpage:<address>   Specify the memory start address of variables in the zero page (26 bytes required)
-o:<outputfile>    Specify the output file path (default <inputfile>.a65)
-diag              Activate diagnostics mode
```

The unit include path must contain the **Mad-Pascal** folder `lib` which contains the standard Pascal libraries.
Additional optional standard libraries are in the `blib`, `dlib` and `wlib` folders.
 
    mp.exe example.pas -ipath:<MadPascalPath>\lib -ipath:<MadPascalPath>\blib

The `-target` option supports the following values for the target platform:
 * a8  - [Atari 8-bit computers](https://en.wikipedia.org/wiki/Atari_8-bit_computers). This is the default if the option is not specified.
 * c4p - [Commodore Plus/4 computers](https://en.wikipedia.org/wiki/Commodore_Plus/4)
 * c64 - [Commodore C64 computers](https://en.wikipedia.org/wiki/Commodore_64)
 * neo - [Neo6502 computers](https://github.com/OLIMEX/Neo6502)
 * raw - Raw binary output without header.
 * x16 - [Commander X16 computers](https://www.commanderx16.com)

The `-diag` option activates the generation of an additional `*.txt` file with information about all used variables, procedures, and functions.

The default output file name is `<inputfile>.a65`. It must be assembled using **Mad-Assembler**. The assembler include path must contain the **Mad-Pascal** assembler base folder using, for example:

    mads example.a65 -x -i:<MadPascalPath>\base

Using the `-x` option to **Exclude unreferenced procedures** is mandatory. It ensures that only the used parts of the libraries are compiled and the resulting **MOS 6502** object code has the minimum size.

## Exit Codes

    0 = No errors occurred, the output files were created correctly
    2 = Errors occurred, and compiling was aborted
    3 = Wrong parameters were specified, and compiling was not started

Warning messages issued by **Mad-Pascal** do not affect the exit code.
