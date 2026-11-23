# HydroStudio verification benchmarks

Public benchmark data for the **HyGeoWorks HydroStudio** calculation core (hydrology, hydraulics, detention, slope stability, retaining walls, check dams, 2D flood and coordinate transformation).
The same Rust calculation core runs the Windows desktop program, the `hydro` command line and the browser calculators at [hygeoworks.com](https://hygeoworks.com/).

**Release 1.0.2, run 2026-11-23: 69 of 69 cases pass** (failed 0, errors 0).
Reference values by kind: Published example / tabulated value 51; Analytical solution 7; Verification example from other software 9; Independent-implementation example (not from literature) 2.

Key cross-check metrics:
- **EPA SWMM 5.2.4** (`X-01`–`X-04`): free-surface drainage peak flow diff **<= 0.02%**, NSE **>= 0.9997**; HEC-22 inlets (142 cases) max relative diff **0.019%** (see [`EXTERNAL.md`](EXTERNAL.md)).
- **Rocscience Slide2** verification examples (`S-03`–`S-07`, `S-10`, `S-11`): factor of safety within **±0.005** for slopes with a horizontal support, micropiles, soil nails and five reinforcement layers.
- **Browser WebAssembly vs. Desktop parity**: **376 cases / 101,613 values** compared on 2026-11-13 with largest relative difference **`<= 4.9 × 10⁻¹⁶`**.
- **Documented errata**: in **11 cases** the published value contains a misprint, an irreproducible reading or rounded intermediates; it is kept unaltered and the target actually checked is documented in [`ERRATA.md`](ERRATA.md).

This repository contains data only: case definitions, reference values and sources, tolerances, computed values and results. It contains no source code, no data library and no licensing code.

## Results by group

| Group | Cases | Pass |
| :--- | ---: | ---: |
| Hydrology | 10 | 10 |
| Culverts | 7 | 7 |
| Hydraulics (energy dissipation, debris flow) | 5 | 5 |
| Detention ponds and site water retention | 4 | 4 |
| Slope stability | 14 | 14 |
| Retaining walls, MSE walls, gabions | 13 | 13 |
| Check dams | 5 | 5 |
| Foundation bearing capacity | 2 | 2 |
| 2D flood inundation | 3 | 3 |
| Coordinate transformation | 2 | 2 |
| Project workflow (embedded project file, via the project-file runner) | 2 | 2 |
| Liquefaction and piles (independent-implementation examples, not from literature) | 2 | 2 |

- [`cases.csv`](cases.csv) / [`cases.json`](cases.json): every case with its published reference value, the target actually checked (`target`, equal to the reference unless listed in `ERRATA.md`) and its basis, source, tolerance, computed value, difference from the target and result (English; the original Traditional Chinese title is kept in `cases.json`). The computed values are those of the release executable listed in `cases.json` (`meta`).
- [`ERRATA.md`](ERRATA.md): side-by-side table of the 11 cases with published example misprints or target adjustments.
- [`EXTERNAL.md`](EXTERNAL.md): comparisons with EPA SWMM 5.2.4 and GDAL/PROJ (recorded values).
- [`EXCLUDED.md`](EXCLUDED.md): items examined but not counted, with the reason.
- [`CITATION.cff`](CITATION.cff): citation metadata for GitHub's "Cite this repository" panel.

## Try the same core online (no installation)

Browser calculators compile the identical Rust calculation core to WebAssembly (`<= 4.9 × 10⁻¹⁶` relative difference vs. desktop); trial inputs stay locally in your browser:

- **International (SI, English)**: [https://hygeoworks.com/en/tools/](https://hygeoworks.com/en/tools/) · [Benchmarks](https://hygeoworks.com/en/benchmarks/)
- **United States (US customary units)**: [https://hygeoworks.com/us/tools/](https://hygeoworks.com/us/tools/)
- **Taiwan (繁體中文)**: [https://hygeoworks.com/tw/tools/](https://hygeoworks.com/tw/tools/) · [驗證紀錄](https://hygeoworks.com/benchmarks/)
- **Japan (日本語)**: [https://hygeoworks.com/ja/tools/](https://hygeoworks.com/ja/tools/) · [検証事例](https://hygeoworks.com/ja/benchmarks/)
- **Free licences for PE reviewers and university faculty**: [https://hygeoworks.com/en/verify/#academic-reviewer-license](https://hygeoworks.com/en/verify/#academic-reviewer-license)

## Benchmark groups you can also run online

These browser calculators run the same calculation core as the cases below (enter the case inputs yourself; trial inputs stay in your browser):

| Group | Cases | Online calculator |
| :--- | :--- | :--- |
| Culverts (FHWA HDS-5, HY-8 inlet control, outlet control) | C-01 – C-07 | [US customary](https://hygeoworks.com/us/tools/culvert-hydraulics/) · [SI](https://hygeoworks.com/en/tools/culvert-hydraulics/) · [繁體中文](https://hygeoworks.com/tw/tools/culvert-hydraulics/) · [日本語](https://hygeoworks.com/ja/tools/culvert-hydraulics/) |
| Slope stability, circular slip surface (simplified Bishop) | S-01 | [SI](https://hygeoworks.com/en/tools/slope-stability-bishop/) · [US customary](https://hygeoworks.com/us/tools/slope-stability-bishop/) · [繁體中文](https://hygeoworks.com/tw/tools/slope-stability-bishop/) · [日本語](https://hygeoworks.com/ja/tools/slope-stability-bishop/) |
| Cantilever retaining wall (Taiwan Soil and Water Conservation Handbook example) | W-01 – W-05 | [繁體中文](https://hygeoworks.com/tw/tools/retaining-wall/) |
| Building-site water retention (Taiwan technical regulations) | D-01 – D-03 | [繁體中文](https://hygeoworks.com/tw/tools/site-water-retention-tw/) |

The other groups (noncircular, reinforced and seismic slopes, MSE and gabion walls, check-dam stability, stilling basins and debris flow, bearing capacity factors, 2D flood inundation, coordinate transformation and the project workflow cases) run in the desktop program; see "Reproduce the results yourself" below.

## Reproduce the results yourself

1. Download and install the free trial of HydroStudio for Windows 10/11 (64-bit): [https://hygeoworks.com/en/downloads/](https://hygeoworks.com/en/downloads/). No licence, card or account is needed; the benchmarks run in trial mode.
2. Open a terminal in the installation folder (by default `C:\Program Files\HyGeoWorks`) and run:

   ```
   hydro.exe verify-benchmarks --include-slow --out results
   ```

3. Compare `results\benchmarks.json` (and `benchmarks.md`, `.xlsx`, `.docx`, written in Traditional Chinese) with [`cases.json`](cases.json), whose computed values come from the release executable with SHA-256 `b3e35e56456bb8c497e02e905b82d64b4c54afd0c7ec46e12850ead358180261`.

`hydro.exe verify-benchmarks --list` prints every case with its reference value and source. Runs are deterministic: the same release gives the same computed values.

## What these benchmarks do and do not show

They check the calculation core against published worked examples, tabulated values, other programs' verification examples and analytical solutions, each with a stated tolerance. They do not replace engineering judgment, site investigation or the review and sign-off of a licensed professional engineer. Where a published example contains an error, the error and its effect are recorded instead of widening the tolerance (see [`ERRATA.md`](ERRATA.md), [`EXCLUDED.md`](EXCLUDED.md) and the verification page).

- Verification page (case tables, errata): [https://hygeoworks.com/en/benchmarks/](https://hygeoworks.com/en/benchmarks/) · [https://hygeoworks.com/benchmarks/](https://hygeoworks.com/benchmarks/)
- Check a calculation report's verification code: [https://hygeoworks.com/en/verify/](https://hygeoworks.com/en/verify/)

## 繁體中文

本倉庫公開 HyGeoWorks HydroStudio 計算核心之 69 項驗證基準資料（1.0.2 版，2026-11-23 執行，通過 69 項）：案例、參考值與出處、判定目標與勘誤依據、容許差、計算值與判定，不含原始碼、資料庫與授權機制。安裝免費試用評估版後，於安裝資料夾執行 `hydro.exe verify-benchmarks --include-slow --out results` 即可自行重現。

- 案例逐項表與勘誤見 [https://hygeoworks.com/benchmarks/](https://hygeoworks.com/benchmarks/) · 免安裝線上計算工作臺：[https://hygeoworks.com/tw/tools/](https://hygeoworks.com/tw/tools/)
- 可於線上以同一計算核心試算之案例組：涵洞 HDS-5（C-01～C-07）[https://hygeoworks.com/tw/tools/culvert-hydraulics/](https://hygeoworks.com/tw/tools/culvert-hydraulics/)、圓弧滑動簡化 Bishop 法（S-01）[https://hygeoworks.com/tw/tools/slope-stability-bishop/](https://hygeoworks.com/tw/tools/slope-stability-bishop/)、水土保持手冊懸臂式擋土牆例題（W-01～W-05）[https://hygeoworks.com/tw/tools/retaining-wall/](https://hygeoworks.com/tw/tools/retaining-wall/)、建築基地保水（D-01～D-03）[https://hygeoworks.com/tw/tools/site-water-retention-tw/](https://hygeoworks.com/tw/tools/site-water-retention-tw/)；其餘案例組以桌面版執行
- 審查委員與大專教師免費授權申請：[https://hygeoworks.com/verify/#academic-reviewer-license](https://hygeoworks.com/verify/#academic-reviewer-license)

## 日本語

HyGeoWorks HydroStudio の計算コアの検証ベンチマーク 69 件（1.0.2 版、2026-11-23 実行、69 件合格）のデータを公開しています。事例、参照値と出典、許容差、計算値と判定のみで、ソースコード・データベース・ライセンス機構は含みません。無料の評価版をインストールし、インストール先で `hydro.exe verify-benchmarks --include-slow --out results` を実行すると、同じ結果を確認できます。

- 検証事例の概要・試用版：[https://hygeoworks.com/ja/benchmarks/](https://hygeoworks.com/ja/benchmarks/) · [https://hygeoworks.com/ja/downloads/](https://hygeoworks.com/ja/downloads/)
- インストール不要のオンラインツール：[https://hygeoworks.com/ja/tools/](https://hygeoworks.com/ja/tools/)
- オンラインツールで同じ計算コアを試せる事例：カルバート HDS-5（C-01～C-07）[https://hygeoworks.com/ja/tools/culvert-hydraulics/](https://hygeoworks.com/ja/tools/culvert-hydraulics/)、円弧すべり 簡易 Bishop 法（S-01）[https://hygeoworks.com/ja/tools/slope-stability-bishop/](https://hygeoworks.com/ja/tools/slope-stability-bishop/)。その他の事例はデスクトップ版で実行します
- 審査担当者・大学教員向け無料ライセンス：[https://hygeoworks.com/ja/verify/#academic-reviewer-license](https://hygeoworks.com/ja/verify/#academic-reviewer-license)

## License

The data and documents in this repository are licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Cite as: Ascend Neural, LLC (HyGeoWorks), *HydroStudio verification benchmarks*, release 1.0.2.
HydroStudio itself is commercial software and is not covered by this licence.
