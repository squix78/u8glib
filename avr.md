

# Install #

  * Download `u8glib_avr_vX.XX.zip`
  * Extract content to a local directory
  * Add all files (.c files and u8g.h) of the `u8glib/src` directory to your project
  * Update search path for the include file (if required)
  * AVR Studio 4: Set additional options (Project - Configuration - Custom Options)
    * `[All Files]`
      * `-ffunction-sections`
      * `-fdata-sections`
    * `[Linker Options]`
      * `-Wl,--gc-sections`
  * AVR Studio 6: [See M2tklib Instructions for AVR](http://code.google.com/p/m2tklib/wiki/as6)


# Setup #

## Hello World Example ##

Here is the "Hello World" example:
```
#include "u8g.h"
#include <avr/interrupt.h>
#include <avr/io.h>

u8g_t u8g;

void draw(void)
{
  u8g_SetFont(&u8g, u8g_font_6x10);
  u8g_DrawStr(&u8g, 0, 15, "Hello World!");
}

int main(void)
{
  /* select minimal prescaler (max system speed) */
  CLKPR = 0x80;
  CLKPR = 0x00;
  /*
    CS: PORTB, Bit 2 --> PN(1,2)
    A0: PORTB, Bit 1 --> PN(1,1)
    SCK: PORTB, Bit 5 --> PN(1,5)
    MOSI: PORTB, Bit 3 --> PN(1,3)
  */
  u8g_InitSPI(&u8g, &u8g_dev_st7565_dogm132_sw_spi, PN(1, 5), PN(1, 3), PN(1, 2), PN(1, 1), U8G_PIN_NONE);

  for(;;)
  {  
    u8g_FirstPage(&u8g);
    do
    {
      draw();
    } while ( u8g_NextPage(&u8g) );
    u8g_Delay(100);
  } 
}
```

## U8glib Init ##

The example above uses
```
  u8g_InitSPI(&u8g, &u8g_dev_st7565_dogm132_sw_spi, PN(1, 5), PN(1, 3), PN(1, 2), PN(1, 1), U8G_PIN_NONE);
```
All devices with `_sw_spi` or `_hw_spi` can be used as second argument. Please look at the [device wiki page](device.md) for a list of available devices.

The prototyp for [u8g\_InitSPI](userreference#InitSPI_,_InitHWSPI_,_Init8Bit.md) is
```
uint8_t u8g_InitSPI(u8g_t *u8g, u8g_dev_t *dev, uint8_t sck, uint8_t mosi, uint8_t cs, uint8_t a0, uint8_t reset);
```
Arguments are:
  * `u8g`: Address of a u8g object
  * `dev`: Address of a display [device](device.md)
  * `sck`: Clock line
  * `mosi`: Data line from controller to display
  * `cs`: Chip select line of the display
  * `a0`: Register select (RS) of the display
All pin names must have the form `PN(port-numer, bit-position)`, with:
  * port-number: 0 for PORTA, 1, for PORTB, 2 for PORTC, ... and
  * bit-position: The position of the pin within a byte.

## U8glib Hardware SPI ##

To use the hardware SPI device simply replace the sw-spi device with the hardware variant:
```
  u8g_InitSPI(&u8g, &u8g_dev_st7565_dogm132_hw_spi, PN(1, 5), PN(1, 3), PN(1, 2), PN(1, 1), U8G_PIN_NONE);
```
Notes:
  * The atmega hardware SPI communication has been written for the ATMEGA88. It might be required to change some settings in `u8g_com_atmega_hw_spi.c` for other AVR controller:
  * It might be required to set the chip select pin of the AVR SPI subsystem to output. If this pin is not used as `cs` or `a0` for the display, then this pin must be manually set to output.





# Links #

  * [Tutorial: Hello World](thelloworld.md)
  * [List of devices, supported by U8glib](device.md)
  * [U8glib Wiki](u8glib.md)