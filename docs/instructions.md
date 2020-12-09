#

## conditional

### case of else

Currently, **Mad Pascal** only accepts types with a length of 1 byte for the `CASE` variable: `SHORTINT` `BYTE` `CHAR` `BOOLEAN`.

```delphi
case a of               // dla zmiennej A typu CHAR
  'A'..'Z': begin end;
  '0'..'9': begin end;
  '+','*': begin end;
end;
```

### if then else

`IF` conditional instructions can be nested. This is used for more complex conditions.

## iterative

### [for to downto do](https://www.freepascal.org/docs-html/ref/refsu57.html)

```delphi
FOR variable := { initial value } TO { final value } DO { instructions to execute }
FOR variable := { final value } DOWNTO { initial value } DO { instructions to execute }
```

This instruction is used to organize calculations which are performed a predetermined number of times. The control variable shall be an identifier of the ordinal type and both expressions shall be consistent in terms of assignment with the control variable type. During the `TO` loop execution, the control variable is assigned the subsequent value in the given type, in the `DOWNTO` loop, the preceding one. It is prohibited to "manually" change the value of a control variable. In case of such an attempt, **MP** does not signal an error.

The compiler makes sure that there is no endless loop so that you can use such a loop without a doubt:

```delphi
for i:=0 to 255 do writeln(i);    // for a variable I of type BYTE
```

### while do

```delphi
while { condition } do { instructions to execute }
```

This construct is used to organize calculations that will be performed as long as the expression after the word `WHILE` is true. Such a loop may not be executed even once.

```delphi
while BlitterBusy do;   // waiting for the VBXE blitter to finish
```
Limitations for `WHILE` instructions:

```delphi
while i<=255 do inc(i); // pętla bez końca gdy zmienna I typu BYTE
```

### [repeat until](https://www.freepascal.org/docs-html/ref/refsu59.html)

```delphi
repeat
  { instructions to execute }
until { termination condition }
```

This statement cyclically executes other statements between `REPEAT` and `UNTIL` until the expression after `UNTIL` takes the value of `TRUE`.

The effect of the `REPEAT` loop is very similar to that of the `WHILE` loop. This loop can also be performed a huge number of times. The only difference is that in the REPEAT loop the end condition is only checked after the instruction is executed. This means that the `REPEAT` loop will always be done at least once. Only after this iteration will the program check if the loop can be terminated. In the case of the `WHILE` loop, the condition is checked immediately before it is executed, which may result in the loop never being executed.

```delphi
i:=0;
repeat
  inc(i);
until i=0;      // pętla wykona się 256 razy
```
