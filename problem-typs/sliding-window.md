# 🪟 Sliding Window — Complete C++ Reference

---

## Table of Contents
1. [Core Idea](#1-core-idea)
2. [Fixed-Size Window](#2-fixed-size-window)
3. [Variable-Size Window (Shrinkable)](#3-variable-size-window-shrinkable)
4. [Window with Frequency Map](#4-window-with-frequency-map)
5. [Window with Two Pointers on Sorted Array](#5-window-with-two-pointers-on-sorted-array)
6. [Minimum Window Substring (Classic Hard)](#6-minimum-window-substring-classic-hard)
7. [At Most K Trick](#7-at-most-k-trick)
8. [Monotonic Deque Window (Sliding Window Maximum)](#8-monotonic-deque-window-sliding-window-maximum)
9. [Binary Search + Sliding Window](#9-binary-search--sliding-window)
10. [Common Tricks & Pitfalls](#10-common-tricks--pitfalls)

---

## 1. Core Idea

A **sliding window** maintains a contiguous subarray/substring using two pointers `l` and `r` (left and right). Instead of recomputing the whole window, you slide it — adding from the right, removing from the left.

```
Array: [a, b, c, d, e, f]
          ^--------^
          l        r   ← This is your window
```

**Two main types:**
| Type | Window Size | When to use |
|------|-------------|-------------|
| Fixed | Constant `k` | "find max sum of subarray of size k" |
| Variable | Shrinks/grows | "find smallest subarray with sum ≥ x" |

---

## 2. Fixed-Size Window

### Template

```cpp
// Scenario: Maximum sum of subarray of exactly size k
int fixedWindow(vector<int>& arr, int k) {
    int n = arr.size();
    int windowSum = 0, maxSum = INT_MIN;

    for (int r = 0; r < n; r++) {
        windowSum += arr[r];              // Expand window

        if (r >= k - 1) {                // Window is full
            maxSum = max(maxSum, windowSum);
            windowSum -= arr[r - k + 1]; // Shrink from left
        }
    }
    return maxSum;
}
```

### Example
```
arr = [2, 1, 5, 1, 3, 2], k = 3

Window [2,1,5] → sum=8
Window [1,5,1] → sum=7
Window [5,1,3] → sum=9  ← max
Window [1,3,2] → sum=6

Answer: 9
```

---

## 3. Variable-Size Window (Shrinkable)

### Template

```cpp
// Scenario: Smallest subarray with sum >= target
int variableWindow(vector<int>& arr, int target) {
    int n = arr.size();
    int l = 0, windowSum = 0;
    int minLen = INT_MAX;

    for (int r = 0; r < n; r++) {
        windowSum += arr[r];              // Expand

        while (windowSum >= target) {     // Condition met → try to shrink
            minLen = min(minLen, r - l + 1);
            windowSum -= arr[l++];        // Shrink from left
        }
    }
    return (minLen == INT_MAX) ? 0 : minLen;
}
```

### Example
```
arr = [2, 3, 1, 2, 4, 3], target = 7

r=0: sum=2
r=1: sum=5
r=2: sum=6
r=3: sum=8 ≥ 7 → len=4, shrink → sum=6, l=1
r=4: sum=10 ≥ 7 → len=4, shrink → sum=7 ≥ 7 → len=3, shrink → sum=4, l=3
r=5: sum=7 ≥ 7 → len=3→2? → len=2 [4,3] ✓

Answer: 2
```

---

## 4. Window with Frequency Map

### Template

```cpp
// Scenario: Longest substring with at most k distinct characters
int atMostKDistinct(string& s, int k) {
    unordered_map<char, int> freq;
    int l = 0, maxLen = 0;

    for (int r = 0; r < s.size(); r++) {
        freq[s[r]]++;                        // Add to window

        while (freq.size() > k) {            // Violated → shrink
            freq[s[l]]--;
            if (freq[s[l]] == 0)
                freq.erase(s[l]);
            l++;
        }

        maxLen = max(maxLen, r - l + 1);     // Update answer
    }
    return maxLen;
}
```

### Example
```
s = "eceba", k = 2

r=0: {e:1}          → len=1
r=1: {e:1,c:1}      → len=2
r=2: {e:2,c:1}      → len=3
r=3: {e:2,c:1,b:1}  → 3 distinct > 2, shrink:
     remove e → {e:1,c:1,b:1} → l=1
     remove c → {e:1,b:1}     → l=2, now ok → len=2
r=4: {e:1,b:1,a:1}  → 3 distinct > 2, shrink...
     → len=2 [ba]

Answer: 3
```

---

## 5. Window with Two Pointers on Sorted Array

### Template

```cpp
// Scenario: Count pairs with sum in range [lo, hi]
int countPairsInRange(vector<int>& arr, int lo, int hi) {
    // Works on sorted array
    sort(arr.begin(), arr.end());
    int n = arr.size(), count = 0;

    // Count pairs with sum <= x
    auto atMost = [&](int x) {
        int l = 0, r = n - 1, cnt = 0;
        while (l < r) {
            if (arr[l] + arr[r] <= x) {
                cnt += r - l;   // all pairs (l, l+1..r) are valid
                l++;
            } else {
                r--;
            }
        }
        return cnt;
    };

    return atMost(hi) - atMost(lo - 1);
}
```

---

## 6. Minimum Window Substring (Classic Hard)

### Template

```cpp
// Scenario: Minimum window in s that contains all chars of t
string minWindow(string s, string t) {
    unordered_map<char, int> need, have_map;
    for (char c : t) need[c]++;

    int have = 0, required = need.size();
    int l = 0, minLen = INT_MAX, start = 0;

    for (int r = 0; r < s.size(); r++) {
        char c = s[r];
        have_map[c]++;

        // Did this char satisfy a requirement?
        if (need.count(c) && have_map[c] == need[c])
            have++;

        // All satisfied → try to shrink
        while (have == required) {
            if (r - l + 1 < minLen) {
                minLen = r - l + 1;
                start = l;
            }
            have_map[s[l]]--;
            if (need.count(s[l]) && have_map[s[l]] < need[s[l]])
                have--;
            l++;
        }
    }
    return (minLen == INT_MAX) ? "" : s.substr(start, minLen);
}
```

### Example
```
s = "ADOBECODEBANC", t = "ABC"

Expand until we have A, B, C → "ADOBEC" (len=6)
Shrink: remove A → need A again
Expand → "ADOBECODEBA" has A,B,C
Shrink → "DOBECODEBA", "OBECODEBA", "BECODEBA" → "BANC" (len=4) ✓

Answer: "BANC"
```

---

## 7. At Most K Trick

> **Used when:** "exactly K" problems are hard. Instead, solve:
> `exactly(K) = atMost(K) - atMost(K-1)`

```cpp
// Scenario: Number of subarrays with exactly k odd numbers
int atMostK(vector<int>& arr, int k) {
    int l = 0, count = 0, odds = 0;
    for (int r = 0; r < arr.size(); r++) {
        if (arr[r] % 2 != 0) odds++;
        while (odds > k) {
            if (arr[l] % 2 != 0) odds--;
            l++;
        }
        count += r - l + 1;  // All subarrays ending at r are valid
    }
    return count;
}

int exactlyK(vector<int>& arr, int k) {
    return atMostK(arr, k) - atMostK(arr, k - 1);
}
```

### Example
```
arr = [1, 1, 2, 1, 1], k = 3

atMost(3) = 12
atMost(2) = 9
exactlyK(3) = 12 - 9 = 3

The 3 subarrays: [1,1,2,1], [1,1,2,1,1], [1,2,1,1]
```

---

## 8. Monotonic Deque Window (Sliding Window Maximum)

### Template

```cpp
// Scenario: Maximum in every window of size k
vector<int> slidingWindowMax(vector<int>& arr, int k) {
    deque<int> dq;   // Stores indices, front = max of window
    vector<int> result;

    for (int r = 0; r < arr.size(); r++) {
        // Remove indices out of window
        while (!dq.empty() && dq.front() < r - k + 1)
            dq.pop_front();

        // Maintain decreasing order (remove smaller from back)
        while (!dq.empty() && arr[dq.back()] < arr[r])
            dq.pop_back();

        dq.push_back(r);

        if (r >= k - 1)
            result.push_back(arr[dq.front()]);
    }
    return result;
}
```

### Example
```
arr = [1, 3, -1, -3, 5, 3, 6, 7], k = 3

Window [1,3,-1]  → max = 3
Window [3,-1,-3] → max = 3
Window [-1,-3,5] → max = 5
Window [-3,5,3]  → max = 5
Window [5,3,6]   → max = 6
Window [3,6,7]   → max = 7

Result: [3, 3, 5, 5, 6, 7]
```

---

## 9. Binary Search + Sliding Window

When the window size isn't obvious but is **monotonic** (larger window → easier/harder to satisfy), binary search on window size.

```cpp
// Scenario: Smallest window size k such that some condition holds
bool check(vector<int>& arr, int k) {
    // Check if any window of size k satisfies condition
    // ... fixed window logic here
    return true; // or false
}

int binarySearchWindow(vector<int>& arr) {
    int lo = 1, hi = arr.size(), ans = -1;
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        if (check(arr, mid)) {
            ans = mid;
            hi = mid - 1;   // Try smaller
        } else {
            lo = mid + 1;   // Need bigger window
        }
    }
    return ans;
}
```

---

## 10. Common Tricks & Pitfalls

### ✅ Key Tricks

| Trick | When to Use |
|-------|-------------|
| `count += r - l + 1` | Count all subarrays ending at `r` |
| `atMost(k) - atMost(k-1)` | "Exactly k" problems |
| `unordered_map` with size check | Track distinct elements |
| Monotonic deque | Window min/max in O(n) |
| `have` + `required` counters | Avoid re-checking entire map |

### ⚠️ Common Pitfalls

```cpp
// ❌ Wrong: shrinking with if instead of while
if (condition violated) { l++; }

// ✅ Correct: keep shrinking until valid
while (condition violated) { l++; }

// ❌ Wrong: updating answer outside the valid window check
maxLen = max(maxLen, r - l + 1); // placed before shrink

// ✅ Correct: update AFTER ensuring window is valid
while (violated) { shrink; }
maxLen = max(maxLen, r - l + 1);

// ❌ Forgetting to erase from map
freq[s[l]]--;
l++;  // map still has key with 0 → freq.size() stays wrong

// ✅ Always erase zero-count entries
freq[s[l]]--;
if (freq[s[l]] == 0) freq.erase(s[l]);
l++;
```

### 📌 Decision Flowchart

```
Is window size fixed?
  ├── YES → Fixed Window Template (#2)
  └── NO  → Variable Window
            │
            ├── Need min/max in window? → Monotonic Deque (#8)
            ├── Exactly K problem?      → atMost(k) - atMost(k-1) (#7)
            ├── Track distinct chars?   → Frequency Map (#4)
            ├── Min window with all?    → Min Window Substring (#6)
            └── Count valid subarrays? → count += r - l + 1
```

---

## Quick Reference Complexity

| Template | Time | Space |
|----------|------|-------|
| Fixed Window | O(n) | O(1) |
| Variable Window | O(n) | O(1) |
| Frequency Map Window | O(n) | O(k) |
| Min Window Substring | O(n + m) | O(m) |
| At Most K Trick | O(n) | O(1) |
| Monotonic Deque | O(n) | O(k) |
| Binary Search + Window | O(n log n) | O(1) |
