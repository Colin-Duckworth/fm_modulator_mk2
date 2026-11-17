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
| J1 | 1 | SMA edge-launch | Samtec EM1 | C5199907 | Extended | SMA-J-P-H-ST-EM1 (Samtec) | RF out, ~$5; or hand-solder |
| TP3, TP4 | 2 | Test loop | Keystone 5015 SMD | C2906768 | **Hand-solder** | 5015 (Keystone) | MIC_IN, OPAMP_OUT; excluded from JLC BOM/CPL, order separately |
| TP5 | 1 | +12V_IN, red | Keystone 5010 THT | C2906765 | **Hand-solder** | 5010 (Keystone) | Alligator-clip power input; excluded from JLC BOM/CPL, order separately |
| TP6 | 1 | GND, black | Keystone 5011 THT | C238127 | **Hand-solder** | 5011 (Keystone) | Alligator-clip ground; excluded from JLC BOM/CPL, order separately |
| TP1 | 1 | Test pad | 1.0 mm pad | — | — | bare copper | No part to place (excluded from BOM/CPL) |
| R114, V101, V102 | — | — | — | — | — | — | **Simulation only**: excluded from BOM and board |

**Summary:** JLC assembles 37 unique parts. 28 are Basic, covering all resistors except R112, all but one fixed capacitor, both transistors, the op amp, the LDO, the diode and the ferrite. 9 are Extended (C109, C105, L101, L102, D101, U2, RV201, J1, R112), roughly $27 in setup fees. The four test loops (TP3–TP6) are hand-soldered: their footprints are on the board, but they're marked *exclude from BOM* and *exclude from position files* in KiCad, so JLC leaves the pads empty. Order them separately (LCSC numbers above, about 2× 5015, 1× 5010 red, 1× 5011 black). TP1 is a bare pad with no part.

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

### 50 Ω RF output (C112 → J1)
- **Geometry:** microstrip on L1 referenced to the L2 ground plane, h = 0.2104 mm, t = 0.035 mm, εr = 4.4.
- **Width:** Hammerstad–Jensen with thickness correction gives Z₀ = 50 Ω at **w = 0.373 mm** bare (51.0 Ω at 0.36 mm). Solder mask lowers Z₀ by about 1–2 Ω, so the line is drawn at **0.36 mm** (≈ 50 Ω under mask). Confirm with JLC's impedance calculator before ordering.
- **Length:** about 11.6 mm. At 100 MHz that's only ~2.5° (λg ≈ 1.68 m, ε_eff ≈ 3.19), so the line is electrically short and the match is really set by the source and load. The source is the buffer: R112 = 68 Ω gives Z_out ≈ 50 Ω, so the source, line and SMA are all ≈ 50 Ω.
- **Ground:** the L1 GND pour is held back ≥ 0.6 mm (≈ 3h) from the line by a rule area, so it behaves as microstrip rather than coplanar. A via fence (GND vias every 2 mm, 1.3 mm either side) runs along it, and the SMA's ground pads are via'd to L2.
- **Connector:** J1 is the Samtec SMA-J-P-H-ST-EM1 edge-launch, rated for a 1.6 mm board, placed so its board-edge marker sits on the right board edge.

### Layout
- **Board:** 60 × 45 mm, four M3 mounting holes (3.2 mm NPTH) in the corners.
- **Floorplan (left → right):** audio section (mic U2, LDO U3, op amp U1, RV201, VMID divider) top-left; the varactor D101 and C106 right at the tank node; Colpitts core (Q101, L102, C102–C105, L101/R101) in the middle; RF buffer (Q102) then the 50 Ω line to the SMA on the right edge. Power entry is along the bottom edge: TP6 (GND), TP5 (+12 V), D201, FB201, C201–C203. The clip loops are 8 mm apart.
- **Routed by script (L1):** the whole oscillator, varactor feed, buffer, the 50 Ω line and the power entry.
- **Vias:** every GND pad has its own via to L2, and every DC_Bias / VCC_AUDIO pad has a via to its L3 plane. R201 straddles the L3 split, so it bridges DC_Bias → VCC_AUDIO. About 80 stitching vias are on a 4 mm grid.
- **Pours:** L1 GND, L2 GND, L3 DC_Bias / VCC_AUDIO, L4 GND.
- **Net classes:** RF (/RF_Out) 0.36 mm, Power (DC_Bias, VCC_AUDIO, 3V3) 0.5 mm, Default 0.25 mm.
- **JLC design rules:** 0.15 mm minimum track and clearance, 0.3/0.6 mm vias, 0.3 mm copper-to-edge.
- **Silkscreen:** the bottom carries the project tag (name, date, revision); the top labels +12V, GND and RF OUT 50R.

### Still to do in KiCad
1. **Route the remaining nets (DRC shows 25 unconnected), preferably on L4:** AUDIO_OUT (U1 pin 7, RV201, TP4, R208), VMID, the mic outputs → C210/C211 → R204/R206 → U1, the U1 feedback nets, and **3V3** (U3 → C208 → C209 → U2 VDD).
2. **Refill zones** (B), then run DRC.
3. **Tidy silkscreen:** about 100 overlap warnings, from reference designators crowding the dense oscillator cluster.
4. **Mic hole-clearance error:** one DRC error comes from the Infineon footprint itself (its centre GND pad sits 0.18 mm from its own sound hole). Exclude it in the DRC dialog.
5. **Optional:** Update PCB from Schematic (F8) should report nothing to change; footprints are already linked to their symbols.

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
