


# Interactive Menu #
  * How draw and handle a selection menu with U8glib?
  * Programming hints for interactive graphics

Note: There is also full menu library for U8glib: [M2tklib](http://code.google.com/p/m2tklib/). Creation of menues and other data entry dialog screens is much simpler with M2tklib. The remaining part of this example will build a simple menu only by using graphics primitives from U8glib.


## Example ##

As an example, this tutorial will demonstrate how to build a selection menu with four entries. The menu will have one cursor bar, which allows to select one of the four lines. The following picture shows the cursor bar over the last entry:

![http://wiki.u8glib.googlecode.com/hg/descpic/menu.png](http://wiki.u8glib.googlecode.com/hg/descpic/menu.png)

With versoin 1.03 this example is also part of the Arduino release. The full Arduino source is available [here](http://code.google.com/p/u8glib/source/browse/sys/arduino/Menu/Menu.pde).

## Theory ##

All interactive (changeable) graphics should be split into two different procedures:
  * `draw()`: A procedure for drawing the picture. Usually such a picture will depend on some global variables. For example a selection menu will depend on the position of the cursor bar.
  * `update()`: A procedure for changing the variables, which influence the picture. In this example we will need a procedure, which modifies the position of the cursor bar.

These two functions must be placed at different locations:
  * The `draw()` procedure must be used **inside** the picture loop.
  * The `update()` procedure must be used **outside** the picture loop.

## Code ##

### Draw Menu ###

The following example code uses the "C" API. The code draws the menu including the cursor bar. The position of the cursor bar is stored in the global variable `menu_current`.

```
#define MENU_ITEMS 4
char *menu_strings[MENU_ITEMS] = { "First Line", "Second Item", "3333333", "abcdefg" };

void draw_menu(void) {
  uint8_t i, h;
  u8g_uint_t w, d;
  u8g_SetFont(&u8g, u8g_font_6x13);
  u8g_SetFontRefHeightText(&u8g);
  u8g_SetFontPosTop(&u8g);
  h = u8g_GetFontAscent(&u8g)-u8g_GetFontDescent(&u8g);
  w = u8g_GetWidth(&u8g);
  for( i = 0; i < MENU_ITEMS; i++ ) {        // draw all menu items
    d = (w-u8g_GetStrWidth(&u8g, menu_strings[i]))/2;
    u8g_SetDefaultForegroundColor(&u8g);
    if ( i == menu_current ) {               // current selected menu item
      u8g_DrawBox(&u8g, 0, i*h+1, w, h);     // draw cursor bar
      u8g_SetDefaultBackgroundColor(&u8g);
    }
    u8g_DrawStr(&u8g, d, i*h, menu_strings[i]);
  }
}
```

### Update Menu ###

External buttons, a touchpanel or other sensors might modify the cursor bar position:
```
void update_menu(void)
{
 if ( up ) {
      menu_current++;
      if ( menu_current >= MENU_ITEMS )
        menu_current = 0;
 }
 else if ( down ) {
      if ( menu_current == 0 )
        menu_current = MENU_ITEMS;
      menu_current--;
 }
}
```

### Main Procedure ###

`draw_menu()` and `update_menu()` are put together in the main procedure:

```
    ...
    u8g_FirstPage(&u8g);
    do {
      draw_menu();                 // inside picture loop
    } while( u8g_NextPage(&u8g) );
    
    update_menu();                 // outside picture loop
    ...
```

## Code Optimization ##

The example above is now working and the menu can be used, however the code has still one little problem: The menu is always refreshed. This might lead to some flicker artefacts on the display. It would be better only to redraw the menu if the cursor bar has been changed:

The main procedure could be changed to this:
```
    ...
    if (  menu_redraw_required != 0 ) {
      u8g_FirstPage(&u8g);
      do {
        draw_menu();                 // inside picture loop
      } while( u8g_NextPage(&u8g) );
      menu_redraw_required = 0;      // menu updated, reset redraw flag
    }
    update_menu();                   // outside picture loop
    ...
```

And of course, `menu_redraw_required` must be set in the `update_menu()` procedure:
```
void update_menu(void)
{
 if ( up ) {
      menu_current++;
      if ( menu_current >= MENU_ITEMS )
        menu_current = 0;
      menu_redraw_required = 1;
 }
 else if ( down ) {
      if ( menu_current == 0 )
        menu_current = MENU_ITEMS;
      menu_current--;
      menu_redraw_required = 1;
 }
}
```

# Conclusion #

Menus and other interactive graphics should be implemented with two different procedures:
  * The `draw` procedure, which depends on some global variables.
  * The `update` procedure, which modifies these global variables.


# Links #

  * [U8glib Wiki](u8glib.md)
