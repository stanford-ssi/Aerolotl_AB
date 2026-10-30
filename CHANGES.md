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

