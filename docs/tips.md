#

## FOR

The counter value at the end of the `FOR` iterative instruction in **FPC** will be equal to the value that was specified for the maximum counter value. In the case of **MP**, the value will be larger by `+1`.

Example:
```delphi
for i:=0 to 10 do;
```

**FPC** at the end of the loop `i = 10', **MP** `i = 11'


## PARAMETERS OF FUNCTIONS, PROCEDURES

For the following example, **FPC** will generate a different result than **MP**.

```delphi
var i: byte;

function ran(a: smallint): byte;
begin

 ran := i;

 inc(i, 3+a);

end;

procedure kefrens(a,b: byte);
begin

 writeln(a);
 writeln(b);

end;


begin

Kefrens(ran(5)+3, ran(3)+5);
```

**FPC**, **Delphi** calculates the parameters of a procedure/function from right to left (result for the above example `9`, `5`).

**MP** calculates procedure/function parameters from left to right (result for above example `3`, `13`)


## STRINGS IN MEMORY

```delphi
 writeln('ala','ma','kota');
 writeln('ala','ma','psa');
```

The compiler will only put back the character strings `ala`, `ma` once in memory. By breaking a longer string into smaller pieces, we can save memory.


## CHARS IN MEMORY

```delphi
writeln(#69,#82,#82,#32, a);
```

Character codes separated by a comma will not be treated as strings that the compiler writes to constants.


## SHORTER BOOLEAN TERMS

```delphi
 if spanbelow = true then ;
```

can be replaced by

```delphi
 if spanbelow then ;
```

## INFINITE LOOP

When assembling a *.a65 file causes an 'Infinite loop', the OBX file is saved but is corrupted.

To get rid of this situation, set `DATAORIGIN' (-data:ADDRESS) hard.

## [USES](../moduly/#uses)

The order of the modules in the `USES` list can make a difference.
