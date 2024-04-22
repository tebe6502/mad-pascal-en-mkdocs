#

## ASM

The compiler allows two syntaxes for Inline assembler blocks: The `ASM` block, with { } brackets as for a comment and the standard one without brackets. The syntax of the code inside an assembler block is not verified by the compiler. This is done only by **Mad-Assembler** during the assembly of the `*.a65` output file.

> **WARNING:**
The **MOS 6502 CPU** register `X` is used to operate the **Mad-Pascal** software stack. Therefore an assembler block must restore the original value of `X` at the end of the block, if the register is modified by the block.

```Delphi
ASM
  lda #10
  sta 712
END;
```

```Delphi
ASM
{  lda #10
   sta 712
};
```

```Delphi
procedure name; assembler;
asm
  lda #10
  sta 712
end;
```

```Delphi
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

The compiler directive `{$link filename}` allows you to attach a relocatable file from **Mad-Assembler** to a compiled **Mad-Pascal** program.

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

In the above example, we use the `PRINT` procedure, which is defined in **Mad-Pascal**.

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

From the assembler level we have access to **Mad-Pascal** procedures but only those marked with the modifier `REGISTER`, i.e. those whose parameters are passed through the program registers `EDX`, `ECX`, `EAX` (we are limited to a maximum of three parameters).

The `KEEP` modifier forces a procedure to remain in the compiled code regardless of whether its use has occurred or not (normally procedures/functions that are not used are eliminated).

**Mad-Pascal**, on the other hand, has access to procedures from the linked assembler file, whose parameters are passed through variables, modifier `.VAR`.

```Delphi
.proc	prc (.dword a .dword b .dword c) .var
```

In **Mad-Assembler** relocatable program, we need an additional declaration of the external symbols `EDX`, `ECX`, `EAX`.

```Delphi
.extrn edx, ecx, eax .dword
```

The **Mad-Pascal** procedure itself, which we want to access from the assembler level, is declared as an external procedure with parameters denoting program registers `EDX`, `ECX`, `EAX`.

For more information on the `REGISTER` modifier and the order in which parameters are allocated in program registers, see [Procedures and functions](../procedures-functions/#register).

```Delphi
.extrn	print .proc (.dword edx) .var
```

We will access the `PRC` procedure from the **Mad-Pascal** level by making it public via the `.PUBLIC` assembler directive.

```Delphi
.public	prc
```

After assembling our sample relocatable assembler program `TEST.ASM`, we get the file `TEST.OBX`, which we can link to the **Mad-Pascal** program with the `{$LINK}` directive.

```Delphi
{$link test.obx}
```
