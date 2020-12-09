#

## Scripts

### Linux

#### mp-build-a8

```bash
#!/bin/bash

mp="$HOME/Programs/MadPascal/mp"
mads="$HOME/Programs/mads/mads"
base="$HOME/Programs/MadPascal/base"

if [ -z "$1" ]; then
  echo -e "\nPlease call '$0 <argument>' to run this command!\n"
  exit 1
fi

name=${1::-4}

$mp $name.pas -o

if [ -f $name.a65 ]; then
  [ ! -d "output" ] && mkdir output
  mv $name.a65 output/
  $mads output/$name.a65 -x -i:$base -o:output/$name.xex
else
  exit 1
fi

if [ ! -z "$2" ]; then
  atari800 output/$name.xex
fi
```

    mp-build-a8 main.pas r


#### mp-build-c64

```bash
#!/bin/bash

mp="$HOME/Programs/MadPascal/mp"
mads="$HOME/Programs/mads/mads"
base="$HOME/Programs/MadPascal/base"

if [ -z "$1" ]; then
  echo -e "\nPlease call '$0 <argument>' to run this command!\n"
  exit 1
fi

name=${1::-4}

$mp $name.pas -t c64 -z 10 -o

if [ -f $name.a65 ]; then
  [ ! -d "output" ] && mkdir output
  mv $name.a65 output/
  $mads output/$name.a65 -x -i:$base -o:output/$name.prg
else
  exit 1
fi

if [ ! -z "$2" ]; then
  x64 output/$name.prg
fi
```

    mp-build-c64 main.pas r

## Atari 8-bit

### Hello World

```delphi
program HelloWorld;

uses crt;

begin
  writeln('Hello World');
  readkey;
end.
```

## C64

### Test

```delphi
// https://bitbucket.org/paul_nicholls/pas6502/src/master/projects/pas6502_test.dpr

program Test;
const
  cScreen0 = 1024;
  cColor   = $d800;

var
  border     : Byte absolute $D020;
  background : Byte absolute $D021;

  screen0    : array[0..1000-1] of Byte absolute cScreen0;
  color0     : array[0..1000-1] of Byte absolute cColor;
  i          : Integer;

begin
  i := 0;
  while i < 1000 do begin
    // fill screen with all screen codes (wrapping around).
    screen0[i] := i;

    // fill color RAM with all colors
    color0[i] := i;

    Inc(i);
  end;
end.
```