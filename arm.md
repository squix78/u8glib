# U8glib with LPC1114FN28 ARM Microcontroller #

This page documents work and results making u8glib compatible with ARM microcontrollers.

# Reference Board #


I decided to build a small microcontroller board based on the NXP LPC1114FN28:
  * LPC1114FN28 (DIP28) Microcontroller
  * Simple USB to UART converter (lower left in the following picture)

![http://wiki.u8glib.googlecode.com/hg/otherpic/lpc1114_um230xb.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/lpc1114_um230xb.jpg)

The board as two buttons: Reset button at the upper right and the programming button at the lower edge of the board. The programming button connects pin PIO0\_1 to GND when pressed. Otherwise a pull up resistor will apply 3.3V to the pin.

The LPC1114 will be put into UART programming mode:
  1. Press and hold the programming button
  1. Press and release the reset button

# Tool Chain #

The tool chain is derived from the gcc-arm-embedded project https://launchpad.net/gcc-arm-embedded/. I will use "gcc-arm-none-eabi-4\_7-2013q1" for Linux.

The following files are required to generate a .hex file for the target controller LPC1114:
  1. GCC and related tools https://launchpad.net/gcc-arm-embedded/4.7/4.7-2013-q1-update/+download/gcc-arm-none-eabi-4_7-2013q1-20130313-linux.tar.bz2
  1. LPC11xx specific header files, located in `AN10995/CMSISv1p30_LPC11xx/inc` of the zip file from http://www.nxp.com/documents/application_note/AN10995.zip

The archive `gcc-arm-none-eabi-4_7-2013q1-20130313-linux.tar.bz2` contains the important linker (ld) script for the Cortex-M0 architecture in the folder `/share/gcc-arm-none-eabi/samples/ldscripts`:
```
linux:~/src/arm/gcc-arm-none-eabi-4_7-2013q1/share/gcc-arm-none-eabi/samples/ldscripts$ ls -al
drwxr-xr-x 2 kraus kraus 4096 Nov 14  2012 .
drwxr-xr-x 5 kraus kraus 4096 Dez  6 18:06 ..
-rw-r--r-- 1 kraus kraus  384 Mai 30 13:03 mem.ld
-rw-r--r-- 1 kraus kraus 2779 Aug 23  2012 sections.ld
-rw-r--r-- 1 kraus kraus 2724 Aug 23  2012 sections-nokeep.ld
```
For a plain minimal project, only `mem.ld` and `sections.ld` are required (`sections-nokeep.ld` will not work with U8glib). `mem.ld` must be updated for the target controller. In this case:
```
/* LPC1114 */
MEMORY
{
  FLASH (rx) : ORIGIN = 0x0, LENGTH = 0x8000 /* 32K */
  RAM (rwx) : ORIGIN = 0x10000000, LENGTH = 0x1000 /* 4K */
}
```

I have combinded the two .ld files into a single file: [ldscript.ld](http://code.google.com/p/u8glib/source/browse/sys/lpc11xx/plain/ldscript.ld). A complete project is placed here: http://code.google.com/p/u8glib/source/browse/#hg%2Fsys%2Flpc11xx%2Fplain.
The project is almost independent from the target controller. It contains:
  * Makefile
  * C-Code (main procedure)
  * ldscript

# Flash Tool #

`lpc21isp` from http://lpc21isp.sourceforge.net/ is a good flash tool also for the LPC1114. Commandline options are:
```
lpc21isp <hex file> <linux port> <baud rate> <clock speed in KHz>
```
Usually this will look like this:
```
lpc21isp my.hex /dev/ttyUSB0 38400 12000
```
Remember to put the device into UART programming mode for this command (see above). After download of the hex code, another reset will start the code.

# Target Specific Code #

LPC11xx specific geader files are located in `AN10995/CMSISv1p30_LPC11xx/inc` of the zip file http://www.nxp.com/documents/application_note/AN10995.zip.


# Blink Example Code #

There are tree different versions of the blink example code. The code should be portable across all ARM controllers except for the pin control, which is specific for the LPC11xx.
  * Blink with "for" loop: [blink](http://code.google.com/p/u8glib/source/browse/#hg%2Fsys%2Flpc11xx%2Fblink)
  * Blink with `SysTick` interrupt handler: [systickblink](http://code.google.com/p/u8glib/source/browse/#hg%2Fsys%2Flpc11xx%2Fsystickblink)
  * Blink with delay procedure (based on `SysTick` value): [delayblink](http://code.google.com/p/u8glib/source/browse/#hg%2Fsys%2Flpc11xx%2Fdelayblink)

# External Links #

http://vilaca.eu/lpc1114/