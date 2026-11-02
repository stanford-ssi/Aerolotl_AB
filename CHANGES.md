# aerolotl_ab: changes from aerolotl rev2

**Removed (old reference designators):**

- The whole Igniter sheet: Q5–Q8, J5, J14, F3, F4, D7, D8, D11, D12, R5, R6, R39–R46, R52, R68–R73, C46, C47, C50, C52, C85, C86, TP6–TP10
- SW4, the arm switch. It fed only `+12V_ARM`.
- D6/R27, the ARM LED.

The freed MCU pins (22, 23, 61, 62) are marked no-connect.

**Both boards:**

- Every previously unnamed net now has a label: 33 on AB, 38 on AV.
- GPS decoupling caps C4/C5 got footprints and were placed on the PCB.
- Power netclasses were added.
- Everything was reannotated in sheet order, top-to-bottom and left-to-right within each sheet.
- Non-standard prefixes were normalized: CS/CIO → C, Card/CN → J, LED → D, X → Y, SAW → FL.

## Reference map (old → new)

**mcu**: C24→C1, C55→C2, C56→C3, C57→C4, C58→C5, C59→C6, C60→C7, C75→C8, C69→C9, C70→C10, C76→C11, C65→C12, C66→C13, C73→C14, C74→C15, C67→C16, C68→C17, C71→C18, C72→C19, FB3→FB1, H1→H1, H2→H2, R2→R1, R3→R2, R65→R3, SW2→SW1, SW1→SW2, U14→U1, X1→Y1, Y3→Y2

**swd**: J1→J1, R4→R4

**power**: BT3→BT1, BT4→BT2, BT5→BT3, C39→C20, C31→C21, C34→C22, C37→C23, C38→C24, C41→C25, C2→C26, C1→C27, C3→C28, D9→D1, J4→J2, J3→J3, L3→L1, Q4→Q1, R1→R5, R8→R6, R9→R7, R15→R8, R16→R9, R10→R10, R7→R11, R11→R12, R48→R13, R13→R14, R14→R15, TP1→TP1, TP2→TP2, TP3→TP3, TP4→TP4, TP5→TP5, U5→U2, U4→U3, U2→U4, U3→U5

**sensors**: AE1→AE1, C45→C29, CIO2→C30, C48→C31, CS2→C32, C4→C33, C5→C34, CS1→C35, CIO1→C36, C43→C37, C42→C38, SAW2→FL1, R47→R16, R17→R17, R18→R18, U10→U6, U1→U7, U6→U8, U9→U9, U7→U10

**indicators**: BZ1→BZ1, C49→C39, C44→C40, LED1→D2, D2→D3, D3→D4, D4→D5, Q1→Q2, R19→R19, R20→R20, R21→R21, R23→R22, R24→R23, R25→R24, R22→R25

**sd**: Card1→J4, R34→R26, R35→R27, R36→R28, R37→R29, R38→R30, R29→R31, R31→R32, R30→R33, R32→R34, R28→R35, R33→R36

**external**: C77→C41, C78→C42, C79→C43, C80→C44, C81→C45, C82→C46, C83→C47, C84→C48, D10→D6, F7→F1, F8→F2, F9→F3, F10→F4, J17→J5, J10→J6, CN1→J7, CN2→J8, J8→J9, J13→J10, J16→J11, J11→J12, J7→J13, J18→J14, J19→J15, J20→J16, J21→J17, R66→R37, R67→R38

**airlift**: U12→U11


## PCB routing, 2026-11-01 / 11-02

**Schematic:** unchanged from commit 4206fce. Only the PCB changed.

**Unconnected items:** 124 (4206fce) → 4. DRC with zones refilled and schematic parity: 0 footprint errors, and the copper findings are the same 23 as on 4206fce (12 footprint-internal clearances, 9 hole clearances incl. D1 vs BT3's peg hole, 1 solder-mask bridge, the LED.B dangling stub).

### Still open (4)

All four are on U1's bottom pin row (pins 41–46), which is boxed in by the SPI1 and PE7–PE10 fan-out:
- SPI4.SCK (U1.42 → J5.4) and SPI4.MISO (U1.43 → J5.3)
- GPIO PE11 (U1.41 → J11.6)
- I2C2.SCL (U1.46 → J8.4)

### Footprints moved

None in the 11-02 pass. Earlier, to make the crystal corner and SD lines routable:
- Y1 and Y2 rotated 180°. They were mirrored relative to the pins they serve.
- C18 and C19 swapped places, so the LSE lines don't cross.
- C1 rotated to horizontal at (135.75, 71.55), clear of the U1 pin row.
- R31, R33, R35 and R36 rotated 180° to open a path for SD DAT3.

### 11-02: the last open signals

Newly connected:
- USB_D− (U4.6 → U1.70): 0.25 mm, same as the hand-routed D+.
- SERVO_UART (U1.82 → R37/R38).
- T_NRST to the debug header (J1.12). This was already open on 4206fce.
- SPI1.INT_BMP (U10.7 → U1.96).
- GPIO PE6 (U1.5 → J10.6).

To make room, parts of these signal traces were re-routed:
- T_SWO, T_VCP_TX
- I2C1.SDA, I2C1.SCL, I2C2.SDA
- SPI4.MOSI, UART8_TARGET_RX
- GPIO PE4, PE5
- BOOT0, PWR_STS
- BUZZER, LED.G
- SDMMC1.D0, D1, D3
- SPI1.SCK, SPI1.CS_BMP
- SPI2.MOSI, SPI2.SCK, SPI2.BUSY

The new copper is 0.2 mm with 0.6/0.3 mm vias, and clears the netclass rules: USB tracks keep 0.2032 mm.

USB_D+ tidy-up:
- Removed the via at (123.70, 119.18). It only touched F.Cu, where the track already runs through.
- Removed two duplicate vias stacked at (155.55, 66.75).

### 11-01: power, servo ports, crystal corner

**Servo ports (J14–J17):** fully routed.
- Each fuse (F1–F4) drops to the +12V plane.
- Fuse → 100 µF / 100 nF caps → connector pin 2, at 1.3 mm (0.8 mm for a few short pieces).
- The servo bus daisy-chains J14–J17 pin 3 with D6 and R38.

**Buck converter (U2):** laid out compactly.
- **Switch node:** U2.2 → under the U2 body → over U2.1/U2.6 → L1. 0.5 mm, F.Cu only, no vias (0.4 mm where it passes under the body).
- **Bootstrap (CB):** a short B.Cu hop under the switch node, then up beside C23 to C20.1.
- **EN, C23 and the +12V feed:** they meet on B.Cu. VIN goes straight to C24.
- **R9.2:** gets its GND via. It was open, which would have left the buck regulating to ~0.6 V.

**BMI088 (U6) supply:** both supply pins were unrouted; they now connect to +3V3.
- **VDD (pin 3):** gets a +3V3 via just above the pin. To make room, the GND stubs of pins 2 and 4 were re-routed to the existing GND via at (144.03, 88.60), and their two vias were removed.
- **VDDIO (pin 11):** gets a 0.5/0.3 mm +3V3 via inside the MISO loop. To make room, SPI2.BUSY's U-turn under U6 moved 0.7 mm east (x 146.7 → 147.4, below the U6 GND via).

**Crystal corner (left of U1).** As placed on 4206fce, neither crystal could be routed, and the PE2/PE3/VOLT_SENSE/T_NRST traces ran straight through the crystal area. Besides the footprint moves above:
- **HSE** (HS_OSC_A/B): F.Cu only, no vias. U1.12/13 → Y1 → C14/C15.
- **LSE** (LS_OSC_A/B): F.Cu only, no vias. U1.8/9 go up through the gap between C8 and C3 → Y2 → C19/C18.
- **PE2, PE3, VOLT_SENSE:** now go around the crystals instead of through them.
  - They drop to B.Cu next to C8 and run west in the band between SDMMC1.D3 and BOOT0.
  - Then they run down alongside BOOT0, three lanes 0.6 mm apart, and hop over I2C1.SCL on F.Cu beside SW2.
  - Each lands on its original copper: VOLT_SENSE via (124.75, 75.20), PE2 via (127.95, 78.40), and PE3 on its original diagonal at (128.58, 80.73).
- **T_NRST:** U1.14/C1.1 rejoin the under-chip B.Cu run with a new via at (137.05, 70.65). R1.2 hops on B.Cu under the crystals to the via at (126.60, 61.70) and to SW2's via (121.35, 68.05).
- **Plane fan-outs:**
  - C3.1 (+3V3) connects straight to U1.11 instead of through a via.
  - The GND vias of C3.2, C14.2 and C18.2 moved slightly.
  - The old C1 GND via at (136.65, 70.12) was removed.

**Also routed on 11-01:** SPI1.MOSI (U1.31), SPI1.CS_IMU_ACC (U1.84 → U6.14), SD CARD_DAT3, the +12V feed to U2.3, I2C4.SCL and BUZZER.

**Widths follow the netclasses:**
- **PWR_HI:** +BATT 2.0 mm. +12V 2.0/1.0 mm, and 0.5 mm on the buck-input branch, with a 0.3 mm neck at U2.3 (well under 1 A).
- **PWR_LO:** 0.5 mm. It necks to 0.3/0.2 mm only at fine-pitch pins (U5 SOT-583, U4 SOT-666, U1); +3.3VA has 0.2/0.3 mm sections.
- **GND/+3V3 plane fan-outs:** 0.25 mm, like the existing stubs.
- **Signals:** 0.2 mm, except a 0.15 mm neck on 2 short BUZZER pieces at U1.67, next to a via.
- **Vias:** 0.6/0.3, and 0.8/0.4 on PWR_HI.
