# Linux-SBC
Rough documentation of AT91SAM9N12 based SBC

#Status
Right now there are 3 errors on the Power Managment Circuit, The 3v3 LDO needs to be soldered standing up to avoid the pad on the back, or this will cause a short. Also the 1v and 1v8 LDO need to have a pull up jumper sodered to their third pin. This will enable the voltage regulation. Once those two problems have been solved, then you can power the Processor circuit.

As of right now the processor is not booting up. It is keeping the SHDW line High and pulling the NRST Line Low. Currently investigating.
