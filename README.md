# UPDI-interface

[![License: CC BY-NC-SA](https://img.shields.io/badge/License-CC_BY--NC--SA-purple.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Hardware: CERN-OHL-S](https://img.shields.io/badge/License-CERN--OHL--S--2.0-purple)](https://gitlab.com/ohwr/project/cernohl/-/wikis/uploads/819d71bea3458f71fba6cf4fb0f2de6b/cern_ohl_s_v2.txt)

This is a KiCad PCB that breaks out a common USB‑to‑TTL serial adapter (often sold as a “USB to TTL Serial Communication Conversion Module”) into UPDI, UART, and RS‑485 interfaces. The board is meant to sit between your USB adapter and targets such I am using it with my ROV project.

## UART TX/RX swapping (poka‑yoke)

Getting UART TX and RX the wrong way round is easy at design time and painful to fix once the board is built. I have implemented a [poka‑yoke](https://en.wikipedia.org/wiki/Poka-yoke) crossover: two solder bridges  let you route either straight‑through or swapped connections by changing which pads are bridged—no trace cuts or bodge wires. How it works and how to use it in other projects: [UART TX/RX swapping made simple](https://philipmcgaw.com/uart-tx-rx-swapping-made-simple/).

## License

 * Hardware design files in this repository are licensed under the **[CERN Open Hardware Licence v2 — Strongly Reciprocal (CERN-OHL-S-2.0)](https://gitlab.com/ohwr/project/cernohl/-/wikis/uploads/819d71bea3458f71fba6cf4fb0f2de6b/cern_ohl_s_v2.txt)**, an open source hardware license recommended by the [Open Source Hardware Association (OSHWA)](https://oshwa.org/).
 * Software files in this repository are licensed under the **[Creatice Commons - Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)**

- **Copyright:** [Philip McGaw](https://philipmcgaw.com/)

You may use, study, modify, and redistribute the sorcecode, schematic and PCB layout under those terms. **Derivative designs must be released under the same license(s).** If you share the design or boards built from it, include a link to the licenses.

## Related links

- [SquashedFly](https://squashedfly.eu/)
- [UART TX/RX swapping made simple](https://philipmcgaw.com/uart-tx-rx-swapping-made-simple/) — poka‑yoke UART symbol and footprints used on this board
- [KiCad](https://www.kicad.org/) — PCB design software