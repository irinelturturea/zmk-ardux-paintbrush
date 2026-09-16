# The Paintbrush

This directory contains the ARDUX implementation for `The Paintbrush` hardware being developed by KemoNine.

## ZMK Studio

The Paintbrush supports [ZMK Studio](https://zmk.dev/docs/features/studio) for runtime keymap editing.

* The overlay defines a `zmk,physical-layout` (8 positions) plus a 1x8
  `zmk,matrix-transform`. Both are required: with `CONFIG_ZMK_STUDIO=y` ZMK
  refuses to build a keyboard that has no physical layout, and a layout with no
  `keys` is rejected too. Without a physical layout the Studio UI would open
  empty even if the firmware built.
* `the_paintbrush_left` carries an `&studio_unlock` binding — on the Custom
  layer (hold the Custom layer key, tap the first position).
* Only the LEFT half is built with Studio (`snippet: studio-rpc-usb-uart` +
  `-DCONFIG_ZMK_STUDIO=y` in `.github/workflows/build.yml`). The RIGHT half is
  built plain, so `the_paintbrush_right.keymap` must not reference
  `&studio_unlock`.
* Studio overrides live in the settings partition and survive both reboots and
  reflashes. After flashing new firmware, run "Restore Stock Settings" in
  zmk.studio so the compiled keymap is used again.
* zmk.studio in the browser needs a USB cable (WebSerial, Chrome/Edge).

The `keys` coordinates describe a plain 2x4 grid. Adjust the `x`/`y` values if
the rendering in zmk.studio does not match the real key arrangement — this only
affects the drawing, not which key does what.
