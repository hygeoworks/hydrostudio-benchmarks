# HydroStudio verification benchmarks

Public benchmark data for the **HyGeoWorks HydroStudio** calculation core (hydrology, hydraulics, detention, slope stability, retaining walls, check dams, 2D flood and coordinate transformation).
The same Rust calculation core runs the Windows desktop program, the `hydro` command line and the browser calculators at [hygeoworks.com](https://hygeoworks.com/).

**Release 1.0.0, run 2026-11-21: 69 of 69 cases pass** (failed 0, errors 0).
Reference values by kind: Published example / tabulated value 51; Analytical solution 7; Verification example from other software 9; Independent-implementation example (not from literature) 2.

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

- [`cases.csv`](cases.csv) / [`cases.json`](cases.json): every case with its reference value, source, tolerance, computed value and result (English; the original Traditional Chinese title is kept in `cases.json`). The computed values are those of the release executable listed in `cases.json` (`meta`).
- [`EXTERNAL.md`](EXTERNAL.md): comparisons with EPA SWMM 5.2.4 and GDAL/PROJ (recorded values).
- [`EXCLUDED.md`](EXCLUDED.md): items examined but not counted, with the reason.

## Reproduce the results yourself

1. Download and install the free trial of HydroStudio for Windows 10/11 (64-bit): [https://hygeoworks.com/en/downloads/](https://hygeoworks.com/en/downloads/). No licence, card or account is needed; the benchmarks run in trial mode.
2. Open a terminal in the installation folder (by default `C:\Program Files\HyGeoWorks`) and run:

   ```
   hydro.exe verify-benchmarks --include-slow --out results
   ```

3. Compare `results\benchmarks.json` (and `benchmarks.md`, `.xlsx`, `.docx`, written in Traditional Chinese) with [`cases.json`](cases.json), whose computed values come from the release executable with SHA-256 `739d2eb756cda874c826237aefe701356f2df6049ba484538139cab499f17e33`.

`hydro.exe verify-benchmarks --list` prints every case with its reference value and source. Runs are deterministic: the same release gives the same computed values.

## What these benchmarks do and do not show

They check the calculation core against published worked examples, tabulated values, other programs' verification examples and analytical solutions, each with a stated tolerance. They do not replace engineering judgment, site investigation or the review and sign-off of a licensed professional engineer. Where a published example contains an error, the error and its effect are recorded instead of widening the tolerance (see `EXCLUDED.md` and the verification page).

- Verification page (case tables, errata): [https://hygeoworks.com/en/benchmarks/](https://hygeoworks.com/en/benchmarks/) · [https://hygeoworks.com/benchmarks/](https://hygeoworks.com/benchmarks/)
- Check a calculation report's verification code: [https://hygeoworks.com/en/verify/](https://hygeoworks.com/en/verify/)

## 繁體中文

本倉庫公開 HyGeoWorks HydroStudio 計算核心之 69 項驗證基準資料（1.0.0 版，2026-11-21 執行，通過 69 項）：案例、參考值與出處、容許差、計算值與判定，不含原始碼、資料庫與授權機制。安裝免費試用評估版後，於安裝資料夾執行 `hydro.exe verify-benchmarks --include-slow --out results` 即可自行重現。案例逐項表與勘誤見 [https://hygeoworks.com/benchmarks/](https://hygeoworks.com/benchmarks/)。

## 日本語

HyGeoWorks HydroStudio の計算コアの検証ベンチマーク 69 件（1.0.0 版、2026-11-21 実行、69 件合格）のデータを公開しています。事例、参照値と出典、許容差、計算値と判定のみで、ソースコード・データベース・ライセンス機構は含みません。無料の評価版をインストールし、インストール先で `hydro.exe verify-benchmarks --include-slow --out results` を実行すると、同じ結果を確認できます。

## License

The data and documents in this repository are licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Cite as: Ascend Neural, LLC (HyGeoWorks), *HydroStudio verification benchmarks*, release 1.0.0.
HydroStudio itself is commercial software and is not covered by this licence.
