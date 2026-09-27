# Beyond the Boundary: What Actually Drives a Billion-Dollar IPL Valuation?

A statistical analysis of what drives the brand value of Indian Premier League (IPL) franchises, built entirely on live Excel formulas.

**Course:** BM5104H Business Statistics and Data Analysis for Management
**Assignment:** Data Tank Group Assignment, Team Shark 9

---

## The Business Question

> Say a company wants to invest in or sponsor an IPL franchise. Which driver of franchise valuation gives the most value for the money spent?

We tested three competing explanations:

| Hypothesis | Proxy variables |
| --- | --- |
| **On-field performance** (the intuitive answer) | Titles, all-time win %, playoff appearances |
| **Geographic market size** (the economist's answer) | Home-city GDP, population |
| **Off-field digital engagement** (the modern answer) | Instagram + X followers |

- **Dependent variable (Y):** 2025 franchise brand value (US$M)
- **Control:** auction spend

## Key Findings

1. **Money does not buy wins.** Auction spend vs. win %: r = 0.35, p = 0.32 (not significant). P(playoffs | top-50% spend) = 0.50. The salary cap has removed spending as a lever.
2. **Winning matches doesn't build brand value, but winning trophies does.** Win % correlates *negatively* with brand value (r = −0.17). Titles correlate at r = 0.81, each one is worth about **+$22.4M** (p = 0.0048), and the link holds after controlling for city GDP (partial r = 0.765).
3. **Digital engagement is the biggest driver.** Social followers correlate at r = 0.91. They are the only significant predictor in the multiple regression (p = 0.0017), add ΔR² = 0.118 after performance and market size are already in the model, and have the largest standardised β (0.661).
4. **Older franchises carry a real premium.** Legacy franchises average $195.75M against $132.00M for expansion teams (Welch t-test, p = 0.018).
5. **The league is competitively balanced.** Net run rate across 128 team-seasons is normally distributed (Shapiro-Wilk W = 0.99, p = 0.515), so no franchise dominates for long.

**Recommendation:** the next marginal dollar should go to **off-field digital content and fan engagement**. RCB is the clearest example: it is the most valuable brand in the league ($269M → $312M) yet a statistically average team (48.25% win rate, p = 0.60 vs. 50%) with only 2 titles. What it does have is the league's largest social following (31.8M).

## Methodology

| Step | Technique | Excel implementation |
| --- | --- | --- |
| Descriptive statistics | Mean, median, SD, variance, skew | `AVERAGE`, `MEDIAN`, `STDEV.S`, `VAR.S` |
| Association | Pearson & Spearman correlation | `CORREL`, `RANK.AVG`, `T.DIST.2T` |
| Robustness | Partial correlation (controlling for GDP) | Built from three `CORREL` calls |
| Probability | Conditional probability | `COUNTIFS` |
| Normality | Shapiro-Wilk on net run rate | Python `scipy.stats.shapiro`; histogram via `FREQUENCY` |
| Estimation | 95% confidence interval for mean brand value | `CONFIDENCE.T` |
| Hypothesis tests | Welch two-sample t-test, one-proportion z-test, one-way ANOVA | `T.TEST`, `NORM.S.DIST`, `SUMPRODUCT`, `F.DIST.RT` |
| Modelling | Simple, multiple & hierarchical regression, standardised betas | `LINEST` array formulas |

Every statistic is a **live formula** that references a single source-of-truth data sheet: 8 sheets and 411 formulas in total.

## Repository Contents

```
├── Beyond-the-Boundary-IPL-Valuation.pptx   # Final presentation (20 slides)
├── IPL_DATA_TANK_Workbook.xlsx              # Live Excel workbook: data + all analysis
├── IPL_DATA_TANK_Workbook.pdf               # PDF export of the workbook
└── README.md
```

## Data Sources

| Domain | Source | Coverage |
| --- | --- | --- |
| Brand valuation | Houlihan Lokey IPL Brand Valuation Studies | 2024–2026 |
| On-field performance | IPL official season points tables (iplt20.com) | 2008–2023, 136 team-seasons |
| Titles & playoffs | IPL official results | Through 2026 |
| Market size | Census of India 2011; metro GDP estimates | 2011 / 2022–23 |
| Digital engagement | Franchise Instagram + X follower counts | 2025–26 snapshot |
| Auction spend | IPL auction purse utilisation reports | 2022–2026 |

## Limitations

- **Small sample (n = 10).** All results are directional rather than high-powered inference. With 5 predictors and only 10 observations, the Block 3 coefficients are individually insignificant even though the overall fit is strong (R² = 0.866).
- The expansion-vs-legacy t-test rests on only **2 expansion franchises**.
- The analysis is cross-sectional and correlational, so it **does not establish causation**.
- Follower counts measure reach, not engagement quality.

## Future Scope

- Extend to a 2020–2026 panel for fixed-effects estimation and causal inference.
- Add engagement-quality metrics (impressions, watch time, engagement rate) beyond raw follower counts.

## Team Shark 9

| Name | Roll Number |
| --- | --- |
| Pranav C Satheesh | 264024021 |
| Kunwar Atul Ang | 252241017 |
| Parth Arvind Deshmukh | 264024020 |

---

*This is an academic project. Valuation figures come from third-party estimates (Houlihan Lokey) and should not be read as investment advice.*
