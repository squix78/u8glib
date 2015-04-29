# Upload to Arduino Due on Linux #
Often the following code seems to be required (enter on terminal):
```
stty -F /dev/ttyACM0 speed 1200 cs8 -cstopb -parenb
```

# Defines #

## GCC ##
  * Show gcc buildin macros: `gcc -dM -E - < /dev/null`

## `F_CPU` ##

  * F\_CPU must be defined and must expand to the CPU frequency in hertz (e.g. -DF\_CPU=16000000L)

## Identify Environment ##

  * `ARDUINO`: Version number of the Arduino Environment. 100 for 1.00.
  * `__AVR__`: Atmel AVR
  * `__18CXX`: MPLAB C18 (PIC)
  * `__PIC32MX`: PIC32
  * `__XC8` MPLAB XC8 Compiler (Microchip)
  * `__PIC18` MPLAB XC8 Compiler with selected PIC18 device
  * `__arm__`: GCC ARM (Arduino Due)
  * `__SAM3X8E__`: Arduino Due
  * `__AVR_ARCH__`: Values 2 and 25 are ATTiny


## Communication Macros ##

  * `U8G_COM_HW_SPI`
  * `U8G_COM_ST7920_HW_SPI`
  * `U8G_COM_SW_SPI`
  * `U8G_COM_ST7920_SW_SPI`
  * `U8G_COM_PARALLEL`
  * `U8G_COM_FAST_PARALLEL`
  * `U8G_COM_SSD_I2C`
  * `U8G_COM_T6963`

These communication macros are specific for each environment.