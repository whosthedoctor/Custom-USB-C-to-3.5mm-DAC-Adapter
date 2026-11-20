# Build struggles

Notes on what went wrong while building this adapter, so the next attempt doesn't repeat it.

## Lifted USB-C resistor pads — 2026-11-20

- I lifted all of the pads on my USB-C breakout boards while working on the CC resistors — about seven USB-C resistor pads lifted in total.
- With the R1/R2 pads gone, there's nowhere left to solder the 5.1kΩ CC resistors on those boards, so those breakout boards can't be used for the CC lines anymore.
- Lesson: the CC resistor pads on the MTDELE breakout are fragile. Don't force a resistor or a joint, and don't keep reheating the same pad.
- Fix going forward: buy replacement USB-C breakout boards that already have the CC1/CC2 5.1kΩ resistors soldered on, so they're ready for data with no CC soldering needed. Amazon only — see the sourcing notes in the main README.
- The DAC boards and everything else are still fine; only the USB-C breakout boards need replacing.
