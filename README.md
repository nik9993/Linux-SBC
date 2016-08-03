# Linux-SBC
Rough documentation of AT91SAM9N12 based SBC

#Status
Right now there are 3 errors on the Power Managment Circuit, The 3v3 LDO needs to be soldered standing up to avoid the pad on the back, or this will cause a short. Also the 1v and 1v8 LDO need to have a pull up jumper sodered to their third pin. This will enable the voltage regulation. Once those two problems have been solved, then you can power the Processor circuit.

As of right now the processor is not booting up. It is keeping the SHDN line High and pulling the NRST Line Low. Currently investigating.

#Boot Process
Right now the Boot Process is held up at the Shutdown Controller (SHDWC). The SHDN line is being held high and NRST is being held low meaning that the Reset Controller in the processor never releases the reset line.

![alt text](https://github.com/nik9993/Linux-SBC/blob/master/images/Power-Up%20Reset.png "Power Up Boot Process")

This could be due to insufficient POR Output or just that the processor never goes through startup to initialize the crystals.

#Expected Boot Process
Once the processor boots, I am expecting to connect the usb slave to a windows computer and windows should recognize a USB CDC device. At that point it will as for a driver. once that happens I will use the SAMBA tool to load the bootloader and other files onto the board.


This Board is based off of 2 previous boards created by [hak8or](https://github.com/hak8or) and [henrik](https://github.com/Ttl), you can see their projects [here](https://github.com/nik9993/Embedded-Linux-System/tree/master/at91sam9n12) and [here](https://github.com/nik9993/sam_board), respectivley.
