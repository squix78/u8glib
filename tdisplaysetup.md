

# Tutorial: How to connect a display #

  * How to connect a display to the Arduino board?


## Parallel or Serial ##

Currently U8glib supports parallel (6800) and serial (SPI) interfaces. If both are available, the serial interface might be better, because much less pins and wires are required.

## 3.3 Volt Graphics Displays ##

Some graphics boards only use 3.3 volt. The digital ports of such a graphics board must not be connected directly to the Arduino Board. Use a level translation (e.g. 74HC4050) between Arduino Board and graphics display.

As an example, here is a simplified picture from the dogm128 project:
![http://wiki.dogm128.googlecode.com/hg/dogm_block.jpg](http://wiki.dogm128.googlecode.com/hg/dogm_block.jpg)

## Example: SPI Interface ##

For U8glib any pins of the Arduino Board can be used. U8glib only need to know which pin is connected to which pin of the graphics display.
A graphics devices with SPI usually has four important lines:
  * Clock (sck)
  * Data-In (mosi)
  * Chip-Select (cs)
  * Command/Data selection (a0)
  * Optional: Reset line

The pin numbers must be assigned to the U8GLIB constructor (using the NHD27OLED\_BW as an example):
```
U8GLIB_NHD27OLED_BW(uint8_t sck, uint8_t mosi, uint8_t cs, uint8_t a0, uint8_t reset = U8G_PIN_NONE) 
```

This will lead to code in the `.pde` file which looks like this:
```
U8GLIB_NHD27OLED_BW u8g(13, 11, 10, 9); 
```
This will tell U8glib, that the clock line is at pin 13, the data line at pin 11, the chip select at pin 10 and the command selection line at pin 9.

## Select U8glib constructor ##

There are a lot of different graphics displays available. While the interface is often similar, there are big differences in the command set and memory architecture. As a consequence there is not a single U8glib constructor. Instead, please select some fitting constructor from [here](device.md).

The constructor above
```
U8GLIB_NHD27OLED_BW u8g(13, 11, 10, 9); 
```
will setup the NHD-27-12864 OLED display with a SSD1325 controller (monochrome mode).



## Example: NHD-27-12864 OLED ##

Here is a more complete setup on a breadboard (thanks to fritzing for the picture) with the NHD-27-12864 OLED.

![http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_Steckplatine.png](http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_Steckplatine.png)

Notes:
  * 3.3 volt is taken from the Arduino Board
  * Reset line is created by a capacitor and a resistor.
  * The schematic above contains a little bug: I forgot to wire VDD and GND for the display.

## Example: DOGM128 ##

Here is an example of the DOGM128 display, taken from the dogm128 lib:

![http://wiki.dogm128.googlecode.com/hg/dogm_sch_100.jpg](http://wiki.dogm128.googlecode.com/hg/dogm_sch_100.jpg)

Notes:
  * 3.3 volt are taken from a line regulator
  * Reset line is directly tied to 3.3 volt, which is ok for some displays, but might not always work reliable.


## Conclusion ##

  * To connect a 3.3 volt display to the Arduino Board, use level translation circuits for the I/O pins.
  * Apply the pin numbers to the U8glib constructor.

# Links #

  * [Instructions for the AVR variant of this library](avr.md)
  * [Tutorial: Hello World](thelloworld.md)
  * [List of devices, supported by U8glib](device.md)
  * [U8glib Wiki](u8glib.md)