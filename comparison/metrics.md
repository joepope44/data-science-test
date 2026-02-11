# Comparison Metrics

## Minimal Guidance
- **Total prompts from user:** 1 (single instruction to implement the plan)
- **Iterations/corrections needed:** 0 (executed cleanly on first run)
- **Code quality (1-10):** 4
- **Analysis depth (1-10):** 4
- **Business value (1-10):** 5

## Structured Approach
- **Total prompts from user:** 7 (system prompt read + 6 phase approvals)
- **Iterations/corrections needed:** 1 (missing sklearn import fixed in Phase 2)
- **Code quality (1-10):** 8
- **Analysis depth (1-10):** 9
- **Business value (1-10):** 9

## Side-by-Side Comparison

| Dimension | Minimal Guidance | Structured Approach | Winner |
|-----------|-----------------|---------------------|--------|
| **Notebook size** | 24 cells (18 code, 6 markdown) | 101 cells (51 code, 50 markdown) | Structured (4.2x larger) |
| **Functions defined** | 0 (inline scripts) | 25 modular functions | Structured |
| **Docstrings** | None | 27 (all functions documented) | Structured |
| **Type hints** | None | 23 instances | Structured |
| **Clustering methods** | 1 (K-Means only) | 3 (K-Means, Hierarchical, GMM) | Structured |
| **Validation metrics** | 0 (inertia only, no silhouette/DB) | 4 (Silhouette, Davies-Bouldin, ARI, NMI) | Structured |
| **Elbow method** | Yes | Yes (with silhouette overlay) | Structured |
| **Dendrogram** | No | Yes | Structured |
| **BIC/AIC analysis** | No | Yes | Structured |
| **Bootstrap stability** | No | Yes (10 runs) | Structured |
| **Cross-method agreement** | N/A | Yes (ARI, NMI) | Structured |
| **Segment naming** | None (numeric IDs + risk labels) | Algorithmic (data-driven names) | Structured |
| **Feature engineering** | Label encoding only | 4 derived features + label encoding | Structured |
| **Outlier analysis** | No | Yes (IQR method, all features) | Structured |
| **Data quality checks** | Basic (missing values, class dist.) | Comprehensive (missing, dupes, IDs, constants, unknowns) | Structured |
| **Output files** | 8 (7 PNG + 1 CSV) | 19 (15 PNG + 2 CSV + 1 MD) | Structured (2.4x more) |
| **Executive summary** | Inline markdown only | Standalone markdown file | Structured |
| **Impact estimation** | No | Yes (quantified: customers + revenue saved) | Structured |
| **Validation checklist** | No | Yes (8/8 criteria passed) | Structured |
| **Radar chart** | No | Yes | Structured |
| **Z-score heatmap** | No | Yes | Structured |
| **Demographic breakdown** | No | Yes (5 demographics × segment) | Structured |
| **Risk dashboard** | No | Yes (3-panel: rate, exposure, revenue) | Structured |
| **User effort** | 1 prompt | 7 prompts | Minimal (lower effort) |

## Segment Quality Comparison

### Minimal Guidance (K-Means, k=4)
| Cluster | Size | Attrition | Key Trait |
|---------|------|-----------|-----------|
| 0 | 4,024 (39.7%) | 8.1% | High utilization (0.56), most loyal |
| 1 | 3,810 (37.6%) | 27.6% | Low utilization (0.08), highest churn |
| 2 | 1,336 (13.2%) | 15.4% | Premium ($27.5K credit), underutilized |
| 3 | 957 (9.4%) | 4.6% | Power users ($12.6K trans amt) |

### Structured Approach (K-Means, k=4)
| Cluster | Name | Size | Attrition | Key Trait |
|---------|------|------|-----------|-----------|
| 0 | High-Value Dormant Loyal | 2,713 (26.8%) | 6.5% | High credit ($12.8K), very loyal |
| 1 | High-Value Active | 1,282 (12.7%) | 12.2% | Highest credit ($15.6K), power users |
| 2 | Low-Limit Revolvers Loyal | 3,327 (32.9%) | 8.5% | High utilization (0.56), loyal |
| 3 | Transactors At-Risk | 2,805 (27.7%) | 36.1% | Near-zero utilization, highest churn |

**Note:** Different segment compositions result from the structured approach's 4 additional engineered features and removal of redundant Avg_Open_To_Buy. The structured approach produced more balanced cluster sizes (CV = 0.35 vs 0.58) and wider attrition rate spread (6.5%–36.1% vs 4.6%–27.6%), indicating better churn discrimination.

## Scoring Rationale

### Code Quality
- **Minimal (4/10):** No functions, no docstrings, no type hints, no error handling. Works but not maintainable or reusable.
- **Structured (8/10):** 25 modular functions with docstrings, type hints, validation checks. Production-ready code.

### Analysis Depth
- **Minimal (4/10):** Single clustering method, no validation metrics beyond inertia, no outlier analysis, no feature engineering.
- **Structured (9/10):** 3 methods compared, 4 validation metrics, bootstrap stability, cross-method agreement, outlier detection, 4 engineered features, pairwise segment distinctiveness testing.

### Business Value
- **Minimal (5/10):** Identifies segments and provides general recommendations by risk tier, but no quantified impact, no segment names, no risk dashboard.
- **Structured (9/10):** Named segments, quantified revenue impact ($662K saveable), per-segment strategies with KPIs, executive summary, risk dashboard, demographic breakdowns.
