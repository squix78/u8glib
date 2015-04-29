

# Picture Loop #

  * How does the "picture loop" work?
  * How to use the "picture loop".
  * What should be avoided...

## Theory ##

### External Restrictions ###

U8glib addresses several problems:
  * Some displays do not allow to read data from the display memory.
  * Some displays do not allow to set a single pixel in the display memory. Often eight pixels must be assigned together.
  * Limited size of the RAM area of an embedded controller.
With some minor restrictions, these problems are solved with U8glib.

### List of Graphics Primitives ###

Let us assume a simple list of graphic commands, grouped into one procedure:
```
void draw(void)
{
  u8g_SetColorIndex(u8g, 1);
  u8g_DrawBox(u8g, 10, 12, 20, 38);  
  u8g_SetFont(u8g, u8g_font_osb35);
  u8g_DrawStr(u8g, 40, 50, "A");
  u8g_SetColorIndex(u8g, 0);
  u8g_DrawPixel(u8g, 28, 14);  
}
```
This will produce the following picture:

![http://wiki.u8glib.googlecode.com/hg/descpic/pl_full.png](http://wiki.u8glib.googlecode.com/hg/descpic/pl_full.png)

Notes:
  * The pixel at (28, 14) is first set by `DrawBox` and later cleared by `DrawPixel`.
  * The sequence order of the graphic commands is important.

### Local Frame Buffer ###

According to the external restrictions, it is not possible to clear a single pixel within the display memory: We can neither set a single pixel, nor can we read the surrounding area of that pixel.

A simple solution is to mirror the display memory into the RAM of the controller.
Assuming a 128x64 monochrome display, an algorithm would look like this:
  1. allocate local frame buffer in the controller RAM for a 128x64 display
  1. clear local frame buffer (128x64 pixel)
  1. execute draw() to render the picture into the local frame buffer
  1. transfer local frame buffer to display memory

### Multiple Draw ###

If draw() is a fixed list of commands, then it is possible to execute
the draw procedure twice. This means that the following procedure will not make a visual difference:
  1. allocate local frame buffer in the microcontroller RAM
  1. clear local frame buffer
  1. execute draw()
  1. execute draw()
  1. transfer local frame buffer to display memory
Of course it takes some longer time to render the picture. And indeed the additional call to the draw procedure does not make sense at the moment.

### Half Frame Buffer ###

There is still the third restriction: RAM is usually very limited in an embedded system. But here is the trick to half the required RAM in the controller: The same picture is divided into two parts: An upper and lower part. The upper part is created by one call to the draw() procedure and the lower part is created by another call to the same draw procedure:
  1. allocate half local frame buffer (called 'page') in the microcontroller RAM (128x32 pixel)
  1. clear page (128x32 pixel), set clipping to lines 0 to 31
  1. execute draw()
  1. transfer page to the upper half of the display frame buffer.
  1. clear page (128x32 pixel), set clipping to lines 32 to 63
  1. execute draw()
  1. transfer page to the lower half of the display frame buffer

During steps 1 to 4 we get the following picture on the display:

![http://wiki.u8glib.googlecode.com/hg/descpic/pl_lower.png](http://wiki.u8glib.googlecode.com/hg/descpic/pl_lower.png)


Steps 5 to 7 will create the lower part:

![http://wiki.u8glib.googlecode.com/hg/descpic/pl_upper.png](http://wiki.u8glib.googlecode.com/hg/descpic/pl_upper.png)

Both half pictures together will appear as a full picture on the display:

![http://wiki.u8glib.googlecode.com/hg/descpic/pl_full.png](http://wiki.u8glib.googlecode.com/hg/descpic/pl_full.png)

### Implementation ###

The decision on the number of parts and the number of calls to the draw() procedure is left to the low level driver. So there is a loop instead of explicit calls:
```
  // picture loop
  u8g.firstPage();  
  do {
    draw();
  } while( u8g.nextPage() );
```

## Issues ##

### Visual Experience ###

Very complex scenes might render slowly and the observer of the display might see, that upper parts are updated earlier than lower parts (depending on the applied rotation).

The good news is, that there is no flickering, because the display memory is never erased completely.

### Programming Restrictions ###

  * The display memory can not be updated
> It is not possible to do this:
    1. Draw 'A' on the display
    1. Wait
    1. Draw 'B' on the display
> Writing only 'B' on the display will erase 'A'. So it is required to draw 'A' and 'B' in the third step.
  * In general the value of a pixel must not depend on any other pixel values: Only information about pixel in the current page is available. As a consequence, it is not possible to copy regions within the display memory or to do scrolling.
  * The same graphics commands must be repeated until the picture loop terminates. This is a consequence of the discussion above.
  * Internal variables are not reset at the beginning of the body of the picture loop. It is a good programming style to set all required variables like the draw color or the font at the beginning of the body of the picture loop.

## Conclusion ##

  * U8glib allows the use of read-only display devices also with little additional ram.
  * Although the screen is rendered several times with the same content, the refresh rate is fully acceptable. Frame-rates of more than 20 are possible on an ATMEGA system.

# Links #
  * [U8glib Wiki](u8glib.md)