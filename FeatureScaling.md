# fit_transform vs transform - MINIMAL VERSION

## The Story: Learning to Cook 👨‍🍳

### Training Phase:
```
Cooking school teaches you:
"Small pizza = 200g dough"
"Large pizza = 600g dough"

You LEARN and WRITE DOWN these rules 📝

This is fit_transform(X_train)
→ LEARN the rules
→ USE the rules
```

### Testing Phase:
```
You open your pizza shop.

✅ CORRECT: Use SAME rules (200g, 600g)
❌ WRONG: Make up NEW rules every day

This is transform(X_test)
→ USE the same rules
→ DON'T learn new rules
```

---

## Code Example:

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()

# TRAINING - Learn + Use
X_train_scaled = scaler.fit_transform(X_train)
                        ↑
                 LEARN rules from this data

# TESTING - Only Use
X_test_scaled = scaler.transform(X_test)
                       ↑
                 USE same rules (don't learn new!)
```

---

## Why?

```
Training: [10, 20, 30, 40, 50]
Learns: Min=10, Max=50

Testing: [15, 25, 100]
Uses: Min=10, Max=50 (SAME rules!)

❌ If you learn new rules from test data:
   Model sees DIFFERENT scales = WRONG predictions!
```

---

## Remember:

```
fit_transform = LEARN + USE  (Training only!)
transform     = USE ONLY     (Testing only!)

Never learn from test data! 🎯
```

**That's it!** 🎉