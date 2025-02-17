# Interrupts

Two routines `GetIntVec` and `SetIntVec` are dedicated to managed the standard vectors for interrupts. You can use them to setup you own interrupt handlers and to restore the previous interrupts handlers.

The presence of the OS ROM during interrupts handling is required for proper operation of the following routines and code examples. So if you want disable the OS ROM, you have to use [$DEFINE ROMOFF](syntax/#romoff), to ensure properly setup OS interrupts vectors and handlers.

If we have disabled the OS ROM using `{$define romoff}` and are calling routines placed in the memory area `$C000..$FFFF` we must take care to set `PORTB` properly.

```delphi
procedure NewInterrupt; interrupt; assembler;
asm

    dec portb                  // Disable the OS ROM
    jsr user_proc_c000_ffff    // Call routine in RAM under the OS ROM
    inc portb                  // Enable the OS ROM

    ...                        // Interrupt-specific return logic, see below
end;
```

## NMIs - Vertical Blank Interrupt (VBL), Display List Interrupt (DLI)

### GetIntVec

    GetIntVec(iVBLI, pointer);	// Get the address of the immediate vertical blank interrupt handler (VVBLKI, $0222)
    GetIntVec(iVBLD, pointer);	// Get the address of the deferred vertical blank interrupt handler (VVBLKD, $0224)
    GetIntVec(iDLI, pointer);	// Get the address of the display list interrupt handler (VDSLST, $0200)

```delphi
var oldVBL: pointer;

begin
    GetIntVec(iVBLD, oldVBL);   // Remeber old vector to restore it later
end.
```

### SetIntVec

    SetIntVec(iVBLI, pointer);	// Set the address of the immediate vertical blank interrupt handler (VVBLKI, $0222)
    SetIntVec(iVBLD, pointer);	// Set the address of the deferred vertical blank interrupt handler (VVBLKD, $0224)
    SetIntVec(iDLI, pointer);	// Set the address of the display list interrupt handler (VDSLST, $0200)

### Immediate Vertical Blank Interrupt

The **VBLI** (vertical blank immediate) interrupt handler is terminated by jumping to the `SYSVBV` address ($E45F). It will perform the standard tasks of the immediate vertical blank interrupt and restore the values of the `A`, `X`, `Y` **CPU6502** registers from the stack before it returns.

```delphi
procedure NewVBLI; interrupt; assembler;
asm
    jmp sysvbv
end;


begin
    SetIntVec(iVBLI, @NewVBLI);
end.
```

### Deferred Vertical Blank Interrupt

The **VBLD** (vertical blank deferred) interrupt handler is terminated by jumping to the `XITVBV` address ($E462) which will restore the value of the `A`, `X`, `Y` **CPU6502** registers from the stack before it returns.

```delphi
procedure newVBLD; interrupt; assembler;
asm
    // Your code
    jmp xitvbv
end;


begin
    SetIntVec(iVBLD, @newVBLD);
end.
```

### Display List Interrupt

As opposed to the vertical blank interrupt handler, which save the values of the `A`, `X`, `Y` **CPU6502** registers before the interupt vector is called, the display list interrupt handler only saves the `A` **CPU6502** register to the stack. Therefore the **iDLI** (display list) interrupt handle is termianted with single `PLA` instruction.

```delphi
procedure NewDLI; interrupt; assembler;
asm
    // Your code
    pla
end; // Will become RTI


begin
    SetIntVec(iDLI, @NewDLI);
end.
```


## IRQs - TIMER1, TIMER2, TIMER4

### GetIntVec

    GetIntVec(iTIM1, pointer);	// Get the address of the TIMER 1 interrupt handler (VTIMR1, $0210)
    GetIntVec(iTIM2, pointer);	// Get the address of the TIMER 2 interrupt handler (VTIMR2, $0212)
    GetIntVec(iTIM4, pointer);	// Get the address of the TIMER 4 interrupt handler (VTIMR4, $0214)

```delphi
var oldIRQ: pointer;

begin
    GetIntVec(iTIM4, oldIRQ);
end.
```

### SetIntVec

    SetIntVec(iTIM1, pointer);	// Set the address of the TIMER 1 interrupt handler (VTIMR1, $0210)
    SetIntVec(iTIM2, pointer);	// Set the address of the TIMER 2 interrupt handler (VTIMR2, $0212)
    SetIntVec(iTIM4, pointer);	// Set the address of the TIMER 4 interrupt handler (VTIMR4, $0214)

```delphi
procedure TimerIRQ; assembler; interrupt;
asm
    // Your code
    pla
end; // Becomes RTI

begin
    SetIntVec(iTIM4, @TimerIRQ, 0, 28);
    repeat until keypressed;

    SetIntVec(iTIM4, oldIRQ);
end.
```

When the system executes a jump to an IRQ interrupt handler, it puts the contents of the accumulator on the stack beforehand.
Keep this in mind and end the interrupt handler with a single `PLA` instruction.

Additional parameters are required to trigger a new **IRQ** interrupt, such as the choice of base clock `clock_base = [0,1]` and frequency `rate = [6.255]`.
Values of `rate` less than `6` will cause the system to slow down severely, up to a possible suspension.

    SetIntVec(iTIM1, pointer, clock_base, rate);
    SetIntVec(iTIM2, pointer, clock_base, rate);
    SetIntVec(iTIM4, pointer, clock_base, rate);
