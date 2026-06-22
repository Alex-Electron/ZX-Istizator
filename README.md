# ZX-Istizator

> *"Istizator"* — from Russian "истязать" (to torment, to stress-test relentlessly).  
> A universal high-speed stress tester and signal analyzer for the Z80 CPU and other retro ICs, driven by the powerful RP2350.

Originally inspired by [slabbi/Z80-CPU-Tester](https://github.com/slabbi/Z80-CPU-Tester) for Z80 testing, this project takes the idea much further. It evolves into a multi-chip test bench featuring dedicated high-speed hardware, full automation, and support for audio and floppy controllers.

---

## What it does

### 1. Z80 CPU Stress Testing
Puts the Z80 CPU through its paces at extreme speeds:
- **Auto clock sweep** — Generates a clock signal and sweeps frequency from low to the CPU's limit, automatically finding the maximum stable operating frequency.
- **Reset control** — Drives the RESET line for controlled startup sequences.
- **Full signal verification** — Tests all major Z80 control signals (`INT`, `NMI`, `/WAIT`, `/HALT`, `M1`, `/RFSH`, `/BUSRQ`, `/BUSACK`).

### 2. AY-3-8910 / YM2149F Audio Testing
- **Authentic clock** — Hardware generation of the 1.7734 MHz clock signal via PWM for pixel-perfect ZX Spectrum sound accuracy.
- **Automated sweeps** — Tests tone channels, noise generator, and envelopes.
- **Built-in Audio** — Integrated LM386/PAM8302 amplifier and onboard speaker/jack to physically hear the test results.

### 3. KR1818VG93 / WD1793 / MB8877A (FDC) Testing
- **FDD Emulation** — RP2350 fully emulates floppy drive signals (`INDEX`, `TR00`, and MFM `RAW READ` streams).
- **HIL (Hardware-in-the-Loop)** — Insert a known-good Z80 into the adjacent socket to let it communicate natively with the FDC under test, while the RP2350 emulates the ROM and disk drive mechanics.
- **Safe 12V System** — Soviet VG93 chips burn instantly if 12V is applied before 5V. Our hardware design uses an MT3608 Step-Up and a MOSFET switch to safely apply +12V *only* during the test sequence, ensuring total protection.

---

## Hardware Architecture

- **Custom PCB** (KiCad) — Designed from scratch.
- **Pimoroni PGA2350 (RP2350B)** — The brain of the project. Featuring **48 GPIOs**, it allows direct parallel connection to address, data, and control buses without slow shift registers. All operations are executed at maximum speed via PIO state machines.
- **Level Shifting** — 74LVC245 transceivers protect the 3.3V RP2350 from 5V retro logic.
- **Diagnostics** — 74HC573 latches freeze and display the bus state on LEDs at any exact machine cycle. INA219 current sensor instantly detects internal short-circuits in dead chips.
- **Color display** — Driven by SPI, shows live test results, pass/fail status, and measured max frequency.

---

## Planned features

- [ ] PCB design in KiCad (Base schematic + PGA2350 routing)
- [ ] Implement ZIF-40 and ZIF-28 sockets for Z80, VG93, and AY chips
- [ ] Safe 12V switching circuit for VG93
- [ ] Audio mixer and amplifier circuit
- [ ] C/C++ Firmware utilizing RP2350 PIO blocks
- [ ] Automatic Z80 max-frequency detection with binary search algorithm
- [ ] Z80 control signals verification (INT, WAIT, HALT, M1, etc.)
- [ ] AY-3-8910 tone and noise auto-test sequence
- [ ] FDC (VG93) read/write test sequence
- [ ] Color display output (SPI TFT, e.g. ST7735 / ILI9341) — real-time results on-device
- [ ] Serial/USB output of test logs

---

## Credits & Acknowledgements

This project was born out of deep passion for retro-computing. Special thanks to:

* **Spectrum Forever** (a group of 7 dedicated ZX Spectrum enthusiasts) — the ideologists, architects, and developers behind expanding this project from a simple CPU tester into a universal ZX-chip testing combine.
  * Active contributors include: **Alexander Lavrinovich ([@Alex-Electron](https://github.com/Alex-Electron))**, **Paul Leikam ([@pahan4](https://github.com/pahan4))**, **Alex ([@Alex-2-Graf](https://github.com/Alex-2-Graf))**, **Mefisto**, **Sergey Lackay**, **Oleg Dejanoff**, and **Sergey Potapov**.

## Status

Early planning and schematic design stage. Hardware layout in KiCad in progress.
