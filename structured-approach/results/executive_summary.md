# Customer Segmentation — Executive Summary

## Overview
Segmented 10,127 credit card customers into 4 distinct groups using K-Means
clustering on 22 behavioral and demographic features. Three clustering methods
were evaluated (K-Means, Hierarchical, Gaussian Mixture); K-Means was selected
based on superior cluster separation, stability, and cross-method validation.

## Segments at a Glance

| Segment | Size | Attrition | Description |
|---------|------|-----------|-------------|
| High-Value Dormant Loyal | 2,713 (26.8%) | 6.5% | High credit limit, moderate activity, very loyal |
| High-Value Active | 1,282 (12.7%) | 12.2% | Power users with high credit and heavy transaction activity |
| Low-Limit Revolvers Loyal | 3,327 (32.9%) | 8.5% | Lower credit, high utilization, steady revolvers |
| Transactors At-Risk | 2,805 (27.7%) | 36.1% | Near-zero revolving usage, declining engagement, highest churn |

## Key Findings
1. **Transaction behavior drives churn:** Customers who stop revolving and reduce
   transaction frequency are 5-6x more likely to churn than engaged customers.
2. **Demographics are secondary:** Gender, education, and marital status show
   relatively uniform attrition rates — behavioral signals matter more.
3. **One segment accounts for 1,012 of 1,627 total churns**
   (62%),
   making it the highest-priority retention target.

## Recommended Actions (Priority Order)
1. **Immediate:** Launch retention campaign for "Transactors At-Risk"
   segment — proactive outreach, balance transfer offers, transaction incentives
2. **Short-term:** Deploy engagement programs for dormant high-value customers
   to increase card usage before disengagement deepens
3. **Ongoing:** Upsell premium products to loyal high-value customers;
   offer credit limit increases to high-utilization revolvers
4. **Monitor:** Track monthly attrition rate by segment; set up early-warning
   triggers based on inactivity and declining transaction patterns

## Estimated Impact
A 20% reduction in churn for the critical segment alone would save
~203 customers and ~$662,521 in annual transaction revenue.

## Methodology
- **Data:** 10,127 customers, 22 features (18 original + 4 engineered)
- **Methods compared:** K-Means, Hierarchical (Ward), Gaussian Mixture
- **Selected:** K-Means (k=4) — highest silhouette, stable under bootstrap, strong cross-method agreement
- **Validation:** Silhouette score, Davies-Bouldin index, bootstrap stability, pairwise distinctiveness
