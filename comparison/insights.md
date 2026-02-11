# Insights — What Worked Better and Why

## TL;DR
The structured approach produced dramatically better results across every quality dimension (code, analysis, business value) at the cost of ~7x more user prompts. The minimal-guidance approach delivered a working but shallow analysis in a single shot.

## 1. Structure Drives Rigor

The most significant difference was **methodological rigor**. The structured prompt explicitly required "at least 3 clustering methods" with "appropriate metrics (silhouette score, Davies-Bouldin, etc.)" — so it got them. The minimal-guidance approach, left to its own judgment, took the path of least resistance: a single K-Means model with no validation metrics beyond inertia.

**Lesson:** Claude will do what you ask, but defaults to the simplest viable approach when not given explicit requirements. If methodological thoroughness matters, specify it upfront.

## 2. Phased Review Catches Errors Early

The structured approach had one bug (missing `LabelEncoder` import) caught and fixed in Phase 2 before it could compound. The minimal-guidance approach happened to execute cleanly on the first run, but if it hadn't, the single-shot nature would have required re-running the entire notebook rather than fixing incrementally.

**Lesson:** Phased delivery with review checkpoints creates natural breakpoints for error detection and course correction.

## 3. Code Quality Standards Must Be Explicit

The structured system prompt specified: "Modular code with clear functions, comprehensive error handling, inline documentation and docstrings, type hints where applicable." The result was 25 documented functions with type annotations.

The minimal-guidance approach produced zero functions — all inline scripts. The code works but is not reusable, testable, or maintainable.

**Lesson:** Code quality standards are not inferred — they must be stated. Claude will write clean code when asked, but optimizes for speed and simplicity when not.

## 4. Feature Engineering Requires Prompting

The structured approach created 4 derived features (Avg_Trans_Value, Activity_Ratio, Utilization_Credit_Interaction, Contacts_per_Relationship) that measurably improved cluster discrimination. The minimal approach performed no feature engineering beyond label encoding.

This is notable because the structured prompt mentioned "Create derived features if beneficial (RFM scores, etc.)" as a specific requirement, while the minimal plan only mentioned encoding and scaling.

**Lesson:** Feature engineering is a creative step that benefits from explicit encouragement. Without it, Claude tends to use raw features as-is.

## 5. Business Value Scales with Specificity

The structured approach produced:
- Named segments with business-meaningful labels
- Quantified revenue impact ($662K saveable)
- Per-segment strategies with specific KPIs
- A standalone executive summary suitable for stakeholder distribution
- A risk dashboard visualization

The minimal approach produced:
- Generic risk tiers (High/Moderate/Low)
- General strategy categories
- No quantified impact

**Lesson:** Requesting "estimate potential business impact" and "name each segment meaningfully" in the prompt directly translates to those deliverables appearing in the output.

## 6. The Effort-Quality Tradeoff

| Approach | User Prompts | Code Quality | Analysis Depth | Business Value |
|----------|-------------|-------------|----------------|----------------|
| Minimal | 1 | 4/10 | 4/10 | 5/10 |
| Structured | 7 | 8/10 | 9/10 | 9/10 |
| **Improvement** | **7x effort** | **+100%** | **+125%** | **+80%** |

The structured approach required 7x more user interaction but delivered roughly 2x improvement across all quality dimensions. Whether this tradeoff is worthwhile depends on the use case:
- **Exploratory/internal analysis:** Minimal guidance may suffice
- **Production/stakeholder-facing work:** Structured approach is clearly superior
- **Learning/experimentation:** Minimal guidance for speed, then iterate

## 7. What Minimal Guidance Got Right

Despite its limitations, the minimal approach:
- Correctly identified the same overall pattern (low-utilization customers churn most)
- Produced all core visualizations (correlation matrix, distributions, elbow plot, PCA)
- Dropped the leakage columns without being told
- Completed the entire analysis in a single interaction
- Generated a conversation log as requested

This suggests that Claude's baseline data science capability is solid — the structured approach improves depth and polish, not fundamental correctness.

## 8. What the Structured Approach Could Improve

- **Silhouette scores were low across all methods** (0.03–0.19), suggesting the 22-dimensional feature space has inherent overlap. Dimensionality reduction before clustering (e.g., PCA to 10 components) was not explored.
- **k=4 was selected over k=2** for business reasons despite k=2 having better metrics. This tradeoff was well-justified but could have been flagged more prominently.
- **GMM with full covariance on 22 features** is parameter-heavy (22×22 covariance matrices per component). A diagonal or tied covariance might have been more appropriate.

## 9. Recommendations for Future Projects

1. **Start with a structured system prompt** that specifies code quality standards, required methods, and deliverable formats — even if you plan to iterate quickly
2. **Use phased delivery** for non-trivial analyses — it doesn't add much user effort but significantly improves error catching and output quality
3. **Explicitly request feature engineering** — it's the step most likely to be skipped under minimal guidance
4. **Require validation metrics by name** (silhouette, Davies-Bouldin) — Claude knows how to compute them but won't volunteer them unprompted
5. **Ask for quantified business impact** — the difference between "target high-risk customers" and "save $662K by reducing churn 20% in segment X" is entirely driven by the prompt
