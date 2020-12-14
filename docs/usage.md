#

## Compiler switches

```bash
Syntax: mp source [switches]

-diag           diagnostic mode
-define:symbol  defines a symbol
-ipath:<x>      dadditional search path
-target:<x>     terget system: a8 (default), c64
-code:address   program launch address
-data:address   memory address of variables and arrays
-stack:address  address of stack (64 bytes)
-zpage:address  address of variables in the zero page (26 bytes)
```

The use of the `-diag` switch causes the generation of an additional file with information about all used variables, procedures, and functions.

The default extension of output file is `*.A65`, assembled using the **Mad-Assembler**, additionally the search path is set using `-i:base`, for example:

    mads source.a65 -x -i:base

The `-x` switch **Exclude unreferenced procedures** allows for the generation of shortest output code for the **6502**.

## Exit codes

    3 = bad parameters, compiling not started
    2 = error occured
    0 = no errors

Warning diagnostics do not affect the exit code.
