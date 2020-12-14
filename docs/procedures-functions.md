#

## [Procedure](https://www.freepascal.org/docs-html/ref/refch14.html#x173-19500014)

**MP** allows up to 8 parameters to be transferred to the procedure. There are three ways to pass parameters - by value, constant `CONST` and variable `VAR`. It is possible to use the `OVERLOAD` modifier to overload procedures.

Available procedure modifiers: `OVERLOAD` `ASSEMBLER` `FORWARD` `REGISTER` `INTERRUPT` `PASCAL`.

It is possible to recurse procedures, provided that the procedure parameters will be passed by value and will be of a simple - ordinal type. The record or pointer type will not be properly allocated in memory.

## [Function](https://www.freepascal.org/docs-html/ref/refch14.html#x173-19500014)

**MP** allows you to transfer up to 8 parameters to the function. There are three ways to pass parameters - by value, constant `CONST` and variable `VAR`. We return the result of the function by assigning it to the function name or using the automatically declared `RESULT` variable, e.g:

```delphi
function add(a,b: word): cardinal;
begin
  Result := a+b;
end;

function mul(a,b: word): cardinal;
begin
  mul := a*b;
end;
```

Available function modifiers: `OVERLOAD` `ASSEMBLER` `FORWARD` `REGISTER` `INTERRUPT` `PASCAL`, *INTERRUPT* not recommended for functions.

It is possible to recurse functions, provided that the function parameters will be passed by value and will be of a simple - ordinal type. The record or pointer type will not be properly allocated in memory.

## Modifiers

### `assembler`

The **procedures/functions** marked by `ASSEMBLER` can only consist of an **ASM** block. The compiler does not analyze the syntax of such blocks, treats them as a comment, possible errors are caught only during the assembly.

```delphi
procedure color(a: byte); assembler;
asm
{   mva a 712
};
end;
```

### `overload`

Overloaded **procedures/functions** are recognized by the parameter list.

```delphi
procedure sum(var i: integer; a,b: integer); overload;
begin
  i := a+b;
end;

procedure sum(var i: integer; a,b,c: integer); overload;
begin
  i := a+b+c;
end;

function fsum(a,b: word): cardinal; assembler; overload;
asm
{
  adw a b result
};
end;

function fsum(a,b: real): real; overload;
begin
  Result := a+b;
end;
```

### `forward`

If you want the **procedure/function** to be declared after its first call, use the `FORWARD` modifier.

```delphi
procedure name [(formal-parameter-list)]; forward;

...
...
...

procedure name;
begin
end;
```

### `register`

Using `REGISTER` modifier causes the first three formal parameters of the **procedure/function** to be placed on the zero page, in 32-bit general-purpose registers `EDX`, `ECX`, `EAX` respectively.

```delphi
procedure name (a,b,c: cardinal); register;

// a = edx
// b = ecx
// c = eax
```

### `interrupt`

**Procedures/Functions** marked by `INTERRUPT` end with `RTI` instruction (instead of standard `RTS`). Regardless of whether such **procedure/function** is called in the program, the compiler always generates code for it. It is recommended to use the **ASM** block for such **procedure/function**, otherwise the **Mad Pascal** software stack will be destroyed, which may lead to unstable program operation, including computer crashes. At the beginning of the **procedure/function** marked by `INTERRUPT`, the programmer must take care to keep the **CPU** registers `A` `X` `Y`, at the output to restore such registers, the compiler only inserts the final `RTI` command.

```delphi
procedure dli; interrupt;
asm
{   pha

    lda #$c8
    sta wsync
    sta $d01a

    pla
};
end;             // the RTI instruction gets inserted automatically
```

### `pascal`
