# Items not included in automatic acceptance

Each item below was examined but is not counted among the 69 automatically judged cases; the reason is given so that no tolerance is widened to make a case pass.

| Item | Reason |
| :--- | :--- |
| HDS-5 Design Example 1.4 outlet control: 5′×5′ square edge H 5.089 ft (CDF 5.2), 6′×5′ H 3.402 ft (CDF 3.55) | Differences of 2.1% and 4.2%; the cause of the differences is not recorded in the project. No special tolerance is set to make them pass, so they are not included (this program's values are still covered by regression unit tests) |
| Pile groups and settlement (pile cap load distribution, Eqs. 5.4-1 to 5.4-3, negative skin friction, consolidation, Converse–Labarre) | The design code has no worked examples; the project compares against independent hand calculations (HyGeoWorks internal validation record, “Pile groups and settlement (no worked examples in the code)”); these are not published reference values |
| Pile axial bearing capacity R4 P-1 to P-4, and the other methods for liquefaction R4 L-1 (NCEER, AIJ, JRA) | Independently implemented examples from research report R4, not design-code examples; only the two items I-01 and I-02 are listed, as “Independent-implementation example (not from literature)” |
| Handbook Debris Flow Part Appendix 4.1: Cd, QDE, hDE, UDE for the sediment-deposit slope (example values 0.21, 58.0, 0.62, 3.04) | The example chains its calculation from the rounded Cde 0.21 (computed value 0.2141) and does not mention the range of Eq. 1.2.7; QDE recomputed from the example's rounded values is 57.87, which still differs from the example's 58.0 by 0.13, so these are not included |
| Check dam example ΣM (Case 1 1745.0, Case 3 1715.0, Case 4 1863.0) | The lever arm of ΔPaev is taken differently (example m2·Hm/3, this program 0.6·m2·Hm); the unit tests compare after removing that term, so this is not a direct comparison |
| USFS Example 4D factor of safety against sliding | The source mistakenly uses 13.47 in the numerator and cos36° for PAH; the unit test compares against the value 0.93 derived in the research report (not the source), so it is not included |
| USBR EM-25 Examples 1 and 3: F1, D2/D1 | The unit tests check these with formulas written inside the tests, not through the library calculation |
| 1D standard step method vs RK4, chute water surface profile vs RK4 | The comparison target is an independent numerical integration, not a published or analytical value |
| Analytical comparisons for the 2D flood drainage network (full-pipe energy equation, inlet weir flow, culvert connections, bottom orifice Torricelli, rectangular/V-notch weir drawdown, pump cycling) and its coupling with buildings, flow barrier lines and detention ponds | Not included in this release; still covered by the 2D flood module's unit tests (values recorded in the HyGeoWorks internal validation record) |
| TWD97 TM2 reference point 23°N 121°E → (250000, 2544283.12) | The source of this reference value is not recorded in the project |
| USLE, sediment yield, outflow control T1, and SCS lag formula conversion | The project has no published worked-example values (T1 is a consistency check of formula conversion; for USLE only the unit plot definition is verified) |
