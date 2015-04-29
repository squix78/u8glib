# Introduction #


bdf2u8g converts a bdf font (glyph bitmap distribution format) to the internal u8glib font format

# Update v1.13 #

The section specifier for the font array will change for U8lib v1.13. For any custom fonts the old section specifier
```
U8G_SECTION(".progmem.fontname")
```
should be replaced by
```
U8G_FONT_SECTION("fontname")
```
U8glib v1.13 already contains the correct section specifier. The new version of bdf2u8g will also generate the new section specifier.



# Details #

Example:
```
bdf2u8g.exe -b 32 -e 127 5x7.bdf font5x7 font5x7.c
```

Required arguments

  * .bdf file (A file which usually ends in .bdf)
  * fontname (C identifier for the fontname)
  * .c file (Output file which has C syntax and contains the data of the font)

Optional arguments
  * `[-b num]` Start with ASCII code `num`, range for `num`: 0..255
  * `[-e num]` End with ASCII code `num`, range for `num`: 0..255
  * `[-l page]` Use this `page` within the bdf font for ASCII codes 0..127, range for `page`: 0..512, page 0 selects encoding 0..127, page 1 selects encoding 128..255, etc.
  * `[-u page]` Use this `page` within the bdf font for ASCII codes 128..255, range for `page`: 0..512, page 0 selects encoding 0..127, page 1 selects encoding 128..255, etc.

# Links #

  * Display unicode strings as hex numbers: http://rishida.net/tools/conversion/