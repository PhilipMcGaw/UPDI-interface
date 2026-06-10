# UPDI-interface

[![License: CC BY-NC-SA](https://img.shields.io/badge/License-CC_BY--NC--SA-purple.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Hardware: CERN-OHL-S](https://img.shields.io/badge/License-CERN--OHL--S--2.0-purple)](https://gitlab.com/ohwr/project/cernohl/-/wikis/uploads/819d71bea3458f71fba6cf4fb0f2de6b/cern_ohl_s_v2.txt)

This is a KiCad PCB that breaks out a common **USB‑to‑TTL serial adapter** (often sold as a “USB to TTL Serial Communication Conversion Module”) into **UPDI**, **UART**, and **RS‑485** interfaces. The board is meant to sit between your USB adapter and targets such I am using it with my ROV project.

**Schematic title:** 2TTL‑UPDI interface PCB  
**Author:** [Philip McGaw](https://github.com/PhilipMcGaw)

## Features

- **Dual 7‑pin sockets** these are for plugging in a standard USB‑to‑TTL module (two rows of header pins) You will need to solder these on to the USB-TTL board yourself.
- **UPDI programming**
  - 1×3 pin header (`UPDI`)
  - 2×3 pin header (`AVR UPDI Header`) for a typical 6‑pin AVR UPDI cable footprint
- **Two UART ports** (`UART0`, `UART1`) — 1×4 pin headers (TX, RX, and flow‑control lines routed per the schematic).
- **RS‑485** (`RS485`) — 1×4 pin header via an on‑board **MAX3072E** half‑duplex transceiver (+3.3 V, ESD‑protected).
- **Poka‑yoke UART** (`Poka Yoke UART`) — not a connector: a **solder‑bridge (or 0805 zero‑ohm) swap point** on the UART0 TX/RX lines so you can correct swapped TX/RX without a PCB respin. See [UART TX/RX swapping made simple](https://philipmcgaw.com/uart-tx-rx-swapping-made-simple/). This will be removed once I am sure I did the connections correctly.
- **Selectable I/O voltage** — solder jumper `Voltage Select` (default **5 V** bridged; optional **3.3 V**).

## What you need

| Item | Notes |
|------|--------|
| USB‑to‑TTL module | Fits the two 1×7 female sockets; common 6‑pin/8‑pin FTDI‑style modules |
| Host software | e.g. [avrdude](https://github.com/avrdudes/avrdude) with UPDI, or [pyupdi](https://github.com/mraardvark/pyupdi) — depends on your adapter firmware |

Fabricate the PCB from the KiCad project (see below). Solder the SMD parts, headers, and the USB module sockets.

## Voltage selection

- **`JP3` (`Voltage Select`)** — shipped/configured for **5 V** by default (see note on schematic: *“Set for 5V by default”*).
- Move the solder jumper to select **3.3 V** I/O when your target requires it.
- **`RS485`** — the schematic notes that **RS‑485 is only guaranteed at 5 V**. Use 5 V operation when you need the MAX3072E link to be reliable.

## Connectors (on‑board labels)

| Reference | Label | Type |
|-----------|--------|------|
| J10 | Primary Header | 1×7 socket — USB‑TTL module |
| J12 | Second Header | 1×7 socket — USB‑TTL module |
| J16 | Voltage in | 1×3 — external supply |
| JP3 | Voltage Select | 3‑pad solder jumper (5 V / 3.3 V) |
| J14 | UART0 | 1×4 pin header |
| J17 | UART1 | 1×4 pin header |
| J15 | UPDI | 1×3 pin header |
| J1 | AVR UPDI Header | 2×3 pin header |
| J13 | RS485 | 1×4 pin header (A/B + power/GND per schematic) |
| R1 | Poka Yoke UART | Solder‑jumper swap footprint on UART0 TX/RX (not a header) |

Pin‑exact assignments are in `KiCAD/UPDI Board.kicad_sch` and the PCB layout; check the silkscreen and net labels (`TX0`, `RX0`, `TX0_poka`, `RX0_poka`, `UPDI`, `A`, `B`, etc.) before wiring.

### UART TX/RX swapping (poka‑yoke)

Getting UART **TX** and **RX** the wrong way round is easy at design time and painful to fix once the board is built. **`R1`** implements a [poka‑yoke](https://en.wikipedia.org/wiki/Poka-yoke) crossover: two solder bridges (this board uses the **solder jumper** footprint; an **0805 zero‑ohm** variant is also in `KiCAD/Common/Footprints/`) let you route either straight‑through or swapped connections by changing which pads are bridged—no trace cuts or bodge wires.

How it works and how to use it in other projects: [UART TX/RX swapping made simple](https://philipmcgaw.com/uart-tx-rx-swapping-made-simple/) (Philip McGaw). KiCad symbol and both footprints live under `KiCAD/Common/`.

## KiCad project

Open the project in **KiCad 10 or later** (project files use the current KiCad 10 schematic format):

```
KiCAD/UPDI Board.kicad_pro
```

| Path | Purpose |
|------|---------|
| `KiCAD/UPDI Board.kicad_sch` | Schematic |
| `KiCAD/UPDI Board.kicad_pcb` | Board layout |
| `KiCAD/UPDI Board.kicad_dru` | Custom design rules |
| `KiCAD/Common/` | Local symbols, footprints, worksheets (includes [SquashedFly](https://squashedfly.eu/) title block and logo footprints) |
| `KiCAD/bom/ibom.html` | Interactive BOM (if generated) |


## License

 * Hardware design files in this repository are licensed under the **[CERN Open Hardware Licence v2 — Strongly Reciprocal (CERN-OHL-S-2.0)](LICENSE)**, an open source hardware license recommended by the [Open Source Hardware Association (OSHWA)](https://oshwa.org/).
 * Software files in this repository are licensed under the **[Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)] (LICENSE)**

- **SPDX identifier:** `CERN-OHL-S-2.0`
- **Copyright:** [Philip McGaw](https://philipmcgaw.com/)
- **Full text:** [LICENSE](LICENSE)

You may use, study, modify, and redistribute the schematic and PCB layout under those terms. **Derivative designs must be released under the same license.** If you share the design or boards built from it, include a copy of the license.

## Credits

- **[SquashedFly](https://squashedfly.eu/)** — title block worksheet (`KiCAD/Common/Squashed Fly.kicad_wks`) and optional PCB logo footprints (`SquashedFlySilk`, `SquashedFlyCopper`, etc.) in `KiCAD/Common/Footprints/`

## Related links

- [SquashedFly](https://squashedfly.eu/)
- [UART TX/RX swapping made simple](https://philipmcgaw.com/uart-tx-rx-swapping-made-simple/) — poka‑yoke UART symbol and footprints used on this board
- [KiCad](https://www.kicad.org/) — PCB design software


https://wiki.dfrobot.com/tel0190/#tech_specs