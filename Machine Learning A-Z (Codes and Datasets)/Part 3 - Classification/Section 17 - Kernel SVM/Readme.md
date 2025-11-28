# Green vs Red Dots - Clear Separation

## Setup:
- **Landmark** 🚩 at center (0, 0) where green dots cluster
- **Threshold** = 0.5 (decision boundary)
- **Rule:** Value > 0.5 = Green ✅ | Value < 0.5 = Red ❌

---

## Walking Towards the Landmark:

**🔴 RED ZONE (Far Away):**
- Distance = 5 → K = e^(−12.5) ≈ **0.00** → **RED** ❌
- Distance = 4 → K = e^(−8) ≈ **0.0003** → **RED** ❌
- Distance = 3 → K = e^(−4.5) ≈ **0.01** → **RED** ❌
- Distance = 2 → K = e^(−2) ≈ **0.14** → **RED** ❌

**🟢 GREEN ZONE (Close):**
- Distance = 1 → K = e^(−0.5) ≈ **0.61** → **GREEN** ✅
- Distance = 0.5 → K = e^(−0.125) ≈ **0.88** → **GREEN** ✅
- Distance = 0 → K = e^(0) = **1.00** → **GREEN** ✅

---

## Visualization:
```
Distance:  5  →  4  →  3  →  2  | 1  →  0.5  →  0
Value:    0.00→0.0003→0.01→0.14 |0.61→ 0.88 → 1.0
Class:    RED  RED  RED  RED    |GREEN GREEN GREEN
          🔴   🔴   🔴   🔴     |🟢   🟢    🟢
          
          |←---- FAR -----|THRESHOLD|---- CLOSE ----|
```

**The Magic:** All dots with distance > ~1.4 = Red, distance < ~1.4 = Green!

**Circular boundary created!** 🎯