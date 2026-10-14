# 1. Tiered quarantine: outbreak probability tables

- [Transmission rate check](#transmission-rate-check)
- [Results by school](#results-by-school)

Tiered-quarantine experiment using the three real per-capita SMART
contact matrices (symmetrised for reciprocity, kept at real magnitude).
R0 = 12 is reached through a per-school transmission rate, not by
scaling the matrix.

For each school we report **P(outbreak e 10 / 20 / 50 cases)** across
vaccination coverage and quarantine strategies, written as **high /
medium / low-risk contact quarantine days**.

The diagnostic single-tier scenarios in the first table do not satisfy
high e medium e low; that constraint is applied to every other analysis.

**Difference from the reference.** Each strategy is compared with a
reference scenario in the same school and at the same vaccination
coverage: *No quarantine* for the no-vaccination table, and *21/21/21*
for the tiered tables. The “Difference” columns give the strategy’s
outbreak probability minus the reference’s, in **percentage points**,
with a 95% confidence interval (Newcombe hybrid score method for a
difference of two proportions).

- A **positive** difference means more outbreaks than the reference; a
  **negative** one means fewer.
- If the interval **includes 0**, the strategy cannot be told apart from
  the reference with this number of simulations.

Every school × scenario is simulated with its own random seed, so the
scenarios are independent samples, as the interval assumes. The interval
reflects simulation (Monte Carlo) uncertainty only, not uncertainty in
the model’s assumptions.

<div>

> **Note**
>
> Model code lives in `measles_model.R`. Simulations are cached in
> `results/`; delete the CSV to re-run. For a quick test render with
> `N_SIMS=200 quarto render 01_tiered_quarantine_tables.qmd`.

</div>

## Transmission rate check

Each school gets its own transmission rate so that R0 = 12. The table
checks this against `epiworldR::compute_reproduction_number()`.

| School     | Students | Transmission rate |  R0 |
|:-----------|---------:|------------------:|----:|
| Elementary |      156 |            0.0886 |  12 |
| Middle     |      236 |            0.0455 |  12 |
| High       |      232 |            0.0741 |  12 |

## Results by school

*Unvaccinated students* is the number of students without vaccine at
that coverage (enrolment × (1  coverage)). Only these students can be
quarantined, and an outbreak can only grow beyond this number through
rare vaccine failures.

Differences are in percentage points with 95% confidence intervals. For
example, **+3.1 (+1.2 to +5.0)** means the strategy has 3.1 percentage
points more chance of that outbreak size than the reference.

### Elementary

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |    Difference P(≥10) |      Difference P(≥20) |      Difference P(≥50) |
|:---------------------|----------------------:|-------:|-------:|-------:|---------------------:|-----------------------:|-----------------------:|
| No quarantine        |                   156 |  97.4% |  97.4% |  97.0% |            Reference |              Reference |              Reference |
| Only high-risk (21d) |                   156 |  88.4% |  84.5% |  66.5% | -9.0 (-10.1 to -7.9) | -12.8 (-14.1 to -11.6) | -30.5 (-32.1 to -28.9) |
| Only med-risk (21d)  |                   156 |  96.0% |  96.0% |  93.2% |  -1.4 (-2.2 to -0.6) |    -1.4 (-2.2 to -0.6) |    -3.8 (-4.8 to -2.9) |
| Only low-risk (21d)  |                   156 |  96.5% |  92.8% |  27.3% |  -0.8 (-1.6 to -0.1) |    -4.5 (-5.5 to -3.6) | -69.8 (-71.2 to -68.2) |

**Tiered strategies (high/medium/low days)**, compared with 21/21/21 at
the same coverage

*50% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    78 |  52.9% |  25.0% |   0.2% |              Reference |              Reference |           Reference |
| 21/14/14 |                    78 |  56.0% |  27.0% |   0.1% |    +3.1 (+0.9 to +5.3) |    +2.0 (+0.1 to +3.9) | -0.1 (-0.3 to +0.1) |
| 21/7/7   |                    78 |  60.9% |  38.3% |   0.5% |   +7.9 (+5.8 to +10.1) | +13.3 (+11.3 to +15.4) | +0.3 (+0.0 to +0.6) |
| 21/0/0   |                    78 |  70.3% |  56.5% |   4.5% | +17.4 (+15.3 to +19.5) | +31.6 (+29.5 to +33.6) | +4.2 (+3.6 to +4.9) |

*60% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    62 |  44.3% |  15.8% |   0.0% |              Reference |              Reference |           Reference |
| 21/14/14 |                    62 |  46.6% |  17.3% |   0.0% |    +2.4 (+0.2 to +4.5) |    +1.5 (-0.1 to +3.2) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    62 |  51.7% |  26.2% |   0.1% |    +7.4 (+5.2 to +9.6) |  +10.4 (+8.6 to +12.2) | +0.0 (-0.1 to +0.2) |
| 21/0/0   |                    62 |  59.1% |  42.5% |   0.4% | +14.9 (+12.7 to +17.0) | +26.8 (+24.9 to +28.7) | +0.4 (+0.2 to +0.6) |

*70% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    47 |  28.3% |   4.8% |   0.0% |              Reference |              Reference |           Reference |
| 21/14/14 |                    47 |  30.9% |   5.5% |   0.0% |    +2.6 (+0.6 to +4.6) |    +0.6 (-0.3 to +1.6) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    47 |  37.6% |  10.9% |   0.0% |   +9.3 (+7.2 to +11.3) |    +6.1 (+5.0 to +7.3) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    47 |  46.3% |  23.1% |   0.0% | +18.0 (+15.9 to +20.0) | +18.2 (+16.8 to +19.7) | +0.0 (-0.1 to +0.1) |

*80% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|--------------------:|--------------------:|
| 21/21/21 |                    31 |  13.0% |   0.5% |   0.0% |              Reference |           Reference |           Reference |
| 21/14/14 |                    31 |  14.8% |   0.6% |   0.0% |    +1.8 (+0.3 to +3.3) | +0.1 (-0.3 to +0.4) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    31 |  19.4% |   1.4% |   0.0% |    +6.4 (+4.8 to +8.0) | +0.9 (+0.4 to +1.3) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    31 |  26.8% |   5.4% |   0.0% | +13.8 (+12.0 to +15.5) | +4.9 (+4.1 to +5.6) | +0.0 (-0.1 to +0.1) |

*90% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    16 |   1.8% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    16 |   2.0% |   0.0% |   0.0% | +0.2 (-0.4 to +0.8) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    16 |   2.4% |   0.0% |   0.0% | +0.6 (-0.0 to +1.2) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    16 |   5.4% |   0.0% |   0.0% | +3.6 (+2.7 to +4.4) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |

*95% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                     8 |   0.1% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                     8 |   0.1% |   0.0% |   0.0% | -0.0 (-0.2 to +0.2) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                     8 |   0.4% |   0.0% |   0.0% | +0.2 (-0.0 to +0.5) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                     8 |   0.5% |   0.0% |   0.0% | +0.4 (+0.1 to +0.7) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |

### Middle

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |      Difference P(≥50) |
|:---------------------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|-----------------------:|
| No quarantine        |                   236 |  92.5% |  92.3% |  90.4% |              Reference |              Reference |              Reference |
| Only high-risk (21d) |                   236 |  67.8% |  49.9% |   6.1% | -24.6 (-26.3 to -22.9) | -42.3 (-44.1 to -40.6) | -84.4 (-85.5 to -83.1) |
| Only med-risk (21d)  |                   236 |  92.8% |  92.8% |  90.6% |    +0.4 (-0.8 to +1.5) |    +0.5 (-0.6 to +1.7) |    +0.2 (-1.1 to +1.5) |
| Only low-risk (21d)  |                   236 |  92.0% |  91.5% |  86.0% |    -0.4 (-1.6 to +0.7) |    -0.7 (-1.9 to +0.5) |    -4.4 (-5.9 to -3.0) |

**Tiered strategies (high/medium/low days)**, compared with 21/21/21 at
the same coverage

*50% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                   118 |  35.3% |   9.3% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                   118 |  35.6% |  10.4% |   0.0% | +0.4 (-1.7 to +2.5) | +1.1 (-0.2 to +2.5) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                   118 |  37.0% |  10.9% |   0.0% | +1.8 (-0.3 to +3.9) | +1.6 (+0.3 to +2.9) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                   118 |  38.4% |  12.4% |   0.0% | +3.1 (+1.0 to +5.2) | +3.1 (+1.7 to +4.5) | +0.0 (-0.1 to +0.1) |

*60% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    94 |  25.4% |   4.2% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    94 |  26.4% |   4.0% |   0.0% | +0.9 (-1.0 to +2.8) | -0.3 (-1.1 to +0.6) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    94 |  26.0% |   4.5% |   0.0% | +0.6 (-1.3 to +2.5) | +0.2 (-0.7 to +1.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    94 |  27.3% |   4.6% |   0.0% | +1.8 (-0.1 to +3.7) | +0.4 (-0.5 to +1.3) | +0.0 (-0.1 to +0.1) |

*70% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    71 |  13.5% |   0.6% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    71 |  15.2% |   0.6% |   0.0% | +1.7 (+0.1 to +3.2) | +0.0 (-0.4 to +0.4) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    71 |  15.3% |   0.8% |   0.0% | +1.8 (+0.3 to +3.4) | +0.2 (-0.2 to +0.6) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    71 |  16.2% |   1.2% |   0.0% | +2.6 (+1.1 to +4.2) | +0.6 (+0.2 to +1.1) | +0.0 (-0.1 to +0.1) |

*80% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    47 |   4.9% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    47 |   5.2% |   0.1% |   0.0% | +0.3 (-0.6 to +1.3) | +0.0 (-0.1 to +0.2) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    47 |   5.0% |   0.1% |   0.0% | +0.2 (-0.8 to +1.1) | +0.0 (-0.1 to +0.2) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    47 |   6.1% |   0.0% |   0.0% | +1.2 (+0.2 to +2.2) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |

*90% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    24 |   0.5% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    24 |   0.2% |   0.0% |   0.0% | -0.3 (-0.6 to -0.0) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    24 |   0.5% |   0.0% |   0.0% | -0.0 (-0.4 to +0.3) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    24 |   0.4% |   0.0% |   0.0% | -0.2 (-0.5 to +0.1) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |

*95% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    12 |   0.0% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    12 |   0.1% |   0.0% |   0.0% | +0.0 (-0.1 to +0.2) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    12 |   0.0% |   0.0% |   0.0% | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    12 |   0.0% |   0.0% |   0.0% | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |

### High

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |      Difference P(≥50) |
|:---------------------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|-----------------------:|
| No quarantine        |                   232 |  98.1% |  98.1% |  97.9% |           Reference |           Reference |              Reference |
| Only high-risk (21d) |                   232 |  94.1% |  92.8% |  80.7% | -4.0 (-4.9 to -3.2) | -5.3 (-6.2 to -4.4) | -17.1 (-18.5 to -15.9) |
| Only med-risk (21d)  |                   232 |  94.3% |  94.3% |  93.8% | -3.7 (-4.6 to -2.9) | -3.8 (-4.7 to -3.0) |    -4.0 (-4.9 to -3.2) |
| Only low-risk (21d)  |                   232 |  96.0% |  92.8% |  67.9% | -2.1 (-2.9 to -1.4) | -5.2 (-6.2 to -4.4) | -29.9 (-31.5 to -28.4) |

**Tiered strategies (high/medium/low days)**, compared with 21/21/21 at
the same coverage

*50% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |      Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|-----------------------:|
| 21/21/21 |                   116 |  61.6% |  43.8% |   6.2% |              Reference |              Reference |              Reference |
| 21/14/14 |                   116 |  64.4% |  45.0% |   4.0% |    +2.8 (+0.7 to +4.9) |    +1.2 (-1.0 to +3.4) |    -2.1 (-3.1 to -1.1) |
| 21/7/7   |                   116 |  70.9% |  55.6% |   8.8% |   +9.4 (+7.3 to +11.4) |  +11.8 (+9.6 to +14.0) |    +2.6 (+1.5 to +3.8) |
| 21/0/0   |                   116 |  80.7% |  73.7% |  22.6% | +19.1 (+17.2 to +21.1) | +29.9 (+27.8 to +31.9) | +16.4 (+14.9 to +17.9) |

*60% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    93 |  51.8% |  31.2% |   0.9% |              Reference |              Reference |           Reference |
| 21/14/14 |                    93 |  55.7% |  33.2% |   1.0% |    +3.9 (+1.7 to +6.1) |    +2.0 (-0.1 to +4.0) | +0.0 (-0.4 to +0.5) |
| 21/7/7   |                    93 |  62.9% |  44.8% |   2.5% |  +11.1 (+9.0 to +13.3) | +13.6 (+11.5 to +15.7) | +1.5 (+1.0 to +2.1) |
| 21/0/0   |                    93 |  72.1% |  60.9% |   6.3% | +20.3 (+18.2 to +22.4) | +29.7 (+27.5 to +31.7) | +5.3 (+4.5 to +6.2) |

*70% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    70 |  40.1% |  17.2% |   0.1% |              Reference |              Reference |           Reference |
| 21/14/14 |                    70 |  42.8% |  18.1% |   0.0% |    +2.6 (+0.5 to +4.8) |    +0.9 (-0.8 to +2.5) | -0.1 (-0.3 to -0.0) |
| 21/7/7   |                    70 |  50.8% |  27.6% |   0.0% |  +10.7 (+8.5 to +12.8) |  +10.4 (+8.6 to +12.2) | -0.1 (-0.3 to +0.0) |
| 21/0/0   |                    70 |  61.4% |  42.3% |   0.3% | +21.2 (+19.1 to +23.4) | +25.1 (+23.2 to +27.0) | +0.1 (-0.1 to +0.4) |

*80% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |      Difference P(≥10) |      Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|-----------------------:|-----------------------:|--------------------:|
| 21/21/21 |                    46 |  23.2% |   4.6% |   0.0% |              Reference |              Reference |           Reference |
| 21/14/14 |                    46 |  26.6% |   5.2% |   0.0% |    +3.3 (+1.4 to +5.2) |    +0.6 (-0.3 to +1.5) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    46 |  32.3% |   8.7% |   0.0% |   +9.0 (+7.1 to +11.0) |    +4.1 (+3.0 to +5.2) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    46 |  42.2% |  17.3% |   0.0% | +19.0 (+17.0 to +21.0) | +12.8 (+11.4 to +14.1) | +0.0 (-0.1 to +0.1) |

*90% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    23 |   6.4% |   0.1% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    23 |   7.1% |   0.2% |   0.0% | +0.7 (-0.4 to +1.8) | +0.1 (-0.1 to +0.3) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    23 |  10.7% |   0.2% |   0.0% | +4.2 (+3.0 to +5.5) | +0.1 (-0.1 to +0.3) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    23 |  14.1% |   0.9% |   0.0% | +7.7 (+6.4 to +9.0) | +0.8 (+0.5 to +1.1) | +0.0 (-0.1 to +0.1) |

*95% vaccinated*

| Strategy | Unvaccinated students | P(≥10) | P(≥20) | P(≥50) |   Difference P(≥10) |   Difference P(≥20) |   Difference P(≥50) |
|:---------|----------------------:|-------:|-------:|-------:|--------------------:|--------------------:|--------------------:|
| 21/21/21 |                    12 |   1.2% |   0.0% |   0.0% |           Reference |           Reference |           Reference |
| 21/14/14 |                    12 |   1.2% |   0.0% |   0.0% | -0.1 (-0.5 to +0.4) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/7/7   |                    12 |   1.4% |   0.0% |   0.0% | +0.1 (-0.4 to +0.6) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
| 21/0/0   |                    12 |   2.9% |   0.0% |   0.0% | +1.7 (+1.1 to +2.4) | +0.0 (-0.1 to +0.1) | +0.0 (-0.1 to +0.1) |
