


# Font and String Handling #
  * How to align and position a text string?
  * How to draw a frame around a text?

## Ascent, Descent and Line Spacing ##

The height of a font is defined by the ascent and descent:
  * Ascent (Pixel above the baseline): [getFontAscent()](userreference#getFontAscent.md)
  * Descent (Pixel below the baseline): [getFontDescent()](userreference#getFontDescent.md)

The following picture has been rendered with the following code:
```
u8g.setFont(u8g_font_gdr25);
u8g.drawStr(5, 40, "(ABg)");  
```
> ![http://wiki.u8glib.googlecode.com/hg/descpic/linespacing_ex_text.png](http://wiki.u8glib.googlecode.com/hg/descpic/linespacing_ex_text.png)

The ascent of `u8g_font_gdr25` is 31, descent is -9 and the single (factor = 64) line spacing is 40.

The dotted line shows the "baseline". All characters are placed above baseline. Some glyphs are lower than the base line: The lower letter "g" extends 9 pixel below baseline.

Ascent, descent and line spacing are derived by a font height calculation method.
There are three calculation methods, where the "extended text" calculation is the default (see also the picture above). The three methods are:
  * void u8glib::setFontRefHeightText(void)
  * void u8glib::setFontRefHeightExtendedText(void)
  * void u8glib::setFontRefHeightAll(void)

These three methods are discussed in the next section.

The line spacing ([getFontLineSpacing](userreference#getFontLineSpacing.md)) is derived from ascent and descent values:
```
line_spacing = ((ascent - descent)*factor) / 64
```
The `factor` allows to strech the line. A factor of 128 means double line spacing:
| factor | 64 | 77 | 128 |
|:-------|:---|:---|:----|
| line height | single | 1.2x | double |

The line spacing factor can be set with [setFontLineSpacingFactor](userreference#setFontLineSpacingFactor.md).

## What is the height of a font? ##

The height of a font obviously depends somehow on the font. I have added a wiki page which gives an [overview on the existing fonts](fontsize.md), based on their size. I decided to use the size of the captial A as a reference size.

However, for the usual tasks in a graphics library, the height of the capital A often is useless, because there are other, more bigger glyphs. It might be better to use the size of '(' or another big character inside the font.

At the moment, u8glib offers three reference heights. The user can choose the height which fits best:

### void u8glib::setFontRefHeightText(void) ###

The size of the capital A is used as a reference height. Ascent is the height of the capital A or the number 1. The descent value is the number of pixel of the lower letter g below baseline.

![http://wiki.u8glib.googlecode.com/hg/descpic/height_text.png](http://wiki.u8glib.googlecode.com/hg/descpic/height_text.png)

### void u8glib::setFontRefHeightExtendedText(void) ###

The size of the glyph "(" is used as a reference height. Ascent are the number of pixel of "(" above baseline. The descent value is the lower value of the descent of "g" or "(". This is also the default.

![http://wiki.u8glib.googlecode.com/hg/descpic/height_ex_text.png](http://wiki.u8glib.googlecode.com/hg/descpic/height_ex_text.png)

### void u8glib::setFontRefHeightAll(void) ###

This will select the highest ascent and lowest descent values of any glyph of the font.

![http://wiki.u8glib.googlecode.com/hg/descpic/height_all.png](http://wiki.u8glib.googlecode.com/hg/descpic/height_all.png)

## How to align and position a text string? ##

There are four different reference positions for a text:
  * Upper left: `void U8GLIB::setFontPosTop(void)`
  * Center: `void U8GLIB::setFontPosCenter(void)`
  * Baseline:  `void U8GLIB::setFontPosBaseline(void)`
  * Bottom `void U8GLIB::setFontPosBottom(void)`


In the following code, the reference position is the upper (plus one) left corner of the text.
```
u8g.setFont(u8g_font_gdr25);
u8g.setFontPosTop();
u8g.drawStr(5, 20, "(ABC)");  
```
![http://wiki.u8glib.googlecode.com/hg/descpic/top_height_ex_text.png](http://wiki.u8glib.googlecode.com/hg/descpic/top_height_ex_text.png)



## What is the width of a string? ##

The procedure
```
u8g_uint_t U8GLIB::getStrWidth(const char *s)
```
calculates and returns the width of a string.
The returned value is the space which should be reserved for the string. It includes some space at the left and right side of the text:

![http://wiki.u8glib.googlecode.com/hg/descpic/str_width.png](http://wiki.u8glib.googlecode.com/hg/descpic/str_width.png)

## How to draw a frame around a text? ##

These are the dimensions of a string:
```
h = u8g.getFontAscent()-u8g.getFontDescent();
w = u8g.getStrWidth("(AgI)");
```
Please note, that only the width depends on the string. The height is defined by the current settings for the reference height (see above):
  * `void u8glib::setFontRefHeightText(void)`
  * `void u8glib::setFontRefHeightExtendedText(void)`
  * `void u8glib::setFontRefHeightAll(void)`

This is the code for drawing a text together with a frame:
```
u8g.setFontRefHeightExtendedText();
u8g.setFontPosTop();
...
h = u8g.getFontAscent()-u8g.getFontDescent(u8g);
w = u8g.getStrWidth("(AgI)");
u8g.drawStr(3, 10, "(AgI)");
u8g.drawFrame(3-1, 10, w+2, h+2) ;
```

![http://wiki.u8glib.googlecode.com/hg/descpic/str_bbx_top2.png](http://wiki.u8glib.googlecode.com/hg/descpic/str_bbx_top2.png)



# Links #

  * [Next Tutorial: Interactive Menu](tmenu.md)
  * [U8glib Wiki](u8glib.md)
