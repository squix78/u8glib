# Introduction #

This wiki page explains the device structure. It should contain enough information to enable users to create their own device.

I will start working on this wiki page and it might be incomplete for a (long?) time. Please excause...


# What is a U8glib device? #

The U8glib device is a C structure:
```
struct _u8g_dev_t
{
  u8g_dev_fnptr dev_fn;         /* device procedure */
  void *dev_mem;                /* device memory */
  u8g_com_fnptr com_fn;         /* communication procedure */
};
typedef struct _u8g_dev_t u8g_dev_t;
```

There are three parts in a device structure:
  1. `dev_fn` (required): A callback procedure, which handles messages from the graphics procedures.
  1. `dev_mem` (optional): A pointer to some local memory.
  1. `com_fn` (optional): A communication procedure

Basic idea is, that (parts of) the frame buffer is stored via `dev_mem`. Display specific procedures (display init, pixel set and clear) are handled by `dev_fn` and communication specific details (TWI, SPI, etc) could be handled via  `com_fn`.

It is always possible that `dev_fn` directly writes to the display device. In this case set `com_fn` to `u8g_com_null_fn`.

Here is a template for a very simple device:
```
uint8_t my_dev_fn(u8g_t *u8g, u8g_dev_t *dev, uint8_t msg, void *arg)
{
  /* handle messages here */
  return 1; /* successful handled */
}

u8g_dev_t u8g_dev_my_simple_display = { my_dev_fn, NULL, u8g_com_null_fn };
```

# Messages to the device callback procedure #

All the communication between the graphics procedures and the device callback procedure (`dev_fn`) is done via messages. A message is a number, which is passed in the argument `msg` of the `dev_fn`:
```
uint8_t my_dev_fn(u8g_t *u8g, u8g_dev_t *dev, uint8_t msg, void *arg)
```
In some cases, there are additional arguments and parameters together with `msg`. In this case `arg` is a none-NULL pointer to these additional arguments.

A typical device callback will look like this:
```
uint8_t my_dev_fn(u8g_t *u8g, u8g_dev_t *dev, uint8_t msg, void *arg)
{
  switch(msg)
  {
    case U8G_DEV_MSG_INIT:
      /* setup/init display */
      /* ... */
      break;

    case U8G_DEV_MSG_PAGE_NEXT:
      /* write a page to the display */
      /* ... */
      break;

    /* maybe handle more messages */
  }
  /* make a call to a suitable page buffer procedure */
  return u8g_dev_pb8v1_base_fn(u8g, dev, msg, arg);
}
```


This is a small reference of all messages:
  * `U8G_DEV_MSG_INIT`: Setup and init display, no args.
  * `U8G_DEV_MSG_STOP`: Shutdown display, no args (not used at the moment).
  * `U8G_DEV_MSG_CONTRAST`: Set contrast or bightness of the display, `arg` is a pointer to `uint8_t` which contains the contrast value (0..255).
  * `U8G_DEV_MSG_SLEEP_ON`: Display should enter sleep mode, no args.
  * `U8G_DEV_MSG_SLEEP_OFF`: Display should recover from sleep mode, no args.
  * `U8G_DEV_MSG_PAGE_FIRST`: Picture loop will start now. Page buffer procedures will reset the page handling to the first page and clear the buffer.
  * `U8G_DEV_MSG_PAGE_NEXT`: A page has been finished, `dev_fn` should transfer page to the device, page buffer procedures will setup next page. 0 should be returned if there are no further pages required. There are no args for this message.
  * `U8G_DEV_MSG_GET_PAGE_BOX`: Return dimensions of the page. `arg` is a pointer to `u8g_dev_arg_bbx_t`. This messages is handled by page buffer procedures.
  * `U8G_DEV_MSG_SET_PIXEL`: Set a pixel. `arg` is a pointer to `u8g_dev_arg_pixel_t`. This messages is handled by page buffer procedures.
  * `U8G_DEV_MSG_SET_8PIXEL`: Set a sequence of 8 pixel. `arg` is a pointer to `u8g_dev_arg_pixel_t`. This messages is handled by page buffer procedures.
  * `U8G_DEV_MSG_SET_COLOR_INDEX` (until v1.12): Not used
  * `U8G_DEV_MSG_SET_COLOR_ENTRY` (since v1.13): Set color palette entry. `arg` is a pointer to `u8g_dev_arg_irgb_t`.
  * `U8G_DEV_MSG_SET_XY_CB`: Not used
  * `U8G_DEV_MSG_GET_WIDTH`: Return the width of the display. `arg` is a pointer to `u8g_uint_t`. The width must be stored at the address pointed to by `arg`.
  * `U8G_DEV_MSG_GET_HEIGHT`: Return the height of the display. `arg` is a pointer to `u8g_uint_t`. The height must be stored at the address pointed to by `arg`.
  * `U8G_DEV_MSG_GET_MODE`: Return the display mode as return value of `dev_fn`, no other args. Possible return values are `U8G_MODE_BW` and `U8G_MODE_GRAY2BIT `

# Page Buffer Procedures #

## Available Page Buffer ##

## Page Buffer Interface ##

## Device Callback and Page Buffer ##

## Example ##

(device for stdout)

# Communication Interface #