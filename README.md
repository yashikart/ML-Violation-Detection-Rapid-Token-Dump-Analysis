# Wallet Violation Detection

## Overview

This project analyzes wallet reports to detect suspicious activities like rapid token dumps.  
It starts with simple rule-based detection and then uses machine learning (ML) for smarter predictions.

---

## How It Works

### Rule-Based Detection (Basic)

- Reads a CSV file `reports.csv` containing wallet reports with columns like wallet address, severity, reason, and creation timestamp.
- Groups the reports by wallet.
- Flags any wallet that has **3 or more high-severity (severity ≥ 4) reports within 1 hour** as suspicious.
- Flags with "Rapid token dump" violation and recommends freezing the wallet.
- Outputs a JSON list of flagged wallets.

### Detailed Reporting (Enhanced)

- Includes wallets even if all timestamps are missing or invalid.
- For each wallet, provides detailed reason if it is not flagged.
- Outputs a full JSON report covering all wallets — flagged or not — with explanations.

---

## Machine Learning Enhancement

To improve accuracy and handle more complex patterns, a machine learning model is used:

- Extracts features per wallet such as:
  - Total number of reports
  - Number of high-severity reports
  - Average severity score
  - Number of distinct reasons reported
  - Average time gap between high-severity reports
- Trains a Random Forest classifier to predict if a wallet should be flagged.
- Outputs probabilities for violation:
  - If probability > 0.7, recommends freezing.
  - Otherwise, marks for monitoring.
- Shows feature importance to understand key factors.

---

## How to Run

1. Place your `reports.csv` file in the project folder.
2. Run the rule-based script for quick flagging results.
3. Run the ML script to train and predict using the machine learning model.
4. Review generated JSON reports for flagged wallets and detailed reasons.

---

## Summary

- Start with simple rule-based logic to quickly catch obvious suspicious wallets.
- Use machine learning for flexible, data-driven, and probabilistic detection.
- Continuously improve the system with more data, better features, and smarter models.

---

*This README explains the core logic, outputs, and how machine learning enhances the detection process.*
