# Third-party reference material

This directory holds third-party documents that the design refers to. They
are copied here so that every reference survives a change in the upstream
repository's branches or layout. These files are not covered by the
project's CC BY 4.0 licence. Each file keeps the licence of its source,
which is stated below.

## Adafruit_Feather_RP2040_pinout.svg

The file is the pinout diagram of the Adafruit Feather RP2040. It is used to
rename the pins of the project's Feather RP2040 symbol, to choose the GPIO of
the key matrix, and to write the pin map of the QMK keyboard definition.

- Source: `Adafruit Feather RP2040 pinout.svg` in
  [adafruit/Adafruit-Feather-RP2040-PCB](https://github.com/adafruit/Adafruit-Feather-RP2040-PCB),
  at commit `ea88166891ee0a1697a3899a5d55ab3722a2f125`.
- Pinned download link:
  <https://raw.githubusercontent.com/adafruit/Adafruit-Feather-RP2040-PCB/ea88166891ee0a1697a3899a5d55ab3722a2f125/Adafruit%20Feather%20RP2040%20pinout.svg>
- Changes: the file was renamed so that the name contains no spaces.
  Additionally, the three `font-family` rules (`.st2`, `.st8`, `.st58`) were
  extended with fallback fonts. The original rules name only PostScript
  fonts (`CourierNewPSMT`, `CourierNewPS-BoldMT`, `DroidSansMono`), which
  most browsers do not match, so the labels fell back to the default serif
  font. Every fallback has an advance width of 0.600–0.602 em, the same as
  Courier New, so that each label still fits its fixed background
  rectangle. The bold rule also received `font-weight:bold`, because the
  bold weight was previously carried only by the PostScript name. The rest
  of the content is unmodified.
- Licence: Creative Commons Attribution-ShareAlike. The upstream README does
  not state the licence version, and the `license.txt` it refers to is not
  present in the upstream repository.

The upstream README requires its text to be included in any redistribution.
It is reproduced below verbatim, apart from the product photograph it embeds.

> # Adafruit-Feather-RP2040-PCB
>
> Open source PCB files for Feather RP2040
>
> PCB format is EagleCAD schematic and board layout
>
> For more details, check out the product pages at
>
>    * https://www.adafruit.com/products/4884
>
> **We are releasing these files so folks can start creating custom designs based on the RP2040 chip. This design has been built and tested successfully**
>
> Adafruit invests time and resources providing this open source design,
> please support Adafruit and open-source hardware by purchasing
> products from Adafruit!
>
> Designed by Adafruit Industries.
> Creative Commons Attribution, Share-Alike license, check license.txt for more information
> All text above must be included in any redistribution

## RP-008371-DS-1-rp2040-datasheet.pdf

The file is Raspberry Pi's datasheet of the RP2040 microcontroller, which
the Adafruit Feather RP2040 carries. It is used to choose the electrical
types of the pins and pin alternates of the project's Feather RP2040
symbol. For example, §2.19.4 (Pads) and §4.3.1.3 (I2C IOs) describe how
the I2C function drives a pad, and §4.4 (SPI) describes how the SPI TX pin
drives its pad. The decisions that rely on it are recorded in
`kicad/Adafruit_Feather_RP2040_review.md`.

- Source: the RP2040 datasheet published by Raspberry Pi Ltd at
  <https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf>. That
  link serves the latest build, which can differ from the copy here. The
  copy here is therefore identified by its colophon, which gives
  `build-date: 2025-02-20` and
  `build-version: 3184e62-clean`, and by its SHA-256 checksum
  `be56fbb75ba0ae9e26558a73c93ac3e75c2ad4e6878d3b6703de2a76d886ea8c`.
- Changes: none. The content is unmodified, as the licence requires.
- Licence: Creative Commons Attribution-NoDerivatives 4.0 International
  (CC BY-ND 4.0), © 2020–2025 Raspberry Pi Ltd, as stated in the
  datasheet's colophon. Portions of the text are © Synopsys, Inc. and © Arm
  Limited and are used with their permission, as the colophon also states.
