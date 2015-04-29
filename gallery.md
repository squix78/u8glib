# Blue and White SPI 128x64 OLEDs #

![http://wiki.u8glib.googlecode.com/hg/otherpic/new_haltec_sh1106_blue_oled.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/new_haltec_sh1106_blue_oled.jpg)

Today I received a blue and a white 128x64 OLED from `HalTec`. The blue OLED has a SH1106 controller. It runs fine with the Uno (5V power) and the Due (3.3V power). U8glib constructor for the setup of the above picture:
```
U8GLIB_SH1106_128X64 u8g(4, 5, 6, 7);	// SW SPI Com: SCK = 4, MOSI = 5, CS = 6, A0 = 7
```

![http://wiki.u8glib.googlecode.com/hg/otherpic/new_haltec_ssd1306_white_oled.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/new_haltec_ssd1306_white_oled.jpg)

The white 128x64 OLED has a SSD1306 controller. It did not run with the Arduno Uno, but it works fine with the Due (3.3V power supply):

```
U8GLIB_SSD1306_128X64 u8g(4, 5, 6, 7);	// SW SPI Com: SCK = 4, MOSI = 5, CS = 6, A0 = 7
```

Unfortunately, I do not have the datasheet, so I can not say, whether it is a bug, that the SSD1306 OLED does not work with the Arduino Uno.



# LD7032 60x32 OLED #

![http://wiki.u8glib.googlecode.com/hg/otherpic/ld7032_nano2.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ld7032_nano2.jpg)

This is a very small OLED module based on the LD7032 controller (See [here](http://www.aliexpress.com/store/product/0-5-inch-OLED-display-shield-for-Arduino-OCELL/329792_1944014364.html)). It requires a 3.3 volt power supply, but the module has 5V tolerant inputs. Support for this controller is added in v1.16. Pin description for the PCB is here:

![http://wiki.u8glib.googlecode.com/hg/otherpic/ld7032_pins.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ld7032_pins.jpg)

# SSD1306 128x64 OLED #

![http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1306_no_ack.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1306_no_ack.jpg)

The SSD1306 has two different signal lines for the I2C data signal (one for input and one for output). However the pins of this OLED module are only connected to the input data line of the SSD1306. As a result it can not send the I2C ACK (it will be also invisible to any I2C scanner). This display from `HelTec` is connected to 5V power supply. Data and clock lines accept 5V signals and do not need a pullup resistor. Support for this OLED is added to v1.16 of U8glib. A beta release can be downloaded here:
http://forum.arduino.cc/index.php?topic=219419.0

To support this display, the I2C constructor requires a special option:
```
U8GLIB_SSD1306_128X64 u8g(U8G_I2C_OPT_NO_ACK);	
```


# ST7920 128x64 #

![http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_128x64.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_128x64.jpg)

Dec 2013, I activated an inexpensive ($9) ST7920 based display module. Setup for this display is:
```
U8GLIB_ST7920_128X64_1X u8g(13, 11, 10, 9); // SPI Com: SCK = en = 13, MOSI = rw = 11, CS = di = 10, Reset = 9
```
There was almost no documentation, so I had to guess the backlight resistor. 150 Ohm seem to be ok with 5V.


# ERC24064-1 COG Display with UC1608 Controller #

![http://wiki.u8glib.googlecode.com/hg/otherpic/u8glib_uc1608_240x64.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/u8glib_uc1608_240x64.jpg)

I recently ordered a 240x64 COG Display with UC1608 controller from buy-display.com. Software modifications had been very simple for U8glib, but I had some trouble to get the bugs out of the hardware setup. Also, the extra reset line seems to be required in my case.

This is a 3.3V display, so for testing I decided to use an Arduino Due to avoid the additional level shifter. The backlight current is limited to 40mA (suggested value is 90mA).

Support for this display will be included in v1.15 of U8glib.

# Arduino Community Logo #

![http://wiki.u8glib.googlecode.com/hg/otherpic/arduino_community_logo_u8g.png](http://wiki.u8glib.googlecode.com/hg/otherpic/arduino_community_logo_u8g.png)

... an updated version of the Arduino community logo http://arduino.cc/en/Trademark/CommunityLogo for U8glib.

# ARM LPC1114 with SSD1351 128x128 OLED #

![http://wiki.u8glib.googlecode.com/hg/otherpic/lpc1114_ssd1351_oled.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/lpc1114_ssd1351_oled.jpg)


U8glib port to Cortex-M0: LPC1114 controller with SSD1351 OLED. ARM port will be available with U8glib v1.14.


# A2 Micro panel thermal printer #

![http://wiki.u8glib.googlecode.com/hg/otherpic/a2_micro_printer.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/a2_micro_printer.jpg)

Version v1.14 of U8lib will include support for a thermal printer. There is a 192x120 mode and 384x240 hi-resolution mode for the A2 Micro panel thermal printer. U8G\_16BIT must be enabled for the hi-resolution mode (see u8g.h).


# SSD1351 128x128 OLED #

![http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1351_128x128_oled.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1351_128x128_oled.jpg)

Version v1.13 of U8lib includes support for the SSD1351 OLED ([ILSoft OLED](http://www.kickstarter.com/projects/ilsoftltd/colour-oled-breakout-board) and [Arduino Shield](http://electronics.ilsoft.co.uk/ArduinoShield.aspx)). The picture shows the 128x128 OLED with the U8glib `HiColor` (16 Bit) mode. The Arduino shield is put on top of an Arduino Uno.

This OLED will reach up to 4 frames per second with an ATMega (16MHz) and up to 26 frames per second with Arduino Due (ARM Core).

Note: The picture does not exactly reflects the colors from the display. For example pure red appears as orange on the image.


# HT1632 Support for U8glib #

![http://wiki.u8glib.googlecode.com/hg/otherpic/ht1632.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ht1632.jpg)

Thanks to the Arduino Community: V1.13 of u8glib will support HT1632 based LED matrix displays.
See also http://forum.arduino.cc/index.php?topic=168537


# U8glib Test Equipment #

![http://wiki.u8glib.googlecode.com/hg/otherpic/all_displays_apr_2013.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/all_displays_apr_2013.jpg)

These displays are used to test a new release of U8glib (Apr 2013). From top left to buttom right: KS0108 (128x64), T6963 (240x128, Varitronix), ST7565 (132x32, DOGM132, EA), ST7920 (192x32, NHD), UC1610 (160x104, DOGXL160, EA), SSD1325 (128x64, NHD), SSD1327 (96x96, Seeedstudio), ST7565 (128x64, DOGM128, EA), ST7565 (128x32, NHD), UC1701 (102x64, DOGS102, EA), PCF8812 (96x65, Nokia Display).

# Arduino Due #

![http://wiki.u8glib.googlecode.com/hg/otherpic/dogs102_arduino_due.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/dogs102_arduino_due.jpg)

First time that I saw the U8glib logo on the Arduino Due (DOGS102 Display).

# Varitronix 240x128 #

![http://wiki.u8glib.googlecode.com/hg/otherpic/varitronix_240x128_t6963.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/varitronix_240x128_t6963.jpg)

Recently, I got access to a used T6963 based display (Varitronix 240x128).
There was not much documentation, so it took some time to implement support for it.
LED backlight requires a lot of current (somewhere between 300mA and 500mA).
Additional -15V are needed for the board, because it does not contain a negative DC-DC converter for the LCD. Support for this display will be available with U8glib v1.11.

# NHD C12832 #

![http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_c12832.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_c12832.jpg)

With the help of the great breakout board from http://www.alexanderhiam.com/projects/nhd-bob/#1, I  finally got my old NHD C12832 Display working with U8glib. Support for the NHD C12832 will be included in v1.10.

# ST7920 and `ChipKit` Uno32 #

![http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_chipkit.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_chipkit.jpg)

  * `ChipKit` Uno32
  * NHD 192x32 display with ST7920 controller

# Electro-Mechanical Flip-Disc #

![http://wiki.u8glib.googlecode.com/hg/otherpic/flipdisc.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/flipdisc.jpg)

See also [Flip-Disc Device](flipdisc.md)

# DOGXL160 E-Bike Controller #

![http://wiki.u8glib.googlecode.com/hg/otherpic/dogxl160_ebike.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/dogxl160_ebike.jpg)

A picture from Frank's E-Bike controller project with the DOGXL160 display and U8glib. (Thanks to Frank for the picture).

# Seeedstudio 96x96 OLED #

![http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1327_i2c_avr.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/ssd1327_i2c_avr.jpg)

  * Seeedstudio 96x96 OLED
  * ATMega328
  * SSD1327 Controller
  * I2C Interface

# ST7920 with AVR #

![http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_avr.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/st7920_avr.jpg)

  * ATMEGA328
  * Aktive NHD 192x32 display with ST7920 controller
  * EA DOGM132x32 not used here

# EA DOGM132 controlled by ATMEGA #

![http://wiki.m2tklib.googlecode.com/hg/pic/avr_file_select.jpg](http://wiki.m2tklib.googlecode.com/hg/pic/avr_file_select.jpg)

  * Picture from M2tklib project

# NHD 128x64 OLED #

![http://wiki.m2tklib.googlecode.com/hg/pic/event_source_oled.jpg](http://wiki.m2tklib.googlecode.com/hg/pic/event_source_oled.jpg)

  * Arduino Board
  * NHD OLED
  * User input via serial interface