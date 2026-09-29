# econ5200-lab03-eda-diagnostics
# Pipeline Health Check — EDA, Corruption & Distribution Shift

## Objective

This project evaluates data-pipeline reliability by identifying data-quality problems, measuring distribution shift, and building reusable monitoring tools for production-style economic datasets.

## Methodology

- Used exploratory data analysis to identify and correct **5 planted data-quality issues** in a country panel:
  - negative GDP values
  - life expectancy stored in months instead of years
  - duplicate country-year observations
  - inconsistent percentage units in `trade_pct`
  - GDP values stored in inconsistent units
- Verified the cleaned dataset with explicit data-quality checks.
- Split the cleaned data into training and inference samples and simulated a GDP distribution shift.
- Measured distribution drift using the **Population Stability Index (PSI)**.
- Compared manual EDA with automated profiling to identify which problems can be detected automatically and which require domain knowledge.
- Built `eda_utils.py` with reusable functions for impossible-value checks, PSI-based shift detection, and EDA summaries.
- Built an interactive pipeline-health dashboard with column-level distribution comparisons, PSI thresholds, editable min/max constraints, and dirty-versus-clean comparisons.

## Key Findings

The manual EDA process successfully identified and corrected all **5 planted data-quality issues**.

The GDP distribution showed a strong shift between the training and inference samples, with a **PSI of 1.7600**, well above the conventional 0.25 threshold for a significant shift.

The automated profiling comparison showed that tools can surface unusual ranges, outliers, and suspicious distributions, but they may miss problems that depend on dataset structure or domain knowledge. For example, the corrupted dataset contained duplicate country-year observations even though there were no exact duplicate rows.

The dashboard also demonstrated the value of explicit domain constraints. Editable minimum and maximum limits made it possible to compare acceptable ranges with the actual dirty-data ranges and immediately identify observations that violated economic plausibility rules.

Overall, the project shows that reliable data-pipeline monitoring requires a combination of automated checks, distribution-shift diagnostics, and domain-informed review rather than relying on a single profiling metric or threshold.
