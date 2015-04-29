A graphics library with support for many different displays.

![http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_oled180.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_oled180.jpg) ![http://wiki.u8glib.googlecode.com/hg/otherpic/dogs102_180.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/dogs102_180.jpg)

Left: NHD-2.7-12864 OLED (SSD1325), right: EA DOGS102 LCD (UC1701)

**U8glib:**
  * [Gallery](gallery.md)
  * [Bintray](https://bintray.com/olikraus/u8glib) download links:
    * U8glib for Arduino: [![](https://api.bintray.com/packages/olikraus/u8glib/Arduino/images/download.png)](https://bintray.com/olikraus/u8glib/Arduino)
    * U8glib for AVR: [![](https://api.bintray.com/packages/olikraus/u8glib/AVR/images/download.png)](https://bintray.com/olikraus/u8glib/AVR)
    * U8glib for ARM: [![](https://api.bintray.com/packages/olikraus/u8glib/ARM/images/download.png)](https://bintray.com/olikraus/u8glib/ARM)
    * Converter for BDF fonts: [bdf2u8g\_101.exe on google drive](https://drive.google.com/folderview?id=0B5b6Dv0wCeCRLWJkYTh2TUlYVDg&usp=sharing).
  * Supported environments:
    * [Arduino (ATMEGA and ARM)](http://www.arduino.cc/)
    * [AVR (ATMEGA)](avr.md)
    * [ARM (with example for LPC1114)](lpc1114.md)
  * Library for graphic LCDs and OLEDs
  * Complete [documentation and tutorials](u8glib.md)
  * Graphical user interface library (GUI) available: [M2tklib](http://code.google.com/p/m2tklib/)
  * Monochrome, grayscale and indexed color (planned)
  * COM interfaces: Software SPI, Hardware SPI, 8Bit parallel
  * Large number of fonts (up to [49 pixel height](fontsize.md))
  * Monospaced and proportional fonts
  * Mouse-Cursor support
  * Landscape and portrait mode
  * Many supported [devices](device.md) (SSD1325, ST7565, ST7920, UC1608, UC1610, UC1701, PCD8544, PCF8812, KS0108, LC7981, SBN1661, SSD1306, SH1106, T6963, LD7032)
  * Well-defined interface to the device subsystem

**News 22 Dec 2014**
  * U8glib 1.17 is available on [Bintray](https://bintray.com/olikraus/u8glib)
  * TWI/I2C is now supported for the Arduino Due
  * TWI 400KHz transfer is available for Arduino Uno and Due boards and SSD1306/SH1106 displays (`U8G_I2C_OPT_FAST`)
  * Support for UC1608 and UC1611 (DOGM240, DOGXL240) has been added.
  * See the [Change Log](http://u8glib.googlecode.com/hg/ChangeLog) for details on the new release

**News 29 Nov 2014**
  * Download of bdf2u8g has been disabled. The link has been redirected to google drive.

**News 05 Jul 2014**
  * U8glib 1.16 is now available on [Bintray](https://bintray.com/olikraus/u8glib)
  * Added features: Support for LD7032 OLED controller, support for I2C without ACK (SSD1306 OLEDs)

**News 16 Mar 2014**
  * A report with some nice pictures on the SDL port of U8glib is provided here: http://www.imaginaryindustries.com/blog/?p=435

**News 24 Jan 2014**
  * New release v1.15 is available for download at [Bintray](https://bintray.com/olikraus/u8glib).
  * [Change Log](http://u8glib.googlecode.com/hg/ChangeLog).
**News 9 Dec 2013**
  * Found another nice tutorial for the ST7920 and U8glib: http://www.bajdi.com/cheap-128x64-graphic-lcd-12864zw/.
**News 26 Oct 2013**
  * A nice tutorial on STM32 and U8glib has been published [here](http://helios.wh2.tu-dresden.de/~benni_koch/blog/?p=759).
**News 4 Oct 2013**
  * New release v1.14 is available.
  * U8glib is now available for ARM controller.
  * Download Locations: [Bintray](https://bintray.com/olikraus/u8glib) [Google Code](http://code.google.com/p/u8glib/downloads/list)
  * [Change Log](http://u8glib.googlecode.com/hg/ChangeLog).

**News 6 Jul 2013**
  * Due to ["A change to google download service"](http://google-opensource.blogspot.de/2013/05/a-change-to-google-code-download-service.html) new downloads are also available here: [Google Drive](https://drive.google.com/folderview?id=0B5b6Dv0wCeCRLWJkYTh2TUlYVDg&usp=sharing)
  * U8glib v1.13 is available for download. Changes are listed [here](http://u8glib.googlecode.com/hg/ChangeLog).
  * Added support for [this](http://www.kickstarter.com/projects/ilsoftltd/colour-oled-breakout-board) SSD1351 true color OLED.

**News 5 Jun 2013**
  * The next release v1.13 will include the ":" glyph in the postfix 'n' variant of the fonts. Pictures are already updated, but please note, that v1.12 does not contain the ":" in the 'n' variant of the font:
![http://wiki.u8glib.googlecode.com/hg/fontpic/u8g_font_chikitan.png](http://wiki.u8glib.googlecode.com/hg/fontpic/u8g_font_chikitan.png).

**News 27 Apr 2013**
  * There is a nice [tutorial](http://bens-it-blog.blogspot.de/2013/03/connect-and-use-sainsmart-lcd12864.html) for graphics displays and U8glib.
  * Added a new picture to the [gallery](gallery.md): Collection of my test equipment for U8glib.
**News 24 Mar 2013**
  * New Arduino release v1.12 includes examples for a 4-wire resistive touch panel.
**News 2 Mar 2013**
  * New release v1.11 is available for [download](http://code.google.com/p/u8glib/downloads/list):
    * Support for T6963
    * Support for Arduino Due
    * Sleep Mode
    * 4x mode for ST7920
    * New C++ interface for ST7920
  * Implementation status for the **Arduino Due** (March 2013):
    * Display Controller
      * Tested: SSD1325, ST7565, UC1610, UC1701
      * Implemented (not tested): SSD1327, SSD1306, SSD1309, ST7920, PCD8544, PCF8812, TLS8204, KS0108, LC7981
      * Not supported: T6963, SBN1661
    * Interface
      * Tested: SW SPI
      * Implemented (not tested): ST7920 SW SPI, Standard 8 Bit parallel
      * Not implemented: I2C, HW SPI, T6963 parallel interface, SBN1661 parallel interface

**News 18 Feb 2013**
  * Support for T6963 almost finished
  * Support for Arduino Due started
  * See [Gallery](gallery.md) for some impressions on these two topics.
  * Beta release added to [download page](http://code.google.com/p/u8glib/downloads/list).

**News 2 Feb 2013**
  * New Release v1.10
  * Support for SSD1309 and NHD-C12832
  * Bugfixes for parallel-mode (reset pin) and ST7920 controller
  * MSP430 Clone: http://code.google.com/r/ronnyspiegel-u8glib-msp430/

**News 23 Dec 2012**
  * New release v1.09 available for download
  * Verified with Arduino 1.0.3
  * Fixes several issues with the ST7920 controller
  * Additional fonts
  * ATMega release also supports ATTiny
  * Box and frame with round edges: u8g::drawRBox(), u8g::drawRFrame()
  * Support for more displays and communication interfaces

**News 15 Dec 2012**
  * There are some updates to the bitmap fonts
    * [Additional fonts from X11 distribution](fontgroupadobex11.md)
    * [Additional font from the Arduino Forum](fontgroupcontributed.md)
    * [Updated font from the Arduino Forum](fontgroupfreeuniversal.md)
  * A developer snapshot (including these fonts) is available for download: v1.09pre14.

**News 26 Oct 2012**
  * bdf font converter available for download
  * Description for the "font converter": [Wiki page bdf2u8g](bdf2u8g.md).

**News 02 Oct 2012**
  * Release 1.08 for Arduino and AVR available
  * Created [Gallery](gallery.md) page on the project wiki
  * SSD1327: Support added with I2C interface
  * SSD1322: Support added, but not fully verified
  * Added new displays for existing chips (LC7981 240x64, GFAG20232, NHD-C12864)
  * Speed improvements
  * Fixed SPI for ST7920 (AVR)
  * `ChipKit` support

**News 18 Jul 2012**
  * A bitmap generator for u8glib has been announced: [See Arduino Forum Thread](http://arduino.cc/forum/index.php/topic,114815.0.html)

**News 4 Jul 2012**
  * Release 1.07 for Arduino and AVR
  * Bugfix for Ardino Examples
  * Added "Makefiles" for AVR Release

**News 15 Jun 2012**
  * Release 1.06 for Arduino and AVR
  * U8G\_PROGMEM Bugfix
  * Support for SBN1661 (=SED1520?) and SSD1306

**News 10 Jun 2012**
  * Release 1.05 for Arduino and AVR
  * Tested with Arduino 1.01 IDE
  * Added icon fonts
  * Backup/restore SPI state

**News 15 Apr 2012**
  * Release 1.04 for AVR
  * Almost identical to v1.03, but some more examples added to the AVR variant
  * Also added 1.04 for Arduino Environment
  * New release for [M2tklib](http://code.google.com/p/m2tklib) with support for U8glib
![http://wiki.m2tklib.googlecode.com/hg/pic/u8g/u8g_combo.png](http://wiki.m2tklib.googlecode.com/hg/pic/u8g/u8g_combo.png)

**News 31 Mar 2012**
  * Release 1.03
  * drawLine
  * Speed up of the graylevel devices

**News 18 Mar 2012**
  * Finished the AVR port of u8glib
  * Added [AVR u8glib wiki](avr.md) page

**News 17 Mar 2012**
  * Release 1.02
  * Several bugfixes
  * Support for LC7981
  * drawCircle, drawDisc
  * ported "little rook chess" from [dogm128 lib](http://code.google.com/p/dogm128/wiki/chess)

![http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_oled_chess_180.jpg](http://wiki.u8glib.googlecode.com/hg/otherpic/nhd_oled_chess_180.jpg)

**News 12 Feb 2012**
  * Stable release 1.0 available for download
  * XBM support
  * F() macro support

**News 03 Feb 2012**
  * New beta release v0.14
  * New/updated examples
  * Bug fixes
  * Derived from Print base class

**News 21 Jan 2012**
  * Support for ST7920
  * New beta release v0.09
  * Improved string handling

**News 15 Jan 2012**
  * The [wiki pages](http://code.google.com/p/u8glib/wiki/u8glib?tm=6) are almost finished
  * Another upload is available for the LM6063 display

**News 07 Jan 2012**
  * Beta Releases available for [download](http://code.google.com/p/u8glib/downloads/list)
  * [User Reference Manual](userreference.md) almost stable
