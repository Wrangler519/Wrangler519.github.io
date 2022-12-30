---
title: 'About PIO'
date: 2019-02-11T19:27:37+10:00
weight: 5
---
PIO was used for the LED(mode indicator) and to drive the APDS9960 distance/motion sensor.

The general steps we programmed the PIO state machine are:

1. Determine which PIO instance to use(out of 2) PIO pio = pio0; PIO pio = pio1; 

2. Assign instructions into instruction memory with sufficient space uint offset = pio_add_program(pio, &program_name_here) 

3. Find an available state machine uint sm = pio_claim_unused_sm(pio, true); some_kind_of_program_init(pio, sm, offset, PICO_DEFAULT_LED_PIN); 
 
5. Up to this point, state machine is ready and running.



**PIO's advantages:**
1. With pio, we can effectively implement any protocol at our need for the I/O communication. It's far more powerful and convenient over bit-banging. If using bit-banging, it will continuously consumes the memory and kernel of the PC, while the computer has other tasks to do.  For slower protocols you might be able to use an IRQ to wake up the processor from what it was doing fast enough (though latency here is a concern) to send the next bit(s). But PC-class processors keep many hundreds of instructions in-flight on a single core at once, which has drawbacks when trying to switch rapidly between hard real time tasks. 

2. PIO has it's strict timestamps, each instruction takes exactly one cycle, so it make it easier for the timing when programming and gives more control to the programmer. 

3. PIO states machine runs independently from the main processor, it saves memory, efficiency and pins.

These features make PIO a unique asset for a microcontroller.


