

# Tutorial: Hello World #

  * How to setup U8glib for a display?
  * How to put a simple message on the display with U8glib?

> ![http://wiki.u8glib.googlecode.com/hg/descpic/hello_world.png](http://wiki.u8glib.googlecode.com/hg/descpic/hello_world.png)

## Theory ##

Once the display is physically connected to an Arduino Board three steps are required to bring some graphics  on the display:

  1. Call an U8glib constructor (selected from [here](device.md))
  1. Add the "picture loop"
  1. Write a graphics "draw" procedure

## Example ##

### U8glib Constructor ###

There is not only a single constructor for U8glib. Instead please select a specific constructor for display or display controller (see [here](device.md)). In some cases a display, which is not listed, might also work if just the controller matches.
For example
```
U8GLIB_DOGM128(sck, mosi, cs, a0 [, reset])
```
might also work for other displays than the dogm128 display, if the controller (ST7565) matches.

The controller also needs to know, how the display is connected to the Arduino pins.
The corresponding pin numbers must be applied as arguments to the constructor. See also the [tutorial](tdisplaysetup.md) about the setup of the display hardware.

U8glib offers to control the reset line of the display. If the reset input of the display is wired to a pin of the Arduino board, then this pin-number can be set here. U8glib then will take care on the proper reset of the device.

### Picture Loop ###

U8glib needs a special programming construct, called "picture loop". It can be usually placed in the loop() procedure of the Arduino Sketch:
```
void loop(void) {
  // picture loop
  u8g.firstPage();  
  do {
    draw();
  } while( u8g.nextPage() );
  
  // rebuild the picture after some delay
  delay(1000);
}
```
The full picture of the graphics device is drawn by looping through the picture loop. The body of the picture loop contains a list of graphic commands. It usually makes sense to place the graphics commands into their own procedure (in this example: `draw()`).

More information on the picture loop is described [here](tpictureloop.md).

### Graphics Output ###

Best practice is to place all graphics commands into one procedure (`draw()`):

```
void draw(void) {
  // graphic commands to redraw the complete screen should be placed here  
  u8g.setFont(u8g_font_unifont);
  u8g.drawStr( 0, 20, "Hello World!");
}
```

#### Graphic Commands ####

There are a lot of graphics commands. All of them are listed in the [User Reference Page](userreference.md) of U8glib.

```
  u8g.setFont(u8g_font_unifont);
```
The first command in this little example selects a font. All fonts start with `u8g_font_`. Fonts can be selected by their [size](fontsize.md) or by their [origin](fontgroup.md).

```
  u8g.drawStr( 0, 20, "Hello World!");
```
The second command writes a string to the display. The first two arguments define the position on the screen. The `drawStr` procedure uses the previously selected font and will use the current color index (defaults to 1) to render the string on the display.

#### General Restriction ####

There are some restrictions on this `draw()` procedure (picture loop). This restrictions are explained in more detail [here](tpictureloop.md). From a programming perspective this means for the `draw()` procedure (picture loop):
  * Do not modify global variables from inside the `draw()` procedure.
  * Do not declare `static` variables inside the `draw()` procedure.
  * Assume a cleared and empty screen at the beginning of the `draw()` procedure.
  * Internal values like draw color or current font should be set at the beginning of the `draw()` procedure.
  * Internal values like draw color or current font can be set outside the picture loop, if they are not changed within the picture loop.
On the other hand, the following is fine (and often required):
  * Read values from global variables or use arguments to the `draw()` procedure.
  * Use local variables, `if` conditions and loops (`for`, `while`) within the `draw()` procedure.

For example, do not do the following:
```
int y_pos = 0;  // global variable

void draw(void) {
  // graphic commands to redraw the complete screen should be placed here  
  u8g.setFont(u8g_font_unifont);
  u8g.drawStr( 0, y_pos, "Hello World!");
  y_pos++;      // Wrong: Global variable modified inside picture loop / draw()
}
```

If you would like to program an animation which increases the y-position for each picture, then increase `y_pos` outside the picture loop:
```
int y_pos = 0;  // global variable

void draw(void) {
  // graphic commands to redraw the complete screen should be placed here  
  u8g.setFont(u8g_font_unifont);
  u8g.drawStr( 0, y_pos, "Hello World!");
}

void loop(void) {
  // picture loop
  u8g.firstPage();  
  do {
    draw();
  } while( u8g.nextPage() );

  // Correct: Increase y_pos outside the picture loop
  y_pos++; 
  // rebuild the picture after some delay
  delay(1000);
}


```


## Conclusion ##

  * Use the correct constructor to setup the display (see [here](device.md)).
  * Place graphics commands inside the [picture loop](tpictureloop.md).
  * Group your graphics commands into a procedure (e.g. `draw()`).
  * Please note the restrictions for the picture loop.

# Links #

  * [Tutorial: How to connect a display](tdisplaysetup.md)
  * [List of devices, supported by U8glib](device.md)
  * [U8glib Wiki](u8glib.md)