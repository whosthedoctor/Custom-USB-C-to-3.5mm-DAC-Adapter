# USB-C to 3.5mm DAC Adapter

A USB-C to 3.5mm headphone adapter built from separate boards soldered together — soldering practice. The phone is an iPhone 15 (USB-C).

## The USB-C

- Male USB-C plug breakout
- Breakout board link: https://www.amazon.com/dp/B0D9W8B97B (MTDELE 10-pack — 5 male + 5 female, $6.99).
- Back pads: only G, D+, D-, V
- Front: R1 (populated), R2 (empty pads), C1 (populated).
- CC lines are NOT on the back pads:
  - R1 = CC1 (pin A5), populated with a 5.1kΩ pull-down.
  - R2 = CC2 (pin B5 / VCONN), empty pads.
  - Both CC lines are now tied with 5.1kΩ through-hole resistors soldered to the CC pins and secured with hot glue (done 2026-11-14).

## DAC vs passive (why DAC)

- Passive (wires only): phone outputs analog audio on D+/D-. Cheap, no latency, but phone-dependent — works on most Android, NOT on iPhone. Sound quality = phone's internal DAC.
- DAC: phone sends digital USB audio to a DAC chip in the adapter. Works on any phone including iPhone, sound quality = the DAC chip, can do mic, needs the chip + supporting parts + USB power, negligible latency.
- Decision: DAC (2026-11-14).

## The DAC board — ordered

- **Hailege 2pcs 5V PCM2704 Sound Card Decoding Module DAC Decoder Board, $16.99 for 2 ($8.50 each), Amazon. Ordered 2026-11-15**
- https://www.amazon.com/gp/product/B08D7D7KX4/ref=ox_sc_act_title_1?smid=A2F7ULK8PUMGS&psc=1
- 2-pack of bare PCM2704 boards on Amazon, found with the search terms below.
- Chip: TI PCM2704 — 16-bit / 48 kHz USB Audio Class 1.0 DAC + headphone amp. iOS supports UAC 1.0, so it works with the iPhone 15 and above
- The board has a USB-A male plug on one end and a green 3.5mm jack on the other, with a 12.000 MHz crystal on board.

## Wiring

- USB-C breakout → DAC board USB-A connector pins: V → pin 1 (5V), D- → pin 2, D+ → pin 3, G → pin 4 (GND).
- Desolder the USB-A connector from the DAC board and solder the four wires to the connector pads.
- Headphones plug straight into the DAC board's built-in jack — no DAC-to-jack wiring.

## Soldering Images

1. **CC resistors** — Solder 5.1kΩ through-hole resistors to the CC pins on the USB-C breakout (R1 = CC1, R2 = CC2), then secure them with hot glue so they don't move or short.

   

2. **Desolder the USB-A connector** — Remove the USB-A plug from the DAC board (see "Desoldering the USB-A connector" above). Clean the pads with wick + flux.

   

3. **Wire the breakout to the DAC board** — Solder four wires from the breakout to the DAC board's USB-A pads: V → pin 1 (5V), D- → pin 2, D+ → pin 3, G → pin 4 (GND).

   

4. **Wrap it** — Surround the whole wired assembly with electrical tape, then hot glue over it to hold everything in place and insulate the connections.

   

5. **Test** — Plug the USB-C end into the iPhone 15, check the DAC shows up, then plug headphones into the board's jack.

   

## Desoldering the USB-A connector

- The USB-A plug is through-hole: 4 signal pins + 2 shell/ground tabs (6 joints).
- Add flux and fresh solder to each joint first, fresh solder helps heat transfer and lowers the melting point of the old lead-free solder.
- Heat each joint and remove the solder with solder wick or a desoldering pump.
- The 2 shell tabs are the hard part — they're soldered to large ground pours that sink heat. Use a bigger tip, higher temp (~380°C), and be patient.
- Don't pull the connector until all 6 joints are free — forcing it rips pads off the board. If a pin won't come free, add more solder and try again.
- After removal, clean the pads with wick + flux, then solder the 4 wires to the signal pads.
- Before powering: double-check 5V vs GND with a multimeter (GND pad should show continuity to the jack's ground / the big ground pour). Mixing up D- and D+ just stops enumeration and is an easy swap; mixing up 5V and GND can damage the board.

## From-scratch DAC spec (if building the DAC board instead of buying one)

- TI PCM2704 (32-pin TQFP), 12 MHz crystal + 2× 22 pF, 3.3 V LDO, decoupling + 10 µF bulk, 100 µF output coupling caps. PCM2912 sibling if mic wanted. Check the PCM2704 datasheet for exact pin numbers.
