# 1. Tiered quarantine: outbreak probability tables

- [Transmission rate check](#transmission-rate-check)
- [Results by school](#results-by-school)

Tiered-quarantine experiment using the three real per-capita SMART
contact matrices (symmetrised for reciprocity, kept at real magnitude).
R0 = 12 is reached through a per-school transmission rate, not by
scaling the matrix.

For each school we report **P(outbreak ≥ 10 / 20 / 50 cases)** across
vaccination coverage and quarantine strategies, written as **high /
medium / low-risk contact quarantine days**.

The diagnostic single-tier scenarios in the first table do not satisfy
high ≥ medium ≥ low; that constraint is applied to every other analysis.

**Significance.** Each scenario’s full outbreak-size distribution is
compared with a reference scenario using a two-sided Wilcoxon rank-sum
test: *No quarantine* for the no-vaccination table, and *21/21/21* at
the same coverage for the tiered table. Stars: \* p \< 0.05, \*\* p \<
0.01, \*\*\* p \< 0.001. P-values are not adjusted for multiple
comparisons.

<div>

> **Note**
>
> Model code lives in `measles_model.R`. Simulations are cached in
> `results/`; delete the CSV to re-run. For a quick test render with
> `N_SIMS=200 quarto render 01_tiered_quarantine_tables.qmd`.

</div>

## Contact matrices

The model uses real per-capita contact matrices from the SMART
(Pittsburgh) school contact study, one per school type. Each row is the
grade of a student, and each column is the grade of the students they
have contact with. The values below are the raw matrices. Before running
the model, each matrix is symmetrised, `0.5 * (C + t(C))`, so that
contacts are reciprocal. Their magnitude is kept as is; R0 = 12 is set
through a per-school transmission rate instead.

### Elementary school (grades K–5, 26 students per grade)

| Grade | K | 1 | 2 | 3 | 4 | 5 |
|:--|--:|--:|--:|--:|--:|--:|
| **K** | 18.74 | 1.32 | 0.25 | 0.09 | 3.77 | 0.14 |
| **1** | 1.14 | 24.52 | 3.06 | 0.02 | 0.17 | 0.00 |
| **2** | 0.29 | 4.21 | 13.96 | 6.60 | 1.60 | 0.00 |
| **3** | 0.08 | 0.02 | 5.03 | 17.49 | 9.57 | 0.02 |
| **4** | 3.21 | 0.16 | 1.15 | 9.00 | 25.37 | 0.79 |
| **5** | 0.21 | 0.00 | 0.00 | 0.03 | 1.39 | 32.42 |

### Middle school (grades 5–8, 59 students per grade)

| Grade | 5 | 6 | 7 | 8 |
|:--|--:|--:|--:|--:|
| **5** | 35.15 | 0.67 | 0.00 | 0.00 |
| **6** | 0.61 | 27.91 | 0.00 | 0.00 |
| **7** | 0.00 | 0.00 | 65.94 | 0.11 |
| **8** | 0.00 | 0.00 | 0.17 | 31.32 |

### High school (grades 9–12, 58 students per grade)

| Grade | 9 | 10 | 11 | 12 |
|:--|--:|--:|--:|--:|
| **9** | 25.98 | 14.45 | 3.94 | 1.38 |
| **10** | 12.12 | 20.71 | 6.04 | 2.42 |
| **11** | 4.56 | 8.33 | 14.26 | 6.31 |
| **12** | 1.89 | 3.97 | 7.48 | 14.97 |

Most contacts happen within the same grade (the diagonal). Middle-school
grades mix very little with each other, while high-school grades mix the
most across grades.

## Transmission rate check

Each school gets its own transmission rate so that R0 = 12. The table
checks this against `epiworldR::compute_reproduction_number()`.

| School     | Students | Transmission rate |  R0 |
|:-----------|---------:|------------------:|----:|
| Elementary |      156 |            0.0886 |  12 |
| Middle     |      236 |            0.0455 |  12 |
| High       |      232 |            0.0741 |  12 |

## Results by school

### Elementary

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------------------|-------:|-------:|-------:|----------------:|:------------:|
| No quarantine        |  0.979 |  0.979 |  0.977 |       Reference |  Reference   |
| Only high-risk (21d) |  0.894 |  0.856 |  0.739 |         \<0.001 |    \*\*\*    |
| Only med-risk (21d)  |  0.961 |  0.961 |  0.941 |         \<0.001 |    \*\*\*    |
| Only low-risk (21d)  |  0.966 |  0.931 |  0.566 |         \<0.001 |    \*\*\*    |

**Tiered strategies (H/M/L days) by vaccination coverage** (compared
with 21/21/21)

| Coverage | Strategy | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------|:---------|-------:|-------:|-------:|----------------:|:------------:|
| 50%      | 21/21/21 |  0.548 |  0.334 |  0.212 |       Reference |  Reference   |
| 50%      | 21/14/14 |  0.572 |  0.342 |  0.184 |           0.905 |              |
| 50%      | 21/7/7   |  0.634 |  0.448 |  0.203 |         \<0.001 |    \*\*\*    |
| 50%      | 21/0/0   |  0.698 |  0.587 |  0.238 |         \<0.001 |    \*\*\*    |
| 60%      | 21/21/21 |  0.430 |  0.244 |  0.172 |       Reference |  Reference   |
| 60%      | 21/14/14 |  0.464 |  0.250 |  0.146 |           0.356 |              |
| 60%      | 21/7/7   |  0.524 |  0.320 |  0.144 |         \<0.001 |    \*\*\*    |
| 60%      | 21/0/0   |  0.605 |  0.454 |  0.086 |         \<0.001 |    \*\*\*    |
| 70%      | 21/21/21 |  0.321 |  0.136 |  0.031 |       Reference |  Reference   |
| 70%      | 21/14/14 |  0.330 |  0.142 |  0.021 |           0.442 |              |
| 70%      | 21/7/7   |  0.386 |  0.192 |  0.026 |         \<0.001 |    \*\*\*    |
| 70%      | 21/0/0   |  0.475 |  0.296 |  0.013 |         \<0.001 |    \*\*\*    |
| 80%      | 21/21/21 |  0.161 |  0.072 |  0.000 |       Reference |  Reference   |
| 80%      | 21/14/14 |  0.186 |  0.069 |  0.000 |           0.397 |              |
| 80%      | 21/7/7   |  0.226 |  0.059 |  0.000 |           0.010 |      \*      |
| 80%      | 21/0/0   |  0.302 |  0.090 |  0.000 |         \<0.001 |    \*\*\*    |
| 90%      | 21/21/21 |  0.038 |  0.006 |  0.000 |       Reference |  Reference   |
| 90%      | 21/14/14 |  0.034 |  0.002 |  0.000 |           0.678 |              |
| 90%      | 21/7/7   |  0.041 |  0.002 |  0.000 |           0.135 |              |
| 90%      | 21/0/0   |  0.059 |  0.004 |  0.000 |           0.014 |      \*      |
| 95%      | 21/21/21 |  0.014 |  0.000 |  0.000 |       Reference |  Reference   |
| 95%      | 21/14/14 |  0.011 |  0.000 |  0.000 |           0.983 |              |
| 95%      | 21/7/7   |  0.009 |  0.000 |  0.000 |           0.853 |              |
| 95%      | 21/0/0   |  0.005 |  0.000 |  0.000 |           0.557 |              |

### Middle

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------------------|-------:|-------:|-------:|----------------:|:------------:|
| No quarantine        |  0.925 |  0.924 |  0.912 |       Reference |  Reference   |
| Only high-risk (21d) |  0.673 |  0.540 |  0.314 |         \<0.001 |    \*\*\*    |
| Only med-risk (21d)  |  0.927 |  0.926 |  0.913 |         \<0.001 |    \*\*\*    |
| Only low-risk (21d)  |  0.930 |  0.928 |  0.910 |           0.006 |     \*\*     |

**Tiered strategies (H/M/L days) by vaccination coverage** (compared
with 21/21/21)

| Coverage | Strategy | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------|:---------|-------:|-------:|-------:|----------------:|:------------:|
| 50%      | 21/21/21 |  0.370 |  0.187 |  0.132 |       Reference |  Reference   |
| 50%      | 21/14/14 |  0.378 |  0.203 |  0.117 |           0.868 |              |
| 50%      | 21/7/7   |  0.377 |  0.186 |  0.082 |           0.953 |              |
| 50%      | 21/0/0   |  0.386 |  0.196 |  0.030 |           0.909 |              |
| 60%      | 21/21/21 |  0.282 |  0.124 |  0.100 |       Reference |  Reference   |
| 60%      | 21/14/14 |  0.288 |  0.146 |  0.092 |           0.769 |              |
| 60%      | 21/7/7   |  0.290 |  0.136 |  0.050 |           0.985 |              |
| 60%      | 21/0/0   |  0.288 |  0.129 |  0.016 |           0.911 |              |
| 70%      | 21/21/21 |  0.163 |  0.066 |  0.062 |       Reference |  Reference   |
| 70%      | 21/14/14 |  0.163 |  0.062 |  0.050 |           0.986 |              |
| 70%      | 21/7/7   |  0.168 |  0.060 |  0.035 |           0.986 |              |
| 70%      | 21/0/0   |  0.164 |  0.036 |  0.005 |           0.877 |              |
| 80%      | 21/21/21 |  0.080 |  0.043 |  0.018 |       Reference |  Reference   |
| 80%      | 21/14/14 |  0.082 |  0.029 |  0.011 |           0.984 |              |
| 80%      | 21/7/7   |  0.078 |  0.016 |  0.004 |           0.946 |              |
| 80%      | 21/0/0   |  0.078 |  0.008 |  0.001 |           0.987 |              |
| 90%      | 21/21/21 |  0.020 |  0.018 |  0.000 |       Reference |  Reference   |
| 90%      | 21/14/14 |  0.016 |  0.011 |  0.000 |           0.960 |              |
| 90%      | 21/7/7   |  0.015 |  0.008 |  0.000 |           0.956 |              |
| 90%      | 21/0/0   |  0.010 |  0.000 |  0.000 |           0.940 |              |
| 95%      | 21/21/21 |  0.010 |  0.000 |  0.000 |       Reference |  Reference   |
| 95%      | 21/14/14 |  0.007 |  0.000 |  0.000 |           0.970 |              |
| 95%      | 21/7/7   |  0.002 |  0.000 |  0.000 |           0.971 |              |
| 95%      | 21/0/0   |  0.000 |  0.000 |  0.000 |           0.971 |              |

### High

**No vaccination: which single tier to quarantine** (compared with no
quarantine)

| Scenario             | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------------------|-------:|-------:|-------:|----------------:|:------------:|
| No quarantine        |  0.974 |  0.974 |  0.974 |       Reference |  Reference   |
| Only high-risk (21d) |  0.934 |  0.926 |  0.864 |         \<0.001 |    \*\*\*    |
| Only med-risk (21d)  |  0.942 |  0.941 |  0.941 |         \<0.001 |    \*\*\*    |
| Only low-risk (21d)  |  0.960 |  0.929 |  0.811 |         \<0.001 |    \*\*\*    |

**Tiered strategies (H/M/L days) by vaccination coverage** (compared
with 21/21/21)

| Coverage | Strategy | P(≥10) | P(≥20) | P(≥50) | Overall p-value | Significance |
|:---------|:---------|-------:|-------:|-------:|----------------:|:------------:|
| 50%      | 21/21/21 |  0.588 |  0.454 |  0.284 |       Reference |  Reference   |
| 50%      | 21/14/14 |  0.629 |  0.490 |  0.294 |           0.380 |              |
| 50%      | 21/7/7   |  0.713 |  0.601 |  0.396 |         \<0.001 |    \*\*\*    |
| 50%      | 21/0/0   |  0.794 |  0.736 |  0.535 |         \<0.001 |    \*\*\*    |
| 60%      | 21/21/21 |  0.534 |  0.374 |  0.220 |       Reference |  Reference   |
| 60%      | 21/14/14 |  0.567 |  0.406 |  0.240 |           0.198 |              |
| 60%      | 21/7/7   |  0.640 |  0.498 |  0.281 |         \<0.001 |    \*\*\*    |
| 60%      | 21/0/0   |  0.725 |  0.628 |  0.367 |         \<0.001 |    \*\*\*    |
| 70%      | 21/21/21 |  0.402 |  0.245 |  0.158 |       Reference |  Reference   |
| 70%      | 21/14/14 |  0.434 |  0.286 |  0.154 |           0.126 |              |
| 70%      | 21/7/7   |  0.501 |  0.371 |  0.154 |         \<0.001 |    \*\*\*    |
| 70%      | 21/0/0   |  0.603 |  0.474 |  0.160 |         \<0.001 |    \*\*\*    |
| 80%      | 21/21/21 |  0.278 |  0.137 |  0.048 |       Reference |  Reference   |
| 80%      | 21/14/14 |  0.304 |  0.149 |  0.036 |           0.261 |              |
| 80%      | 21/7/7   |  0.366 |  0.184 |  0.035 |         \<0.001 |    \*\*\*    |
| 80%      | 21/0/0   |  0.454 |  0.272 |  0.028 |         \<0.001 |    \*\*\*    |
| 90%      | 21/21/21 |  0.083 |  0.040 |  0.000 |       Reference |  Reference   |
| 90%      | 21/14/14 |  0.095 |  0.040 |  0.000 |           0.549 |              |
| 90%      | 21/7/7   |  0.112 |  0.031 |  0.000 |           0.030 |      \*      |
| 90%      | 21/0/0   |  0.168 |  0.024 |  0.000 |         \<0.001 |    \*\*\*    |
| 95%      | 21/21/21 |  0.030 |  0.001 |  0.000 |       Reference |  Reference   |
| 95%      | 21/14/14 |  0.034 |  0.000 |  0.000 |           0.827 |              |
| 95%      | 21/7/7   |  0.028 |  0.000 |  0.000 |           0.467 |              |
| 95%      | 21/0/0   |  0.036 |  0.001 |  0.000 |           0.266 |              |
