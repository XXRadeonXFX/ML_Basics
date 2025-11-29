# Elastic Net Regression

## What is Elastic Net?

**Elastic Net = Ridge + Lasso COMBINED!** 🎯

It's the **best of both worlds**:

```
Ridge:  Shrinks all features 📉
Lasso:  Deletes weak features ✂️

Elastic Net: Does BOTH! 🔥
```

---

## How It Works:

```
Cost = Error + α × [L1_ratio × |β| + (1-L1_ratio) × β²]
                    ↑                  ↑
                  Lasso              Ridge
                (Delete)           (Shrink)
```

**Two dials to control:**
1. **alpha** (α) = How strict overall
2. **l1_ratio** = Mix between Lasso and Ridge

---

## The L1_Ratio Slider:

```
l1_ratio = 0.0  → 100% Ridge (shrink all)
l1_ratio = 0.5  → 50/50 Mix ⚖️ (best balance!)
l1_ratio = 1.0  → 100% Lasso (delete weak)
```

---

## Example:

```python
from sklearn.linear_model import ElasticNet

model = ElasticNet(alpha=1.0, l1_ratio=0.5)
model.fit(X_train, y_train)

# Result: 
# - Shrinks all features (like Ridge)
# - Deletes some features (like Lasso)
# Best of both! 🎯
```

---

## When to Use Elastic Net?

```
✅ Many correlated features (Ridge can't handle alone)
✅ Want feature selection (Lasso alone is unstable)
✅ Don't know if Ridge or Lasso is better

→ Use Elastic Net! It combines both strengths!
```

---

## Is It In Your Course? 🔍

Looking at your course structure... **NO, Elastic Net is NOT included.** ❌

Your course has:
- Part 2 - Regression (no Ridge/Lasso/Elastic Net)
- Part 10 - Model Selection & Boosting (might mention it?)

**Ridge, Lasso, and Elastic Net are missing from this course!**

But now you know them anyway! 💪

---

## Quick Summary:

| Method | What it does |
|--------|-------------|
| **Ridge** | Shrinks all features 📉 |
| **Lasso** | Deletes weak features ✂️ |
| **Elastic Net** | Does BOTH! 🎯 |

**Elastic Net = The complete package!**