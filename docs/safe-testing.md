# Safe testing — no bench supply needed

Test in stages, cheapest / most protected device first. Never plug the finished adapter straight into the iPhone first.

## 1. Multimeter first, no power at all

- 5V to GND: not a short. It reads low for a second as the caps charge, then climbs into the kΩ range. If it stays at 0–10Ω, do not plug it in.
- D+ to GND, D− to GND, D+ to D−: not shorts.
- CC1 to GND and CC2 to GND: about 5.1kΩ each — this confirms the pull-downs.
- Continuity, end to end: 5V pin on the DAC board to 5V on the USB-C plug, same for GND, D+, D−.

## 2. Power-only test, with a current limit

No bench supply? Use one of these instead:

- A powered USB hub with overcurrent protection, or
- A USB power meter / USB tester inline between the adapter and the host, so you can see the live current, or
- A plain 5V USB charger for a power-only check — it powers the board but carries no data, so it only tests for heat / shorts, not audio.

Plug it in with no headphones. A PCM2704 board should idle well under 100mA. If the current jumps, the board gets hot, or anything smells, unplug immediately.

Check the DAC board is getting about 5V at its 5V pin, and that nothing heats up after 30 seconds.

## 3. Data test on a sacrificial port

Use an old laptop, a Raspberry Pi, or that same protected hub — something with USB overcurrent protection and a replaceable port, not the phone.

Plug in through a USB power meter if you have one. It should show up as a USB audio device and stay under roughly 100–200mA while playing. Play audio and check both channels.

## 4. Only then the iPhone

If it passed steps 1–3 with normal current, no heat, and clean enumeration, the risk to the iPhone is basically gone — the dangerous faults (5V/GND short, D+/D− shorted to power) would have shown up already.

## Why this order works

A short is found by the multimeter, an overcurrent fault is found by the protected hub / power meter, and by the time the iPhone sees it, both of those are already ruled out.
