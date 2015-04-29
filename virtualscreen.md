# Virtual Screen #

  * Virtual display with user specific dimension
  * Up to 4 sub displays
  * Two to four physical displays can be combined


# Example Code #

  * Currently only C API supported
  * Physical displays u8g1 and u8g2 are combined:

```
u8g_t u8g1;  // physical display 1
u8g_t u8g2;  // physical display 2
u8g_t u8g;   // virtual display

int main(void)
{
  u8g_uint_t h;

  
  u8g_Init(&u8g1, ...);
  u8g_Init(&u8g2, ...);

  // setup virtual display, assign virtual dimension
  u8g_Init(&u8g, &u8g_dev_vs);
  u8g_SetVirtualScreenDimension(&u8g, 128, 127);

  // map physical displays on this screen
  u8g_AddToVirtualScreen(&u8g, 0, 0, &u8g1);
  u8g_AddToVirtualScreen(&u8g, 0, 64, &u8g2);
  
  u8g_FirstPage(&u8g);
  do
  {
    u8g_DrawLine(&u8g, 0,0,127,127);
    u8g_SetFont(&u8g, u8g_font_7x13);
    h = u8g_GetFontAscent(&u8g);
    u8g_DrawStr(&u8g, 10, h, "ABCgdef");
    u8g_DrawStr(&u8g, 0, 10+h, "AB");
  }while( u8g_NextPage(&u8g) );
  return 0;
}

```