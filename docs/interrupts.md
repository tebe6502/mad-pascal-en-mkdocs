#

## VBL, DLI

Two routines `GetIntVec` and `SetIntVec` are dedicated to handle **VBL**, **DLI** interrupts. The presence of OS is required for proper operation (disable ROM only by [$DEFINE ROMOFF](/composition/#romoff))

### GetIntVec

    GetIntVec(iVBL, pointer);	// getting VBL interrupt service program address ($0224)
    GetIntVec(iDLI, pointer);	// getting DLI interrupt service program address ($0200)

```delphi
var oldVBL: pointer;

begin

GetIntVec(iVBL, oldVBL);

end.
```

### SetIntVec

    SetIntVec(iVBL, pointer);	// set address of VBL interrupt handler ($0224)
    SetIntVec(iDLI, pointer);	// set address of DLI interrupt handler ($0200)

```delphi
procedure newVBL; interrupt; assembler;
asm

 jmp xitvbv

end;


begin

SetIntVec(iVBL, @newVBL);

end.
```

The **VBL** interrupt is terminated by jumping to the `XITVBV` address ($E462) which will restore the value of the `A` `X` `Y` **CPU6502** registers.


## IRQ - TIMER1, TIMER2, TIMER4

Two routines `GetIntVec` and `SetIntVec` are dedicated to handle **IRQ** - **TIMER1**, **TIMER2**, **TIMER4** interrupts. The presence of OS is required for proper operation (disable ROM only by [$DEFINE ROMOFF](/composition/#romoff))

### GetIntVec

    GetIntVec(iTIM1, pointer);	// getting the address of the TIMER 1 interrupt handler ($0210)
    GetIntVec(iTIM2, pointer);	// getting the address of the TIMER 2 interrupt handler ($0212)
    GetIntVec(iTIM4, pointer);	// getting the address of the TIMER 4 interrupt handler ($0214)

```delphi
var oldIRQ: pointer;

begin

GetIntVec(iTIM4, oldIRQ);

end.
```

### SetIntVec

    SetIntVec(iTIM1, pointer);	// establishing the address of the TIMER 1 interrupt handler ($0210)
    SetIntVec(iTIM2, pointer);	// establishing the address of the TIMER 2 interrupt handler ($0212)
    SetIntVec(iTIM4, pointer);	// establishing the address of the TIMER 4 interrupt handler ($0214)

```delphi
procedure irq; assembler; interrupt;
asm

 pla

end;

begin

SetIntVec(iTIM4, @irq, 0, 28);

repeat until keypressed;

SetIntVec(iTIM4, oldIRQ);

end.
```

When the system executes a jump to an interrupt service routine, it puts the contents of the accumulator on the stack beforehand; keep this in mind and end the interrupt service with `PLA`.

Additional parameters are required to trigger a new **IRQ** interrupt, such as the choice of base clock `clock_base = [0,1]` and frequency `rate = [6.255]`. Values of `rate` less
than `6` will cause the system to slow down severely, up to a possible suspension.

    SetIntVec(iTIM1, pointer, clock_base, rate);
    SetIntVec(iTIM2, pointer, clock_base, rate);
    SetIntVec(iTIM4, pointer, clock_base, rate);
