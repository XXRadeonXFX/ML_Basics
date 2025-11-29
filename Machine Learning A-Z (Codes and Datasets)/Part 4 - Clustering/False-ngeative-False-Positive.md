# False Positive vs False Negative - Advanced Cheat Sheet

---

## Core Definitions

```
FALSE POSITIVE (Type I Error):
Predicted = 1  |  Actual = 0
"Said YES when it was NO" - False Alarm 🚨

FALSE NEGATIVE (Type II Error):  
Predicted = 0  |  Actual = 1
"Said NO when it was YES" - Missed Detection 😴
```

---

## Position in Confusion Matrix

```
                Predicted
                NO   YES
            ┌──────────┐
Actual  NO  │ TN   FP  │ ← FP here
            ├──────────┤
        YES │ FN   TP  │ ← FN here
            └──────────┘
```

---

## Real-World Trade-offs

| Domain | FP Impact | FN Impact | Optimize For |
|--------|-----------|-----------|--------------|
| **Cancer Screening** | Unnecessary biopsy, anxiety | Untreated cancer, death | Minimize FN ☠️ |
| **Spam Filter** | Miss important email | Inbox clutter | Minimize FP 📧 |
| **Fraud Detection** | Transaction blocked | Money stolen | Balance ⚖️ |
| **Criminal Justice** | Innocent jailed | Criminal free | Minimize FP ⚖️ |
| **Fire Alarm** | False evacuation | Building burns | Minimize FN 🔥 |
| **COVID Test** | Unnecessary quarantine | Spread disease | Minimize FN 🦠 |

---

## Mathematical Relationships

```
Precision = TP / (TP + FP)
↑ Affected by FP - High FP = Low Precision

Recall = TP / (TP + FN)  
↑ Affected by FN - High FN = Low Recall

F1 Score = 2 × (Precision × Recall) / (Precision + Recall)
↑ Balances both errors
```

---

## Threshold Impact

```
Lower Threshold → More Positives → ↑FP, ↓FN
Higher Threshold → Fewer Positives → ↓FP, ↑FN

         Sensitivity ↔ Specificity
         (Recall)        (1 - FP Rate)
              Can't optimize both!
```

---

## Cost-Sensitive Learning

```
Cost(FP) vs Cost(FN)

Medical: Cost(FN) >> Cost(FP) → Lower threshold
Spam: Cost(FP) >> Cost(FN) → Higher threshold  
Security: Cost(FP) ≈ Cost(FN) → Balanced threshold

Adjust decision boundary based on domain cost!
```

---

## Metrics to Use

```
High FN Cost (life/death):
→ Maximize Recall (Sensitivity)
→ Minimize FN at expense of FP

High FP Cost (false accusations):
→ Maximize Precision  
→ Minimize FP at expense of FN

Balanced:
→ Optimize F1-Score or AUC-ROC
```

---

## Memory Aids

```
FP = "False Alarm" - Predicted danger, but safe
FN = "Missed Opportunity" - Predicted safe, but danger

Alpha (α) = P(Type I Error) = P(FP)
Beta (β) = P(Type II Error) = P(FN)
Power = 1 - β = Ability to detect true positives
```

---

## Quick Decision Framework

```
Ask: "What's worse in my domain?"

Worse to MISS something → Minimize FN
Worse to FALSE ALARM → Minimize FP  
Equal importance → Balance both

Then tune threshold/model accordingly.
```

---

**Key Insight:** There's always a trade-off. Choose based on domain consequences. 🎯