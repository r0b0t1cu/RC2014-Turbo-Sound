# Jumper settings

This guide explains the jumper legend printed on the bottom of the PCB.

## J1 RC bus connector

J1 is the large RC bus connector. The footprint has two rows of pin header. One row is used for the electrical connection; the additional row was included for RC bus fit and mechanical stability.

## J2 base address

Install **one J2 jumper only** in the selected position. The table shows the base address selected by each J2 pin pair. The `A15` and `(ZX)` entries are the Spectrum decode position, not MSX base addresses.

| J2 pins | Lower (`A4=0`) | High (`A4=1`) |
| --- | ---: | ---: |
| 1–2 | `00h` | `10h` |
| 3–4 | `80h` | `90h` |
| 5–6 | `40h` | `50h` |
| 7–8 | `C0h` | `D0h` |
| 9–10 | `20h` | `30h` |
| 11–12 | `A0h` | `B0h` |
| 13–14 | `60h` | `70h` |
| 15–16 | `E0h` | `F0h` |
| 17–18 | `A15` | `(ZX)` |

JP2 selects address bit A4. It chooses between the lower/even and upper/odd half of the address range selected by J2. For example, J2 11–12 with JP2 low selects `A0h`; JP2 high selects `B0h`. This lets the board use the other half if an I/O address conflicts with another device.

JP2 performs the same A4 selection as JP5 on the [electrified RC2014 YM2149 board](https://github.com/electrified/rc2014-ym2149), but the jumper positions are reversed:

| A4 selection | This board, JP2 | electrified board, JP5 |
| --- | --- | --- |
| Low / even (`A4=0`) | 1–2 | 2–3 |
| High / odd (`A4=1`) | 2–3 | 1–2 |

## Addressing mode

| Mode | J2 | JP1 | JP3 | JP4 | JP2 |
| --- | --- | --- | --- | --- | --- |
| MSX | 11–12 | 1–2 | 1–2 | 1–2 | 1–2 (low, `A4=0`) |
| ZX Spectrum | 17–18 | 2–3 | 2–3 | 2–3 | A4 selection is not specified in the printed mode note |

The board's printed legend describes the mode jumpers as follows:

- **JP1** selects the decode input: `A0` for MSX, `A14` for ZX Spectrum.
- **JP3** selects the BC1 path: read at `A2h` for MSX, or `/RD` read at `FFFDh` for ZX Spectrum.
- **JP4** selects the BDIR path: data write at `A1h` for MSX, or `/WR` write at `BFFDh` for ZX Spectrum.
- **JP2** selects A4 low (`1–2`, `A4=0`) or high (`2–3`, `A4=1`).

## Clock source and division

| Jumper | Position | Function |
| --- | --- | --- |
| JP5 | 1–2 | Onboard oscillator |
| JP5 | 2–3 | RC bus clock |
| JP6 | 1–2 | Divide clock by 2 |
| JP6 | 2–3 | Divide clock by 4 |
| JP9 (U6) and JP10 (U5) | Closed | YM clock divided by 2 |
| JP9 (U6) and JP10 (U5) | Open | Leave open for AY-3-8910 |

## LED port

TSPLAYER's eight-LED meter uses the separate RCBus Digital I/O module at port 0. The Turbo Sound board jumpers configure AY address decoding and clocking.
