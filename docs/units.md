#

## [PROGRAM](https://www.freepascal.org/docs-html/ref/refse111.html#x232-25600016.1)

The `program` header is not required, it is provided only for backward compatibility with `Turbo Pascal`.

```
   program name [(parameters, ...)] [: address];
```

It is possible to specify the compilation address after the colon character `:`, this is equivalent to the command-line switch `-code address`.

```delphi
program test;

uses // List of unit dependencies goes here...
     
// Implementation of procedures, and functions goes here...

end.
```

## [UNIT](https://www.freepascal.org/docs-html/ref/refse111.html#x224-24600016.2)

The `UNIT` modules come only in the form of source `.pas` files, they cannot be compiled separately.

The `UNIT` modules consist of sections:

- `INTERFACE` **wymagana**
- `IMPLEMENTATION` **wymagana**
- `INITIALIZATION` *opcjonalna*.

```delphi
{
  Example UNIT
}
unit Unit1;

interface

uses // List of unit dependencies goes here...
     
// Interface section goes here

implementation

uses // List of unit dependencies goes here...

// Implementation of procedures, and functions goes here...

initialization

// Unit initialization code goes here...

end.
```

Example:
```delphi
unit test;

interface

type  TUInt24 =
  record
    byte0: byte;
    byte1: byte;
    byte2: byte;
  end;

const
  LoRes = 1;
  MedRes = 2;
  HiRes = 3;

  procedure Print(a: string);

implementation

uses test2;

procedure Print(a: string);
begin

  writeln(a);

end;

end.
```

## [LIBRARY](https://www.freepascal.org/docs-html/ref/refse117.html#x242-26600016.7)

The `library` header is required.

```
   library name [: address];
```

It is possible to specify the compilation address after the colon character `:`, this is equivalent to the command-line switch `-code address`.

The structure of the library is similar to the `unit` module, `program` program.


```delphi
{
  Example LIBRARY
}
library lib1;

uses // List of unit dependencies goes here...
     
// Implementation of procedures, and functions goes here...


// exported subroutine(s), variable(s)

exports

idents, ... ;

// optional library initialization code goes here...

begin

end.
```

By default, functions and procedures declared and implemented in the library are not available to a programmer who wants to use the library.

To make functions or procedures from the library available, they must be exported in the `exports` clause.

Functions, procedures and other identifiers are exported with the exact names specified in the `exports` clause.

To use libraries in `UNIT` modules or `PROGRAM` program, they must first be compiled and assembled, the **Mad Assembler-a** `-hm` switch must be active.

```DELPHI
mp.exe library.pas -ipath:<Mad_Pascal_path>\lib 
mads.exe library.a65 -hm -xi:<Mad_Pascal_path>\base
```

We cannot place `.pas` files with library source code in the `uses` clause.

To use the identifiers exported in `LIBRARY` we use the `EXTERNAL` modifier.


## [USES](https://wiki.freepascal.org/Uses)

The `uses` clause imports identifiers from `unit` modules.

Each **Mad-Pascal** unit - `program`, `unit`, or `library` - can have a maximum of one `uses` clause per section, which must appear immediately after the section headers. 

Section headers are `interface`, `implementation` in `unit` modules. There are no explicit section headers in `program` and `library`, so the `uses` clause appears immediately after the `program`, `library` header.

```delphi
    uses crt, sysutils, atari;
```

The `SYSTEM` module cannot be in this list, because it is always loaded by the compiler by default.

The order in which modules appear is important because it determines the order in which they are initialized. 
Modules are initialized in the same order in which they appear in the `uses` clause. 

Identifiers are searched for in reverse order, that is, when the compiler looks for an identifier, it looks for it first in the last module in the `uses` clause, then in the penultimate one, and so on.
This is important when two or more modules in the `uses` clause declare the same identifier. 

    uses graph, vbxe;

In both `GRAPH` and `VBXE` modules there is a `SetColor` and `Line` procedure, for the aforementioned example references to these procedures will be made by the `VBXE` module,

    uses vbxe, graph;

references to these procedures will be made by the `GRAPH` module.

We can also directly refer to the identifier from a specific module, such as:

```delphi
    vbxe.Line
    graph.Line
    vbxe.SetColor
    graph.SetColor
```

The compiler will look for source versions of all modules listed in the `uses` clause based on the path from which the `mp.exe` compiler was run.

Using the `IN` keyword, we can override the automatic module search mechanism.

```delphi
    uses unita in '..\unita.pas';
```

The `unita` module is searched for in the parent directory of the current compiler working directory. 
You can add a `{$UNITPATH ..}` directive to ensure that the module is found no matter where the current compiler working directory is.

When the compiler looks for module files, it adds the `.pas` extension to the module name.


## [$LIBRARYPATH](https://www.freepascal.org/docs-html/prog/progsu99.html)

```delphi
{$LIBRARYPATH path1; path2; ...}
```
The `$LIBRARYPATH` directive allows you to indicate additional search paths for `UNIT` modules declared by `uses`.

## [$UNITPATH](https://www.freepascal.org/docs-html/prog/progsu119.html)

```delphi
{$UNITPATH path1; path2; ...}
```
The `$UNITPATH` directive allows you to indicate additional search paths for `UNIT` modules declared by `uses`.
