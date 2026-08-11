# 🛡️ Phishing URL Classifier with Explainable AI (XAI)

An end-to-end machine learning pipeline that detects phishing URLs using custom lexical feature engineering and provides local, human-readable explanations for every alert using **SHAP (SHapley Additive exPlanations)**.

Designed to bridge the gap between AI accuracy and Security Operations Center (SOC) trust by turning "black-box" machine learning classifications into transparent, actionable threat intelligence.

---

## 🎯 Problem Statement & Motivation

In modern SOC workflows, automated security classifiers often suffer from two major drawbacks:
1. **Alert Fatigue:** High volumes of automated alerts without context force Tier 1/2 analysts to waste time manually verifying DNS and WHOIS records.
2. **The "Black Box" Problem:** Traditional deep learning or tree-based classifiers output confidence scores (e.g., *94% Phishing*) without explaining *why* a URL was flagged, making it difficult to verify alerts or diagnose False Positives.

This project solves this by pairing a **Random Forest Classifier** with **SHAP TreeExplainer**, giving security teams instant visibility into the exact lexical signals driving each classification.

---

## ✨ Key Features

- **Custom Lexical Feature Extraction:** Transforms raw URL strings into quantitative security signals using Python's `urllib`, regular expressions, and mathematical analysis:
  - `url_length`: Detects padding and hidden payload parameters.
  - `hostname_length`: Identifies deeply nested, deceptive subdomains.
  - `has_ip`: Flags raw IPv4 addresses used in place of domain names.
  - `special_chars`: Counts obfuscation and brand-mimicking symbols (`@`, `-`, `?`, `=`, `%`).
  - `entropy`: Calculates Shannon Entropy to catch Domain Generation Algorithms (DGAs) and random character strings.
- **Global & Local Explainability:**
  - **Global Importance:** Identifies overarching model behaviors across the entire dataset (`len(url)` and `entropy` rank as primary indicators).
  - **Local SHAP Waterfall Plots:** Generates individual feature attribution charts for any flagged alert, allowing analysts to instantly see which features pushed the decision toward Benign or Phishing.
- **False Positive Triage:** Proves how XAI helps analysts identify model blind spots (e.g., legitimate long query strings like Google Search links) without blocking critical business tools.

---

## 🛠️ Tech Stack

- **Language:** Python 3.10+
- **Machine Learning:** Scikit-Learn (`RandomForestClassifier`)
- **Explainable AI (XAI):** SHAP (`TreeExplainer`)
- **Data Manipulation:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
