# Linux-SBC
Rough documentation of AT91SAM9N12 based SBC

![](https://github.com/nik9993/Linux-SBC/blob/master/images/RevB.png "RevB")

#Status
Right now there are 3 errors on the Power Managment Circuit, The 3v3 LDO needs to be soldered standing up to avoid the pad on the back, or this will cause a short. Also the 1v0 and 1v8 LDO need to have a pull up jumper sodered to their third pin. This will enable the voltage regulation. Once those two problems have been solved, then you can power the Processor circuit.

![](https://github.com/nik9993/Linux-SBC/blob/master/images/power%20fixes.jpg "Power Fixes")

Even when the voltage regulators are working properly the 1v and 1v8 LED barely light up, this is due to the low voltage being supplied, it does not have enough difference to light the LED, however, by checking the LDOs' output with a multimeter, I can tell that they are, in fact, working as intended.

Also the NAND on the Back was removed because the pitch on the component is just a hair smaller than the board, this causes a short in the NAND, so it is removed for the time being.

As of right now the processor is not booting up. It is keeping the SHDN line High and pulling the NRST Line Low.

#Boot Process
Right now the Boot Process is held up at the Shutdown Controller (SHDWC). The SHDN line is being held high and NRST is being held low meaning that the Reset Controller in the processor never releases the reset line.

![alt text](https://github.com/nik9993/Linux-SBC/blob/master/images/Power-Up%20Reset.png "Power Up Boot Process")

This is due to the LDO's not coming up at the right time. The 3v3 LDO comes up first, and enables the other two LDO's, however, the 1v0 LDO is coming up at 100us while the 1v8 LDO is coming up at 400us. This causes the core voltage to come up before the processor is ready for it which in turn causes the reset controller to never boot up the processor.

#Expected Boot Process
Once the processor boots, I am expecting to connect the usb slave to a windows computer and windows should recognize a USB CDC device. At that point it will as for a driver. once that happens I will use the SAMBA tool to load the bootloader and other files onto the board.


This Board is based off of 2 previous boards created by [hak8or](https://github.com/hak8or) and [henrik](https://github.com/Ttl), you can see their projects [here](https://github.com/hak8or/Embedded-Linux-System/tree/master/at91sam9n12) and [here](https://github.com/ttl/sam_board), respectivley.
