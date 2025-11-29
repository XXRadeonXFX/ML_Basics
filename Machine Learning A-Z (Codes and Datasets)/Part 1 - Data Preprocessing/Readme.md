# Data Preprocessing - Quick Notes

---

## 1. SimpleImputer - Filling Missing Values

### The Problem:
```
Your data has missing values (NaN):
[25, NaN, 30, NaN, 50]
      ↑        ↑
   Missing! Missing!
```

### The Solution:
```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
                        ↑                       ↑
                   What to find?          How to replace?

imputer.fit(X[:, 1:3])
# LEARNS: Calculate mean of columns 1 and 2
# Example: Column 1 mean = 30, Column 2 mean = 45

X[:, 1:3] = imputer.transform(X[:, 1:3])
# REPLACES: All NaN with the learned means
```

---

### Simple Example:

```python
# Before:
X = [[1, 10, NaN],
     [2, NaN, 30],
     [3, 20, 40]]

# Imputer learns:
# Column 1 mean = (10+20)/2 = 15
# Column 2 mean = (30+40)/2 = 35

imputer.fit(X[:, 1:3])

# After transform:
X = [[1, 10, 35],   ← NaN replaced with 35
     [2, 15, 30],   ← NaN replaced with 15
     [3, 20, 40]]
```

---

### Strategies:

```python
strategy='mean'     # Replace with average (most common)
strategy='median'   # Replace with middle value
strategy='most_frequent'  # Replace with most common value
strategy='constant' # Replace with a specific number
```

---

## 2. OneHotEncoder - Converting Categories to Numbers

### The Problem:
```
Countries: ['France', 'Spain', 'Germany', 'Spain', 'France']
           ↑
Machine learning needs NUMBERS, not text!
```

### The Solution (One-Hot Encoding):
```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder

ct = ColumnTransformer(
    transformers=[('encoder', OneHotEncoder(), [0])],
                   ↑          ↑                 ↑
                 Name      What to use    Which column?
    remainder='passthrough'
              ↑
    Keep other columns unchanged
)

X = ct.fit_transform(X)
```

---

### What OneHotEncoder Does:

```
Before:
Country
-------
France    →  [1, 0, 0]  (France=1, Spain=0, Germany=0)
Spain     →  [0, 1, 0]  (France=0, Spain=1, Germany=0)
Germany   →  [0, 0, 1]  (France=0, Spain=0, Germany=1)
Spain     →  [0, 1, 0]
France    →  [1, 0, 0]

One column becomes THREE columns (one for each category)
```

---

### Complete Example:

```python
# Before:
X = [['France', 25, 50000],
     ['Spain', 30, 60000],
     ['Germany', 35, 70000]]
      ↑
    Column 0 (categorical)

# After OneHotEncoder on column 0:
X = [[1, 0, 0, 25, 50000],  ← France
     [0, 1, 0, 30, 60000],  ← Spain
     [0, 0, 1, 35, 70000]]  ← Germany
      ↑  ↑  ↑   ↑     ↑
      F  S  G  Age  Salary (remainder='passthrough')
```

---

## 3. LabelEncoder - Simple Category to Number

### For Target Variable (y):

```python
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
y = le.fit_transform(y)
```

---

### What LabelEncoder Does:

```
Before:
y = ['Yes', 'No', 'Yes', 'No', 'Yes']

After:
y = [1, 0, 1, 0, 1]
     ↑     ↑
   Yes=1  No=0

Simple: Just converts categories to 0, 1, 2, 3...
```

---

## Key Differences:

| Method | Use For | Output |
|--------|---------|--------|
| **OneHotEncoder** | Features (X) with categories | Multiple columns (0s and 1s) |
| **LabelEncoder** | Target (y) with categories | Single column (0, 1, 2...) |

---

### Why Different Encoding?

```
OneHotEncoder (for X):
Country: France, Spain, Germany
→ [1,0,0], [0,1,0], [0,0,1]
Why? Prevents model thinking Germany(2) > Spain(1)

LabelEncoder (for y):
Output: Yes, No
→ [1, 0]
Why? Simple binary - No ordering confusion
```

---

## Complete Workflow:

```python
# 1. Handle missing values
imputer = SimpleImputer(strategy='mean')
X[:, 1:3] = imputer.fit_transform(X[:, 1:3])

# 2. Encode categorical features (X)
ct = ColumnTransformer(
    transformers=[('encoder', OneHotEncoder(), [0])],
    remainder='passthrough'
)
X = ct.fit_transform(X)

# 3. Encode categorical target (y)
le = LabelEncoder()
y = le.fit_transform(y)
```

---

## Remember:

```
SimpleImputer    → Fill missing values (NaN → mean/median)
OneHotEncoder    → Categories → Multiple columns (for X)
LabelEncoder     → Categories → Single numbers (for y)
```

**Done!** 🎯