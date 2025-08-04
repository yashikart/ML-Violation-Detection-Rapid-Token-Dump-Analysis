Wallet Violation Detection System
================================

Overview:
---------
This project detects suspicious blockchain wallets based on analysis of report data.
It uses both rule-based methods and machine learning (ML) to find wallets involved in rapid token dumps or other suspicious activities.

How It Works:
-------------

1. Rule-Based Detection:
   - Loads 'reports.csv' with columns: Wallet, Severity, Reason, Created At.
   - Groups data by wallet.
   - Flags wallets with 3 or more high-severity (Severity >= 4) reports within 1 hour.
   - Outputs JSON with address, violation type, score (0.75-1.0), and recommended action ('freeze').

2. Full Wallet Report:
   - Covers all wallets, even those with missing or invalid timestamps.
   - For unflagged wallets, provides clear reasons why.
   - Outputs detailed JSON report for every wallet.

3. Real-Time Detection (Simulated):
   - Processes incoming reports in streaming fashion.
   - Maintains a sliding time window (1 hour) per wallet.
   - Flags wallets immediately when rapid token dump pattern detected.
   - Prints alerts with violation info.

4. Machine Learning Detection:
   - Extracts features per wallet:
       * Total reports count
       * Count of high-severity reports
       * Average severity
       * Number of distinct reasons
       * Average time gap between high-severity events
   - Trains Random Forest classifier on synthetic labels.
   - Predicts violation probability.
   - Flags wallets for freeze if probability > 0.7; otherwise monitor.
   - Shows feature importance for explainability.

How To Run:
-----------
- Place your 'reports.csv' in the project folder.
- Run rule-based scripts for quick flagging.
- Run full report script for detailed audit info.
- Run real-time detection simulation for streaming scenarios.
- Run ML scripts for data-driven prediction.

Outputs:
--------
- ml_violations.json: flagged wallets by rule-based method
- full_wallet_report.json: detailed report for every wallet with reasons
- ml_predictions.json: ML predicted probabilities and recommendations

Example Output (Rule-Based):
----------------------------
[
    {
        "address": "0xabc123",
        "violation": "Rapid token dump",
        "score": 1.0,
        "recommended_action": "freeze"
    },
    {
        "address": "0xdef456",
        "violation": "Rapid token dump",
        "score": 0.9,
        "recommended_action": "freeze"
    }
]

Example Output (Full Report):
-----------------------------
{
    "address": "0x123",
    "flagged": false,
    "reason": "Only 1 high severity reports (need 3+)",
    "violation": null,
    "score": null,
    "recommended_action": null
}

Example Real-Time Alert:
------------------------
ALERT: {
    "address": "0xabc123",
    "violation": "Rapid token dump",
    "score": 0.75,
    "recommended_action": "freeze"
}

Example ML Prediction:
----------------------
{
    "address": "0xabc123",
    "violation_probability": 0.84,
    "violation": "Rapid token dump",
    "recommended_action": "freeze"
}

Summary:
--------
Start simple with rule-based logic for fast suspicious wallet detection.
Add machine learning for smarter, probabilistic identification.
Continuously improve data, features, and models for better security monitoring.



---

