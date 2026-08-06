# NASCAR Manufacturer Competitive Balance Index

A Herfindahl–Hirschman Index (HHI) analysis of manufacturer concentration in the NASCAR Cup Series championship, 1949–2016. Answers three questions: was the sport ever genuinely "wide open," does concentration track observable events (manufacturer entries/exits, rule changes), and was the sport trending toward more or less balance by the end of the data window.

**[View the report](./nascar_manufacturer_hhi_report.html)** — single self-contained HTML file, no build step required. Just open it in a browser.

## Why HHI

HHI is the standard concentration measure from industrial economics and antitrust review (used by the DOJ/FTC to evaluate market power in merger cases). It maps directly onto sports parity questions: instead of firms' market share, use each manufacturer's share of championships won in a given decade. It's a more rigorous lens than "count the trophies by brand" because it's sensitive to *distribution*, not just who's on top — a 5-way split and a 60/40 split can have the same leader but very different HHI scores.

```
HHI = Σ (championship share_i × 100)²
```

Scale: 0–10,000. Below 1,500 = unconcentrated, 1,500–2,500 = moderately concentrated, above 2,500 = highly concentrated.

## Data

`NASCAR_Champion_History_Dataset.csv` — 68 championship seasons (1949–2016), one row per driver/manufacturer/car-number combination used in that title-winning season.

**Data quirk:** 18 of the 68 seasons have more than one row — the champion drove for more than one manufacturer within the same season (car-number/manufacturer swaps were common before teams settled into exclusive factory deals). None of these seasons had a tie for most wins, so each title was attributed to the manufacturer the champion won the *most races* with that year, not just whichever they started the season in. Every multi-manufacturer season falls at or before 1983 — after that, champions stuck with one manufacturer for the full year, a small signal of the sport professionalizing.

## Key findings

1. **The 1960s were the genuinely competitive era** — lowest HHI in the dataset (2,200), five manufacturers, no one over 30% of titles.
2. **Concentration tracks manufacturer exits almost mechanically** — Plymouth (1977), Mercury/Dodge (early '80s), Oldsmobile/Buick (mid-90s) all leaving the grid lines up with HHI climbing to a 1990s peak of 6,800 (a near-duopoly).
3. **New entrants (Toyota, 2007) only partially reverse it** — 2000s HHI drops to 4,400, but Chevrolet hasn't taken less than 50% of titles in any decade since the 1980s.
4. **No return to parity by the end of the window** — the partial 2010s (2010–2016) sit at 5,510, higher than the 2000s. Trend within this dataset is toward re-concentration, not away from it.

## Tech

Single HTML file, Chart.js (line chart with concentration-zone shading + stacked bar for manufacturer composition), no framework or build step. Pandas/Python used for the HHI computation and decade aggregation (not included in this repo — happy to add the analysis notebook on request).

## Limitations

- Dataset stops at 2016; the "is it trending toward more balance *recently*" question is only answered up to that point from the numbers here. Chevrolet went on to win 5 consecutive titles 2021–2025, which would extend the concentration trend if the index were updated — noted in the report but not built into the index since full 2017–2025 manufacturer data isn't in this dataset.
- The 1940s decade is a single season (1949, NASCAR's inaugural year) and is excluded from the trend narrative — its HHI of 10,000 is a data-availability artifact, not a real finding.
- The 2010s decade is partial (7 of 10 years) and should be read as a soft signal, not a completed trend.
