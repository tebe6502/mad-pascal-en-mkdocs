#

## [UNIT](https://www.freepascal.org/docs-html/ref/refse111.html#x224-24600016.2)

The modules `UNIT` in **MP** consist of sections `INTERFACE` **required**, `IMPLEMENTATION` **required**, `INITIALIZATION` *optional*.

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

## [USES](https://wiki.freepascal.org/Uses)

Use the `USES` statement to declare the selected module, for example:

    uses crt, sysutils, atari;

The modules are read from the end of the `USES` list (from right to left), for the above example the default is `SYSTEM` first, then `ATARI` `SYSUTILS` `CRT`.

The order of modules in the `USES` list can make a difference when using procedures/functions with the same names, subsequent modules cover the previous ones e.g:

    uses graph, vbxe;

In both `GRAPH` and `VBXE` modules there is a `SetColor` and a `Line` routine, for the above example the calls to these routines will be executed by the `GRAPH` module.

In case

    uses vbxe, graph;

references to procedures will be made by the VBXE module.

We can also directly call a procedure/function from a specific module, such as:

    vbxe.Line
    graph.Line
    vbxe.SetColor
    graph.SetColor
    