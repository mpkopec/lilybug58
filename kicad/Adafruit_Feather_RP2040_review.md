# Feather RP2040 KiPart CSV — review notes (2026-10-25)

The CSV is ready for review. It's saved at `kicad/Adafruit_Feather_RP2040.csv`, untracked, and KiPart builds a symbol from it without errors. Below, each header pin is condensed to one row. In the CSV itself, every alternate is a separate row with the same pin number.

Build command: `.venv/bin/kipart -s row kicad/Adafruit_Feather_RP2040.csv -o <lib>`. It is run without `-a`, because each alternate needs its own electrical type.

**Pin map.** It was read from `doc/reference/Adafruit_Feather_RP2040_pinout.svg` and checked against the RP2040's GPIO function-select pattern. All 24 GPIO matched.

Each cell gives the pin name and its type: B `bidirectional`, I `input`, O `output`, OC `open_collector`, PI `power_in`, PO `power_out`. The Other column holds the `power_in` alternates of the power pins.

| Pin | Main name | SPI | UART | I2C | PWM | ADC | Other |
|---|---|---|---|---|---|---|---|
| 1 | ~{RESET} (I) |  |  |  |  |  |  |
| 2, 3 | 3V3 (PO) |  |  |  |  |  |  |
| 4 | GND (PO) |  |  |  |  |  | GND_IN (PI) |
| 5 | A0/GPIO26 (B) | SPI1_SCK (B) | UART1_CTS (I) | I2C1_SDA (OC) | PWM5_A (O) | ADC0 (I) |  |
| 6 | A1/GPIO27 (B) | SPI1_TX (O) | UART1_RTS (O) | I2C1_SCL (OC) | PWM5_B (B) | ADC1 (I) |  |
| 7 | A2/GPIO28 (B) | SPI1_RX (I) | UART0_TX (O) | I2C0_SDA (OC) | PWM6_A (O) | ADC2 (I) |  |
| 8 | A3/GPIO29 (B) | SPI1_~{CS} (B) | UART0_RX (I) | I2C0_SCL (OC) | PWM6_B (B) | ADC3 (I) |  |
| 9 | D24/GPIO24 (B) | SPI1_RX (I) | UART1_TX (O) | I2C0_SDA (OC) | PWM4_A (O) |  |  |
| 10 | D25/GPIO25 (B) | SPI1_~{CS} (B) | UART1_RX (I) | I2C0_SCL (OC) | PWM4_B (B) |  |  |
| 11 | SCK/GPIO18 (B) | SPI0_SCK (B) | UART0_CTS (I) | I2C1_SDA (OC) | PWM1_A (O) |  |  |
| 12 | MOSI/GPIO19 (B) | SPI0_TX (O) | UART0_RTS (O) | I2C1_SCL (OC) | PWM1_B (B) |  |  |
| 13 | MISO/GPIO20 (B) | SPI0_RX (I) | UART1_TX (O) | I2C0_SDA (OC) | PWM2_A (O) |  |  |
| 14 | RX/GPIO1 (B) | SPI0_~{CS} (B) | UART0_RX (I) | I2C0_SCL (OC) | PWM0_B (B) |  |  |
| 15 | TX/GPIO0 (B) | SPI0_RX (I) | UART0_TX (O) | I2C0_SDA (OC) | PWM0_A (O) |  |  |
| 16 | D4/GPIO6 (B) | SPI0_SCK (B) | UART1_CTS (I) | I2C1_SDA (OC) | PWM3_A (O) |  |  |
| 17 | SDA/GPIO2 (B) | SPI0_SCK (B) | UART0_CTS (I) | I2C1_SDA (OC) | PWM1_A (O) |  |  |
| 18 | SCL/GPIO3 (B) | SPI0_TX (O) | UART0_RTS (O) | I2C1_SCL (OC) | PWM1_B (B) |  |  |
| 19 | D5/GPIO7 (B) | SPI0_TX (O) | UART1_RTS (O) | I2C1_SCL (OC) | PWM3_B (B) |  |  |
| 20 | D6/GPIO8 (B) | SPI1_RX (I) | UART1_TX (O) | I2C0_SDA (OC) | PWM4_A (O) |  |  |
| 21 | D9/GPIO9 (B) | SPI1_~{CS} (B) | UART1_RX (I) | I2C0_SCL (OC) | PWM4_B (B) |  |  |
| 22 | D10/GPIO10 (B) | SPI1_SCK (B) | UART1_CTS (I) | I2C1_SDA (OC) | PWM5_A (O) |  |  |
| 23 | D11/GPIO11 (B) | SPI1_TX (O) | UART1_RTS (O) | I2C1_SCL (OC) | PWM5_B (B) |  |  |
| 24 | D12/GPIO12 (B) | SPI1_RX (I) | UART0_TX (O) | I2C0_SDA (OC) | PWM6_A (O) |  |  |
| 25 | D13/GPIO13 (B) | SPI1_~{CS} (B) | UART0_RX (I) | I2C0_SCL (OC) | PWM6_B (B) |  |  |
| 26 | VBUS (PO) |  |  |  |  |  | VBUS_IN (PI) |
| 27 | EN (I) |  |  |  |  |  |  |
| 28 | VBAT (PO) |  |  |  |  |  | VBAT_IN (PI) |

The Feather names don't follow the GPIO numbers: D4 is GPIO6, D5 is GPIO7 and D6 is GPIO8. Several labels in the SVG are not header pins and were left out: the NeoPixel (GPIO16), the GND and VBAT labels of the battery JST connector, and the four STEMMA QT labels.

**Symbol layout and KLC review (2026-10-28).** The CSV's side column only gives KiPart a starting layout. The final layout was arranged by hand in the Symbol Editor and was then checked against the KLC (KiCad Library Convention) symbol rules.

The layout groups the pins by function, as S4.2 asks, with gaps between the groups:
- Left, from top to bottom: `~{RESET}` and EN, then A0–A3, D24/D25, D4, RX/TX, and SCK/MOSI/MISO.
- Right, from top to bottom: 3V3, VBUS and VBAT, then SCL/SDA, then D13 down to D5.
- Bottom: GND.

The body is centred on the origin, and every pin's connection point lies on the 100 mil grid. Outline, fill, text size and field visibility conform to the KLC.

Two deliberate deviations from KLC recommendations are to be explained in the upstream merge request:
1. **All pins are 200 mil long.** S4.1.2 links the pin length to the number of characters in the pin number. For two-character numbers it gives 100 mil. However, the stacked 3V3 pin is numbered `[2,3]`, and that label needs a 200 mil pin to fit. S4.1.2 also requires all pins of a symbol to be the same length, so all pins are 200 mil. The KLC does not address the length of a pin stack.
2. **The power pins are on the right side, not at the top.** S4.2 places positive power at the top of a symbol. Its exception for power-conversion devices puts the power inputs on the left and the power outputs on the right. In this design, the Feather is used much like a regulator. It converts the supply it receives into 3V3, VBUS and VBAT outputs, which are all typed `power_out`. The symbol therefore follows the power-conversion layout.

The metadata follows S6.2.6 and S6.2.7. The Description is comma-separated device information that ends with the footprint name, `Adafruit_Feather`. The keywords repeat no word from the Description and are not prefixes of any word in it. For that reason, `Adafruit` (a prefix of `Adafruit_Feather`), `USB` (a prefix of `USB-C`) and `feather` are not keywords. The upstream `Adafruit_Feather_*` symbols do not follow these two rules. However, the KLC preamble says to match existing symbols only where the KLC itself is unclear, and these two rules are clear.

**Decisions on the draft's conventions (2026-10-28).** All five original proposals were accepted, and six further points were settled.
1. **Peripheral-prefixed alternate names**, e.g. `SPI1_TX` instead of `TX1`. The SVG uses the same label for different peripherals and tells them apart only by colour: `TX1` is SPI1 TX on GPIO27 but UART1 TX on GPIO24. KiCad shows no colour, so in the schematic `TX1` would be ambiguous. No Feather symbol in KiCad's `MCU_Module` library uses alternates, so there is no Feather convention to follow. The prefixed form was chosen as the most readable. `RaspberryPi_Pico` in the same library uses it as well.
2. **I2C as `open_collector`.** The RP2040 has one pad type, a tri-state buffer with an Output Enable (§2.19.4 of the RP2040 datasheet, `doc/reference/RP-008371-DS-1-rp2040-datasheet.pdf`). In I2C mode the controller only drives the pin low or releases it (§4.3.1.3). This emulates open drain with the tri-state buffer. A KiCad pin type describes the pin's behaviour on the net, not the pad circuit, so `open_collector` applies. It also makes ERC flag a push-pull `output` wired to the bus, which `bidirectional` would let pass. `RaspberryPi_Pico` uses `bidirectional` here; the difference is deliberate.
3. **PWM A as `output`, PWM B as `bidirectional`.** On the RP2040, only the B pin of a PWM slice can also be an input, for frequency or duty-cycle measurement.
4. **SPI SCK and CS as `bidirectional`.** The RP2040's SPI can run as master or as slave, so these two pins change direction with the role. SPI TX stays `output` and SPI RX stays `input`, because their direction does not depend on the role.
5. **3V3 as `power_out`.** Adafruit describes the pin as the output of the board's 3.3 V regulator, rated 500 mA peak. As `power_out` it also satisfies ERC without a PWR_FLAG.
6. **Active-low is marked by an overbar only**, e.g. `SPI0_~{CS}`. The overbar covers the signal, not the peripheral prefix. An additional `n` suffix, as in the Pico's `~{SPI0_CSn}`, would mark the signal as active-low twice.
7. **Alternates are limited to what Adafruit documents.** The pinout SVG shows SPI, UART, I2C, PWM and ADC. The RP2040's USB functions (function-select column F9), clock inputs and outputs, and PIO are left out, because this is a Feather symbol, not an RP2040 symbol.
8. **The main name puts the CircuitPython name first, then the GPIO**, e.g. `A0/GPIO26` and `SCK/GPIO18`.
9. **Pin 26 is named `VBUS`**, as in the SVG. The draft's `USB` came from `Adafruit_Feather_Generic`.
10. **VBUS and VBAT are `power_out`, each with a `power_in` alternate** (`VBUS_IN`, `VBAT_IN`), following `RaspberryPi_Pico`. VBUS changes direction with the USB role. As a USB device, the board receives 5 V from the host, and the pin supplies it. As a USB host, the pin must be fed. VBAT is the battery terminal, which the on-board charger also feeds. As `power_out`, it can supply a load from the battery, and the `VBAT_IN` alternate covers a battery wired to the header pin instead of the JST connector.
11. **GND is `power_out`, with a `GND_IN` alternate typed `power_in`.** Ground is a shared node with no real direction. The pin type only tells ERC which symbol drives the net, and the Feather is the board's supply. ERC reports an error when two `power_out` pins share a net, for example when a second supply module also has a `power_out` GND. In that case the `GND_IN` alternate resolves the conflict.

The CSV and the pin table above reflect all eleven decisions.

**Errors in the draft symbol** (`kicad/lilybug58.kicad_sym`). The CSV corrects all of these:
- Pin 6 is named `GPIO27A1`; the `/` is missing.
- Pin 6 has `RTS1` typed `input`. RTS is driven by the UART, so it is an output.
- Pin 10 has `RX1` typed `output`. That alternate is UART1 RX, which is an input.
- Pin 11 has `CTS0` typed `output`. CTS is received by the UART, so it is an input.
- The PWM types are inconsistent: PWM4A/4B/1A are `bidirectional`, while PWM5A/5B/6A/6B are `output`.
- Pins 12–16 are still copies of pin 10.
- Pin 9's `RX1/SDI1` is the only alternate with a second name. It now follows the same naming scheme as the rest.

**State (2026-10-28):**
- `kicad/Adafruit_Feather_RP2040.csv` has 27 pin entries and 91 alternates and reflects all eleven decisions. KiPart builds it without errors. The file is untracked.
- The user reviewed the full pin table against the Adafruit documentation and confirmed it. The symbol in `kicad/lilybug58.kicad_sym` was generated from the CSV with `-m`, which replaced the hand-made draft. The layout was then arranged by hand, checked against the KLC as described above, and the Description and keywords were set in both the symbol and the CSV header.
- Still open: adding `.venv/` to `.gitignore`, which is not yet applied.
