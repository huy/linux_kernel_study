## Interrupt and exception


Exceptions aka “Synchronous interrupts” are produced by the CPU control unit while executing instruction, the control
unit issues them after terminating the execution of an instruction. E.g. are divide by zero or trap. Programmed exception is used to implement syscal and debug.

Interrupts aka “Asynchronous interrupts” are generated by other hardware devices at arbitrary times with respect to the
CPU clock signals. APIC - Advanced Programmable Interrupt Controller.

There is table of 256 of 8 bytes interrupt descriptors. Each corresponds with one address of interrupt or exception
handler. Interrupt Descriptor Table (IDT) can be located in any place in memory, its address and length is stored in register idtr. The table is initialized using lidt assembly language.

There are 3 types of descriptors

1. task gate
2. interrupt gate
3. trap gate

**References**

* http://linux.linti.unlp.edu.ar/images/0/0c/ULK3-CAPITULO4-UNNOBA.pdf
