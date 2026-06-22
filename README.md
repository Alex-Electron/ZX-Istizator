# Z80-Istizator

> *"Istizator"* — from Russian "истязать" (to torment, to stress-test relentlessly).  
> A Z80 CPU stress tester and signal analyzer driven by a Raspberry Pi Pico.

Inspired by [slabbi/Z80-CPU-Tester](https://github.com/slabbi/Z80-CPU-Tester).  
This project takes the idea further with dedicated hardware and full automation.

---

## What it does

Z80-Istizator puts a Z80 CPU through its paces:

- **Auto clock sweep** — Pico generates a clock signal and sweeps frequency from low to the CPU's limit, automatically finding the maximum stable operating frequency.
- **Reset control** — Pico drives the RESET line, allowing controlled startup sequences and reset-during-run tests.
- **Full signal verification** — Tests all major Z80 control signals:
  - `INT` / `NMI` — Interrupt handling (maskable and non-maskable)
  - `/WAIT` — Bus wait state injection
  - `/HALT` — Halt state detection
  - `M1` — Machine cycle 1 indicator (opcode fetch)
  - `/RFSH` — DRAM refresh cycle verification
  - `/BUSRQ` / `/BUSACK` — Bus request/acknowledge handshake

---

## Hardware

- **Custom PCB** (KiCad) — designed from scratch for this project
- **Raspberry Pi Pico** — clock generation, reset control, test sequencing, result reporting
- **Z80 CPU socket** — accepts NMOS and CMOS Z80 variants

---

## Planned features

- [ ] PCB design (KiCad)
- [ ] Pico firmware (MicroPython or C/C++)
- [ ] Automatic max-frequency detection with binary search algorithm
- [ ] Interrupt test sequences (INT, NMI)
- [ ] WAIT state injection test
- [ ] HALT detection
- [ ] M1 / RFSH cycle verification
- [ ] BUSRQ / BUSACK handshake test
- [ ] Serial/USB output of test results
- [ ] Pass/fail summary with timing data

---

## Status

Early planning stage. Hardware design in progress.
