#

## FOR

The counter value at the end of the `FOR` iterative instruction in **FPC** will be equal to the value that was specified for the maximum counter value. In the case of **Mad-Pascal**, the value will be larger by `+1`.

Example:
```delphi
for i:=0 to 10 do;
```

**FPC** at the end of the loop `i = 10', **Mad-Pascal** `i = 11'


## SHL

**FPC** provides other results for SHL that exceeds the size of the type, such as:

```delphi
i: byte;
c: cardinal;

i:=1;
c:=i shl 33;
```

For the above example, **FPC** will return a value of 2, **Mad-Pascal** will return 0.

Whereas for:
```delphi
c:=1 shl 33;
```

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
