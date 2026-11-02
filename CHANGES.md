# Audit and refactor

Removes price-per-meter and alternate-currency price leakage. Parses comma-separated Area values, retains neighborhood and boolean amenities, and handles unseen addresses. R2 uses y_true first. No target/correlation-based pruning touches the holdout. Random holdout does not measure price changes over time or unseen-neighborhood generalization.

Original algorithms and historical outputs remain in legacy/. No production dataset was available during refactoring; new real-data metrics remain unmeasured. See README.md for the reproducible evaluation protocol.
