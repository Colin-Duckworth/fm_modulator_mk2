FM Modulator Project

This project is to make a colpitts oscillator based fm modulator from the transistor/component level.
It will consist of a common emitter, BJT amplifier, tapped LC tank (to form the oscillator), and emitter follower amp (as buffer) into an antenna feed

In terms of the toolchain, this will be an introduction for me to learn KiCad with its integrated SPICE simulation to build out the schematic.

## Projects

| Folder | Contents | Simulation |
|---|---|---|
| `project_folders/fm_modulator_openloop` | CE stage + tank, driven by an AC source | AC sweep |
| `project_folders/fm_modulator_closedloop` | Colpitts oscillator, RF buffer, varactor FM, mic + audio chain, power input (the board) | TRAN / FFT |

## BOM — `fm_modulator_closedloop` (JLCPCB assembly)

Stock and part type checked on jlcpcb.com on 2026-11-16. **Basic** parts have no setup fee; each unique **Extended** part adds a loading fee (about $3). The `LCSC` field on every symbol holds the part number, so the JLCPCB Tools / Fabrication Toolkit plugins can export the BOM and CPL directly.

| Designator | Qty | Value | Package / footprint | LCSC | Type | Part (manufacturer) | Notes |
|---|---|---|---|---|---|---|---|
| Q101, Q102 | 2 | MMBT3904 | SOT-23 | C20526 | Basic | MMBT3904 (CJ) | Oscillator + buffer; sim model = 2N3904 die |
| U1 | 1 | NE5532 | SOIC-8 | C7426 | Basic | NE5532DR (TI) | Dual op amp: mic diff amp + gain stage |
| U3 | 1 | AMS1117-3.3 | SOT-223 | C6186 | Basic | AMS1117-3.3 (AMS) | 3.3 V for the mic |
| D201 | 1 | SS14 | SMA (DO-214AC) | C2480 | Basic | SS14 (MDD) | Reverse-polarity protection |
| FB201 | 1 | 100 Ω @ 100 MHz | 0805 | C1015 | Basic | GZ2012D101TF (Sunlord) | Supply ferrite |
| R101, R104 | 2 | 510 Ω | 0603 | C23193 | Basic | 0603WAF5100T5E | Was 500 Ω (not a standard value) |
| R102 | 1 | 27 kΩ | 0603 | C22967 | Basic | 0603WAF2702T5E | |
| R103 | 1 | 10 kΩ | 0603 | C25804 | Basic | 0603WAF1002T5E | |
| R105 | 1 | 150 Ω | 0603 | C22808 | Basic | 0603WAF1500T5E | |
| R108 | 1 | 12 kΩ | 0603 | C22790 | Basic | 0603WAF1202T5E | |
| R109 | 1 | 2.7 kΩ | 0603 | C13167 | Basic | 0603WAF2701T5E | |
| R110 | 1 | 22 Ω | 0603 | C23345 | Basic | 0603WAF220JT5E | |
| R111 | 1 | 75 Ω | 0603 | C4275 | Basic | 0603WAF750JT5E | Was 68 Ω (68 Ω is Extended); buffer Ic ≈ 14 mA instead of 15 mA |
| R112 | 1 | 68 Ω | 0603 | C27592 | Extended | 0603WAF680JT5E | Buffer output termination: 68 Ω gives ≈50 Ω output once Cμ feedback is included (51 Ω gave ≈40 Ω) |
| R113 | 1 | 220 Ω | 0603 | C22962 | Basic | 0603WAF2200T5E | |
| R201 | 1 | 47 Ω | 0603 | C23182 | Basic | 0603WAF470JT5E | Audio supply RC filter |
| R202, R203 | 2 | 22 kΩ | 0603 | C31850 | Basic | 0603WAF2202T5E | VMID divider |
| R204, R206 | 2 | 5.1 kΩ | 0603 | C23186 | Basic | 0603WAF5101T5E | Diff amp inputs |
| R205, R207, R208 | 3 | 100 kΩ | 0603 | C25803 | Basic | 0603WAF1003T5E | |
| R209 | 1 | 3.3 kΩ | 0603 | C22978 | Basic | 0603WAF3301T5E | |
| C101, C102 | 2 | 47 pF C0G | 0603 | C1671 | Basic | CL10C470JB8NNNC | Were 50 p / 48 p |
| C103 | 1 | 22 pF C0G | 0603 | C1653 | Basic | CL10C220JB8NNNC | Was 33 p; trimmer now carries the rest |
| C104 | 1 | 33 pF C0G | 0603 | C1663 | Basic | CL10C330JB8NNNC | |
| C106 | 1 | 10 pF C0G | 0603 | C1634 | Basic | CL10C100JB8NNNC | Varactor coupling (was 1 p) |
| C110, C112, C203 | 3 | 1 nF X7R | 0603 | C1588 | Basic | CL10B102KB8NNNC | |
| C111, C202, C205, C209, C212 | 5 | 100 nF X7R | 0603 | C14663 | Basic | CC0603KRX7R9BB104 | |
| C210, C211 | 2 | 1 µF X5R | 0603 | C15849 | Basic | CL10A105KB8NNNC | Mic coupling |
| C201, C204, C206, C207, C213 | 5 | 10 µF 25 V X5R | 0805 | C15850 | Basic | CL21A106KAYNNNE | |
| C208 | 1 | 22 µF 25 V X5R | 0805 | C45783 | Basic | CL21A226MAQNNNE | AMS1117 output |
| C109 | 1 | 2.2 pF C0G | 0603 | C5137608 | Extended | FCC0603N2R2C500CT (FOJAN) | No Basic 2.2 pF exists |
| C105 | 1 | 5.8–20 pF trimmer | TZC3 (4.5×3.2) | C22468122 | Extended | STC3MD20-T1 (SEHWA) | Coarse frequency set (was fixed 3.3 p) |
| L101 | 1 | 1 µH ±5% | 0603 | C127458 | Extended | FHW0603UF1R0JST (FH) | SRF 400 MHz; most 1 µH 0603 parts self-resonate near 100 MHz |
| L102 | 1 | 100 nH ±2% wirewound | 0603 | C98088 | Extended | LQW18ANR10G00D (Murata) | Tank inductor; Q matters more than the setup fee |
| D101 | 1 | 1SV229 | SOD-323 | C2762682 | Extended | 1SV229(TPH3F) (Toshiba) | FM-band varactor |
| U2 | 1 | IM73A135V01 | PG-LLGA-5 (4×3) | C3171831 | Extended | IM73A135V01XTSA1 (Infineon) | Analog differential MEMS mic, bottom port (footprint has the sound hole) |
| RV201 | 1 | 50 kΩ trim | Bourns 3314J | C50895 | Extended | 3314J-1-503E (Bourns) | Deviation / audio gain |
| J1, J2 | 2 | SMA jack, vertical through-hole | Amphenol 132134 pattern (5 pins, 5.08 mm square) | C496549 | Extended | BWSMA-KE-Z001 (BAT Wireless) | J1 = ANT, J2 = TEST. About $0.40 each; JLC solders through-hole parts (wave/hand), or hand-solder them |
| U101 | 1 | PE4259 SPDT RF switch | SC-70-6 | C470892 | Extended | PE4259-63 (pSemi) | TX enable: CTRL high = RFC→RF1 (J1) |
| S101 | 1 | SPDT slide switch | SMD right-angle (Shouhan MSK12C02) | C431540 | Extended | MSK12C02 | STBY / TX, lever overhangs the right edge |
| D202 | 1 | Green LED | 0805 | C2297 | Basic | KT-0805G (KENTO) | PWR (on DC_Bias) |
| D102 | 1 | Red LED | 0603 | C2286 | Basic | KT-0603R (KENTO) | TX |
| R210 | 1 | 4.7 kΩ | 0603 | C23162 | Basic | 0603WAF4701T5E | PWR LED, ≈1.9 mA |
| R115, R117 | 2 | 1 kΩ | 0603 | C21190 | Basic | 0603WAF1001T5E | TX LED (≈1.3 mA); CTRL series resistor |
| R116 | 1 | 100 kΩ | 0603 | C25803 | Basic | 0603WAF1003T5E | TX_EN pull-down (STBY by default) |
| C113, C114 | 2 | 1 nF X7R | 0603 | C1588 | Basic | CL10B102KB8NNNC | PE4259 RF1/RF2 DC blocks |
| C115, C116 | 2 | 100 nF X7R | 0603 | C14663 | Basic | CC0603KRX7R9BB104 | U101 VDD decoupling; CTRL filter |
| TP3, TP4 | 2 | Test loop | Keystone 5015 SMD | C2906768 | **Hand-solder** | 5015 (Keystone) | MIC_IN, OPAMP_OUT; excluded from JLC BOM/CPL, order separately |
| TP5 | 1 | +12V_IN, red | Keystone 5010 THT | C2906765 | **Hand-solder** | 5010 (Keystone) | Alligator-clip power input; excluded from JLC BOM/CPL, order separately |
| TP6 | 1 | GND, black | Keystone 5011 THT | C238127 | **Hand-solder** | 5011 (Keystone) | Alligator-clip ground; excluded from JLC BOM/CPL, order separately |
| TP1 | 1 | Test pad | 1.0 mm pad | — | — | bare copper | No part to place (excluded from BOM/CPL) |
| R114, V101, V102 | — | — | — | — | — | — | **Simulation only**: excluded from BOM and board |

**Summary (Rev B):** JLC assembles 43 unique parts. 32 are Basic, covering all resistors except R112, all but one fixed capacitor, both transistors, the op amp, the LDO, the diode, the ferrite and both LEDs. 11 are Extended (C109, C105, L101, L102, D101, U2, RV201, J1/J2, R112, U101, S101), roughly $33 in setup fees. J1 and J2 are through-hole parts: JLC assembly adds a through-hole soldering charge, or leave them off the order and hand-solder them like the test loops. The four test loops (TP3–TP6) are hand-soldered: their footprints are on the board, but they're marked *exclude from BOM* and *exclude from position files* in KiCad, so JLC leaves the pads empty. Order them separately (LCSC numbers above, about 2× 5015, 1× 5010 red, 1× 5011 black). TP1 is a bare pad with no part.

## PCB — `fm_modulator_closedloop.kicad_pcb`

### Substrate and stackup (JLCPCB JLC04161H-7628, standard 4-layer FR-4)

| Layer | Use | Material | Thickness | εr |
|---|---|---|---|---|
| L1 — F.Cu | RF and oscillator traces, all parts | 1 oz copper | 0.035 mm | — |
| dielectric 1 | | 7628 prepreg | 0.2104 mm | 4.4 |
| L2 — In1.Cu "GND" | Solid ground plane (no routing) | 0.5 oz copper | 0.0152 mm | — |
| dielectric 2 | | FR-4 core | 1.065 mm | 4.6 |
| L3 — In2.Cu "PWR" | Power: DC_Bias plane + VCC_AUDIO plane | 0.5 oz copper | 0.0152 mm | — |
| dielectric 3 | | 7628 prepreg | 0.2104 mm | 4.4 |
| L4 — B.Cu | Control / audio / signal traces, GND pour | 1 oz copper | 0.035 mm | — |

Total ≈ 1.6 mm; HASL lead-free finish. In the JLC order choose **4 layers, 1.6 mm, Specify Stackup → JLC04161H-7628**.

### 50 Ω RF output (C112 → U101 → J1 / J2)
- **Geometry:** microstrip on L1 referenced to the L2 ground plane, h = 0.2104 mm, t = 0.035 mm, εr = 4.4.
- **Width:** Hammerstad–Jensen with thickness correction gives Z₀ = 50 Ω at **w = 0.373 mm** bare (51.0 Ω at 0.36 mm). Solder mask lowers Z₀ by about 1–2 Ω, so the RF traces are drawn at **0.36 mm** (≈ 50 Ω under mask). Confirm with JLC's impedance calculator before ordering.
- **Length:**
  - C112 → U101 RFC is about 11 mm, a straight run across the BUFFER AMP / TX SWITCH boundary.
  - Each throw (U101 → C113/C114 → J1/J2) is about 9 mm.
  - At 100 MHz that's under 2° (λg ≈ 1.68 m, ε_eff ≈ 3.19), so the lines are electrically short and the match is set by the source and load.
  - The source is the buffer: R112 = 68 Ω gives Z_out ≈ 50 Ω. With the switch's 0.35 dB loss and a 50 Ω load on J1/J2, everything is ≈ 50 Ω.
- **Ground:**
  - J1 and J2 are through-hole, so their four ground posts tie L1, L2 and L4 together right at the connector.
  - U101's GND pin has its own via beside the pin.
  - At these lengths, the L1 pour's normal 0.3 mm clearance to the RF traces has a negligible effect. The old rule-area keep-out and via fence went with the edge-launch connector.
- **Connectors:** J1 (ANT) and J2 (TEST) are vertical through-hole SMA jacks (BWSMA-KE-Z001) on the standard 5-pin pattern (centre pin plus four ground posts on a 5.08 mm square). The cable plugs in perpendicular to the board. The ~1.6 mm the centre pin runs through the stackup is about λ/1000 at 100 MHz, so it doesn't matter.

### Layout
- **Board:** 100 × 62 mm, four M3 mounting holes (3.2 mm NPTH) 3.5 mm in from each corner. Still within JLC's ≤ 100 × 100 mm price tier.
- **Floorplan** (re-laid 2026-11-18): five labelled silkscreen boxes. The top row is four 25 mm columns that follow the signal left → right, and a full-width POWER strip (about 16 mm) runs along the bottom.

  | Box | Parts | Notes |
  |---|---|---|
  | AUDIO (x 100–125) | U2 mic, C209, TP3, C210/C211, R204–R207, U1, C212, R209, C213, RV201, TP4, R202/R203/C206 (VMID) | Widely spaced for probing and rework. Mic at the top, U1 in the middle, AUDIO_OUT (RV201 / TP4) bottom-right facing R208. |
  | OSCILLATOR (x 125–150) | Q101, L101/R101, L102, C101–C106, R102–R105, TP1, D101, R208 | Kept tight (short tank loops), but spaced so no reference designators overlap. The tank output leaves at the bottom-right towards C109. |
  | BUFFER AMP (x 150–175) | C109, Q102, R108–R113, C110–C112 | Generous spacing. The RF line runs straight through at y = 127.5 mm. |
  | TX SWITCH & PORTS (x 175–200) | U101 + C113–C116, R116/R117, J2 TEST (top), J1 ANT (bottom), S101 + D102/R115 (red TX LED) | S101 sits on the right edge with its slider at the edge; silk reads STBY (top) / TX (bottom). |
  | POWER (bottom strip) | TP5 (+12 V) / TP6 (GND) clip posts, D201, FB201, C201–C203, D202 + R210 (green PWR LED), R201, C204/C205, C207, U3, C208 | Input on the right, flowing left: DC_Bias parts, then R201 at x = 150, then the VCC_AUDIO / 3V3 parts. |
- **Routing:**
  - **By script (L1):** RF only. That means the oscillator (including the varactor feed), the buffer, the tank → C109 link, and C112 → U101 → C113/C114 → J1/J2. Also U101's local nets (CTRL via C116/R117, VDD to C115, TX_EN R116 → R117) and GND / DC_Bias pad vias for the RF parts.
  - **By hand:** everything in AUDIO and POWER, plus the TX LED / S101 and the 3V3 and TX_EN runs to the switch column.
- **Vias:** each RF-part GND pad has its own via to L2, and each RF-part DC_Bias pad has a via to the L3 plane. GND stitching runs on a 4 mm grid inside the three RF boxes plus a ring around the board edge.
- **Pours:** L1 GND, L2 GND, L4 GND. L3 is split to match the sections:
  - **VCC_AUDIO:** under the AUDIO column plus the POWER strip left of x = 150 mm.
  - **DC_Bias:** everywhere else (under the OSCILLATOR, BUFFER and TX columns and the right half of the strip).
  - **R201** straddles the split at x = 150 mm in the strip.
- **Net classes:** RF (/RF_Out, /RF_Ant, /RF_Test, U101 RF1/RF2) 0.36 mm, Power (DC_Bias, VCC_AUDIO, 3V3) 0.5 mm, Default 0.25 mm.
- **JLC design rules:** 0.15 mm minimum track and clearance, 0.3/0.6 mm vias, 0.3 mm copper-to-edge.
- **Silkscreen, front:**
  - Five labelled section boxes.
  - Labels for +12V, GND, PWR, ANT (J1), TEST (J2) and STBY/TX at the switch.
  - Reference designators are 0.8 mm (meets the project's text-height rule), horizontal and clear of pads, with 0 silkscreen warnings.
- **Silkscreen, back:**
  - Each section has a short description sitting directly behind it.
  - The stackup (JLC04161H-7628 layer table + 50 Ω width) sits behind the oscillator / buffer boundary.
  - The power-path description and the project tag (name, date, Rev B) are in the POWER strip.

### Still to do in KiCad
DRC after the 2026-11-18 re-layout shows 0 copper/clearance errors, 0 silkscreen warnings and 0 schematic-parity issues. 47 unconnected items are left for hand routing.

1. **Route the non-RF nets.** Prefer L4 for anything crossing an RF box.
   - **Audio:** mic → C210/C211 → R204/R206 → U1, the U1 feedback nets, VMID, and AUDIO_OUT (U1 pin 7 / RV201 / TP4 → R208 in the oscillator box).
   - **Power:** TP5 → D201 → FB201 (wide, L1), DC_Bias and VCC_AUDIO plane vias for the POWER and AUDIO parts, and the PWR LED (R210 → D202).
   - **3V3:** U3 tab → C208 → C209 / U2 VDD, plus a run over to **C115 pad 1** (U101 VDD) and **S101 pin 1**.
   - **TX_EN:** S101 pin 2 → R115 (→ D102) and over to **R116 / R117** beside U101.
2. **Mic ground:** tie U2 pad 5 (centre GND) to pad 4.
3. **Refill zones** (B), then run DRC. The L3 VCC_AUDIO "isolated copper" warning clears once its pads have vias.
4. **Mic hole-clearance error:** one DRC error comes from the Infineon footprint itself (its centre GND pad sits 0.18 mm from its own sound hole). Exclude it in the DRC dialog.
5. **Check S101's direction with a meter** before the first power-up with an antenna: in the **TX** position, pins 2–1 should be connected. The red TX LED always shows the real state, because it hangs off TX_EN itself.
6. **Optional:** Update PCB from Schematic (F8) should report nothing to change; every footprint is linked to its symbol.

## Rev B: power LED and TX-enable switch

> **Status:** in the schematic and on the PCB (2026-11-18). Parts checked on jlcpcb.com on 2026-11-17/18; the PE4259 pinout and truth table were checked against the pSemi datasheet. The rows are in the BOM table above.

### Power indicator (green "PWR")
- **D202** (green 0805) + **R210** (4.7 kΩ) from `DC_Bias` to GND, in the POWER box.
- It sits after D201 and FB201, so it lights only when 12 V is present **and** the polarity is correct.
- Current: (11.65 V − ~2.9 V) / 4.7 kΩ ≈ **1.9 mA**. For a dimmer LED, raise R210 to 10 kΩ (≈ 0.9 mA).

### TX enable (SPDT RF switch after the buffer)
The oscillator and buffer **run all the time**, and only the buffer's output is steered. The tank therefore sees the same load in both positions, so the carrier doesn't jump when you go from tuning to transmitting. (Turning the buffer off instead would pull the carrier and leak 30–40 dB.)

```
                                     ┌─ RF1 ─ C113 1n ─ 50 Ω ─► J1  ANTENNA   (TX)
buffer ─ C112 ─ 50 Ω ─ RFC  U101 PE4259
                                     └─ RF2 ─ C114 1n ─ 50 Ω ─► J2  TEST      (STBY)
                       VDD ◄─ 3V3 (C115 100 nF)
                       CTRL ◄─ R117 1 kΩ ─┬─ TX_EN
                                          C116 100 nF to GND (debounce, keeps RF off the control line)

        3V3 ──o TX
               \___ S101 common ── TX_EN ──┬── R115 1 kΩ ── D102 red "TX" ── GND
        GND ──o STBY                       └── R116 100 kΩ ── GND (STBY if the switch is mid-travel)
```

- **The physical control:** **S101** is a small SMD slide switch (MSK12C02, right-angle). Its lever sticks out past the board edge, and the silkscreen reads **STBY ◄ ► TX**.
  - It drives `TX_EN` hard to 3V3 or GND, so no logic IC is needed.
  - The 100 kΩ pull-down means a broken switch or a mid-travel position defaults to STBY.
- **TX LED:** **D102** (red) hangs straight off `TX_EN`, so it lights exactly when the switch routes RF to the antenna. Current: (3.3 V − ~2.0 V) / 1 kΩ ≈ 1.3 mA.
- **RF switch:** **U101** is a pSemi PE4259: SPDT, 10 MHz–3 GHz, 0.35 dB insertion loss, ≥ 30 dB isolation (spec; typically more at 100 MHz), 1.8–3.3 V, with single-pin CMOS control.
  - **Pinout (SC-70-6):** 1 RF1, 2 GND, 3 RF2, 4 CTRL, 5 RFC, 6 VDD.
  - **Truth table (datasheet Table 5, VDD = 3 V):** CTRL high = RFC→RF1 (J1 antenna); CTRL low = RFC→RF2 (J2 test).
  - **DC blocking:** the datasheet requires RF pins 1, 3 and 5 to be DC-blocked. C112 blocks RFC; C113 and C114 block RF1 and RF2.
  - **Supply:** VDD comes from the 3V3 rail. The operating maximum is 3.3 V and the absolute maximum is 4.0 V, so the AMS1117's ±1–2 % tolerance is fine.
  - **Symbol:** the PE4259 symbol lives in the project library `fm_modulator.kicad_sym`, registered in the project `sym-lib-table`.
- **Test port:** **J2** is a second vertical through-hole SMA, the same part as J1, so it adds no extra Extended fee. In STBY the RF goes there, into a spectrum analyzer or SDR through an attenuator.
  - Keep a 50 Ω terminator on J2 when you're not measuring, so the buffer always sees 50 Ω.

### How you use it
1. Power up with S101 on **STBY**: green PWR on, red TX off.
2. J2 → 20–30 dB attenuator → analyzer/SDR. Set the carrier with C105 and the deviation with RV201 (±75 kHz).
3. Antenna on J1. Slide to **TX**: the red LED lights and RF goes to J1. The oscillator and buffer conditions don't change, so the carrier stays where you tuned it.
4. Slide back to STBY at any time.

Standby isn't absolute silence. About 30–40+ dB of the switch's isolation still leaks to J1, and the oscillator radiates slightly by itself; a shield can over the oscillator would reduce that. Transmit only on frequencies and at power levels you're permitted to use.

### Cost and load
- **Parts:** Rev B adds two new Extended parts (U101 and S101, about $6 in fees). J1 → BWSMA-KE-Z001 replaces the ~$5 Samtec edge-launch with a ~$0.40 part.
- **Load:** about 3.2 mA extra.
- **Simulation:** all Rev B parts are excluded from simulation. R114 (the 50 Ω simulation load) still sits on RF_Out, so the transient sim behaves as before.

## Design notes and calculations

All numbers below are hand estimates. Confirm them in the transient + FFT simulation.

### Power input
- 12 V on TP5/TP6 → **D201** (SS14, reverse-polarity protection, ~0.3–0.35 V drop at ~33 mA) → **FB201** + C201/C202/C203 → `DC_Bias` ≈ **11.65 V**.
- Current budget: oscillator ~5 mA + buffer ~14 mA + NE5532 ~8 mA + AMS1117 ground current ~5 mA + mic 0.17 mA + dividers → **≈ 33 mA**.
- `VCC_AUDIO` = DC_Bias through R201 (47 Ω, ~13.5 mA) ≈ **11.0 V**. R201 + C204 (corner ≈ 340 Hz) keep op-amp audio current ripple off the oscillator rail; supply ripple on the oscillator is FM noise (pushing).
- `VMID` = VCC_AUDIO / 2 ≈ **5.5 V** (R202/R203 + C206). It is both the op-amp DC operating point and the varactor's reverse bias.
- AMS1117-3.3 from 11.0 V: (11.0 − 3.3) V × ~5.4 mA ≈ 42 mW, which is fine for SOT-223.

### Tank sensitivity (how much a capacitor change moves the frequency)
- L102 = 100 nH at f₀ = 100 MHz → effective tank capacitance C_eff = 1 / ((2πf₀)²·L) = **25.3 pF**.
- The Colpitts pi network puts the collector-side capacitance C_c (C103 + C105 + ~3 pF transistor ≈ 38 pF) in series with the tank-side capacitance C_t (C104 + base branch + buffer + varactor branch). C_eff = C_c·C_t/(C_c+C_t) gives **C_t ≈ 76 pF**.
- A change at Tank_Output reaches C_eff scaled by (C_c/(C_c+C_t))² = (38/114)² = **0.111**.
- K_C = (f₀/2)·0.111/C_eff = 50 MHz × 0.111 / 25.3 pF ≈ **220 kHz per pF at Tank_Output**.
- **Calibrate this in simulation:** change C104 by 1 pF and measure the frequency shift. Every number below scales with it.

### Varactor (D101, 1SV229)
- Model `models/1SV229.lib`: C(V) = 39.9 pF / (1 + V/0.7)^0.665. This is a two-point fit to the listed specs (6.5 pF at 10 V, C2V/C10V = 2.5); check it against the datasheet curve.
- At VMID = 5.5 V: **C = 9.3 pF**, slope **dC/dV ≈ −1.0 pF/V**.
- Through C106 = 10 pF: branch capacitance = 10·9.3/19.3 = 4.8 pF. Its slope is (10/19.3)² × 1.0 = **0.27 pF/V**.
- **Modulator gain K_V = 220 kHz/pF × 0.27 pF/V ≈ 59 kHz/V.**
- **±75 kHz deviation needs 75/59 ≈ 1.27 V peak of audio on AUDIO_OUT.** The NE5532 can swing about ±3.5 V around 5.5 V on an 11 V supply, so the hard limit is about ±200 kHz. RV201 sets the operating level; very loud input will over-deviate.
- RF across the varactor: about 2 V peak on the tank, divided by C106 vs D101 to about 1 V peak on the diode. That stays well inside 5.5 V reverse bias, so the diode never conducts on RF peaks.

### Microphone and audio gain
- IM73A135V01: −38 dBV/Pa (differential) → 12.6 mV rms = **17.8 mV peak at 94 dB SPL (1 Pa)**.
- U1A differential amp: gain R207/R206 = 100k/5.1k = **19.6**, which rejects common-mode noise on the mic lines. The input high-pass (1 µF × 5.1 kΩ) is at 31 Hz.
- U1B non-inverting gain: 1 + RV201/R209 = **1 to 16.2**, with C213 setting DC gain to 1 so the output stays at VMID. Total gain is **19.6 to 318**.
- For ±75 kHz at 94 dB SPL: 1.27 V / (17.8 mV × 19.6) = 3.6 → **RV201 ≈ 8.7 kΩ**.
- At maximum gain (318), full deviation is reached at 1.27 V / 318 = 4.0 mV peak ≈ 0.22 Pa ≈ **81 dB SPL**, which is normal speech at about 10 cm. So RV201 covers full deviation from ~81 dB SPL (pot at max) to ~94 dB SPL (pot at ~8.7 kΩ).
- Possible additions: 75 µs (US) / 50 µs (EU) pre-emphasis in U1B's feedback, and a ~15 kHz low-pass to limit occupied bandwidth.

### Why ±75 kHz and not ±1 MHz deviation
- **Receivers:** broadcast FM uses ±75 kHz deviation on 200 kHz channel spacing, and receiver IF filters are about 150–250 kHz wide. With ±1 MHz the occupied bandwidth (Carson's rule) is 2 × (1 MHz + 15 kHz) ≈ **2 MHz, about 10 channels**. A receiver would only catch the signal as it swept through its IF, giving clipped, distorted audio and interference outside the allowed band.
- **Circuit:** ±1 MHz with ±3.5 V of swing needs K_V ≈ 285 kHz/V, i.e. about 1.3 pF/V at Tank_Output. That exceeds the 1SV229's entire slope at 5.5 V (1.0 pF/V) even with C106 removed. Getting there would need a low bias voltage (where 2 V of RF would forward-bias the diode) or several varactors, and the C–V curvature would then add percent-level audio distortion.
- **Where 1 MHz makes sense is tuning range.** The C105 trimmer (5.8–20 pF) moves C_c from about 31 pF to 45 pF, i.e. C_eff from 21.9 to 28.3 pF, giving roughly **95–107 MHz**. That's about ±6 MHz of channel selection, with ±75 kHz of audio FM on top.

### Simulation notes (closed loop)
- U1, U2, U3, RV201, D201, FB201, the test points and J1 are excluded from simulation (no SPICE models). **V102** (simulation only) stands in for the op-amp output: `dc=5.5` biases the varactor. Set `ampl=1.27 f=200k` to see FM sidebands in the FFT. Use a 200 kHz test tone because a 1 kHz tone needs milliseconds of 100 MHz simulation.
- V101 (simulation only) still provides the 0 → 12 V power-on ramp on DC_Bias.
- ERC shows two `lib_symbol_mismatch` warnings for MMBT3904. They're cosmetic; "Update symbol from library" clears them, but re-check the Sim fields afterwards (`Sim.Library models/2N3904.lib`, `Sim.Name 2N3904`, `Sim.Pins 1=B 2=E 3=C`).
