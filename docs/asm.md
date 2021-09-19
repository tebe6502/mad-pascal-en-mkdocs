#

## ASM

Assembler blocks are not verified for syntax by the compiler, this is done only by **Mad Assembler**.

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
