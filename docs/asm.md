#

## ASM

Inline assembler blocks are not verified for syntax by the compiler, this is done only by **Mad-Assembler**.

> **WARNING:**  
> _It is required to maintain the state of the `X` `CPU6502` register, which is used to operate the **MP** software stack._

The compiler allows two syntaxes for the `ASM` block, with { } brackets as for a comment and the standard one without brackets.

```delphi
ASM
  lda #10
  sta 712
END;
```

```delphi
ASM
{  lda #10
   sta 712
};
```

```delphi
procedure name; assembler;
asm
  lda #10
  sta 712
end;
```

```delphi
procedure name; assembler;
asm
{
  lda #10
  sta 712
};
end;
```

## $LINK

```Delphi
{$link filename}
```

The compiler directive `{$link filename}` allows you to attach a relocatable file from **Mad-Assembler** to a compiled **MP** program.

```Delphi
	.reloc

.extrn edx .dword

.extrn	print .proc (.dword edx) .var

.public	prc


.proc	prc (.dword a .dword b .dword c) .var

.var a,b,c .dword

	print a
	print b
	print c

	rts

.endp
```

In the above example, we use the `PRINT` procedure, which is defined in **MP**.

```Delphi
uses crt;


procedure prc(a,b,c: integer); external;


procedure print(value: dword); keep; register;
begin

 writeln(value);

end;


{$link test.obx}	// link PRC procedure


begin

 prc(11, 347, 321785);

 repeat until keypressed;

end.
```

From the assembler level we have access to **MP** procedures but only those marked with the modifier `REGISTER`, i.e. those whose parameters are passed through the program registers `EDX`, `ECX`, `EAX` (we are limited to a maximum of three parameters).

The `KEEP` modifier forces a procedure to remain in the compiled code regardless of whether its use has occurred or not (normally procedures/functions that are not used are eliminated).

**MP**, on the other hand, has access to procedures from the linked assembler file, whose parameters are passed through variables, modifier `.VAR`.

```Delphi
.proc	prc (.dword a .dword b .dword c) .var
```

In **Mad-Assembler** relocatable program, we need an additional declaration of the external symbols `EDX`, `ECX`, `EAX`.

```Delphi
.extrn edx, ecx, eax .dword
```

The **MP** procedure itself, which we want to access from the assembler level, is declared as an external procedure with parameters denoting program registers `EDX`, `ECX`, `EAX`.

For more information on the `REGISTER` modifier and the order in which parameters are allocated in program registers, see [Procedures and functions](../procedures-functions/#register).

```Delphi
.extrn	print .proc (.dword edx) .var
```

We will access the `PRC` procedure from the **MP** level by making it public via the `.PUBLIC` assembler directive.

```Delphi
.public	prc
```

After assembling our sample relocatable assembler program `TEST.ASM`, we get the file `TEST.OBX`, which we can link to the **MP** program with the `{$LINK}` directive.

```Delphi
{$link test.obx}
```
