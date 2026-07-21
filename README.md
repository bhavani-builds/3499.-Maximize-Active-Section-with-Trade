# 🔄 Maximum Active Sections After One Trade

## 📌 Problem Statement

You are given a binary string `s` where:

- `'1'` represents an **active** section.
- `'0'` represents an **inactive** section.

You can perform **at most one trade** to maximize the number of active sections.

A trade consists of:

1. Converting a contiguous block of `'1'`s that is surrounded by `'0'`s into `'0'`s.
2. Converting a contiguous block of `'0'`s that is surrounded by `'1'`s into `'1'`s.

The string is treated as:

```text
t = "1" + s + "1"
```

The added `'1'` characters are only used to determine valid trades and are **not included** in the final answer.

---

## 💡 Approach

1. Count the initial number of active sections (`'1'`s).
2. Augment the string by adding `'1'` at both ends.
3. Perform **Run-Length Encoding (RLE)** to group consecutive identical characters.
4. Traverse every `'1'` block that is surrounded by two `'0'` blocks.
5. For each valid block, compute the gain:

```text
Gain = Left Zero Block + Right Zero Block
```

6. The maximum answer is:

```text
Initial Active Sections + Maximum Gain
```

---

## ✅ Python Solution

```python
class Solution(object):
    def maxActiveSectionsAfterTrade(self, s):
        t = "1" + s + "1"
        original = s.count('1')

        runs = []
        i = 0
        while i < len(t):
            j = i
            while j < len(t) and t[j] == t[i]:
                j += 1
            runs.append((t[i], j - i))
            i = j

        ans = original

        for i in range(1, len(runs) - 1):
            if (runs[i][0] == '1' and
                runs[i - 1][0] == '0' and
                runs[i + 1][0] == '0'):
                gain = runs[i - 1][1] + runs[i + 1][1]
                ans = max(ans, original + gain)

        return ans
```

---

## 📖 Example

### Example 1

**Input**

```text
s = "1000100"
```

**Output**

```text
7
```

**Explanation**

```
Original String:
1000100

Augmented String:
110001001

Runs:
1(2) → 0(3) → 1(1) → 0(2) → 1(1)

Gain = 3 + 2 = 5

Original Active Sections = 2

Maximum Active Sections = 2 + 5 = 7
```

---

## 🧠 Algorithm

- Count total `'1'`s.
- Compress the augmented string into runs.
- Identify every pattern:

```
0...0  1...1  0...0
```

- Calculate:

```
gain = left_zero_run + right_zero_run
```

- Return:

```
original_ones + maximum_gain
```

---

## ⏱️ Complexity Analysis

| Complexity | Value |
|------------|-------|
| Time | **O(n)** |
| Space | **O(n)** |

---

## 🛠️ Topics

- String
- Greedy
- Run-Length Encoding (RLE)
- Simulation
- Arrays

---

## 📚 Key Concepts

- Run-Length Encoding (RLE)
- String Manipulation
- Greedy Optimization
- Pattern Recognition
- Linear Traversal

---

## 🚀 LeetCode

- **Difficulty:** Medium
- **Language:** Python
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)`

---

⭐ If you found this solution helpful, consider giving the repository a **star**!
