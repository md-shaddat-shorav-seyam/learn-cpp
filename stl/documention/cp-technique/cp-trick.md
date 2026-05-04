You’re asking for the *real* competitive programming tricks—the kind that saves time and turns TLE into AC. Good. Let’s go beyond basics and focus on **high-impact STL + algorithmic patterns** (like your remove–erase).

I’ll group them so you can actually remember and use them in contests.

---

# 🔥 1. Remove–Erase Pattern (you already saw)

```cpp
nums.erase(remove(nums.begin(), nums.end(), val), nums.end());
```

👉 Removes all `val` from vector in **O(n)**

---

# ⚡ 2. Unique–Erase (Remove duplicates)

```cpp
sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());
```

👉 Removes duplicates
⚠️ `unique` only removes **consecutive duplicates**, so sorting is required.

---

# ⚡ 3. Count + Frequency Trick

```cpp
count(v.begin(), v.end(), x);
```

👉 Count occurrences in O(n)

Better for large data:

```cpp
unordered_map<int,int> freq;
for (int x : v) freq[x]++;
```

---

# ⚡ 4. Lower Bound / Upper Bound (Binary Search)

```cpp
lower_bound(v.begin(), v.end(), x);
upper_bound(v.begin(), v.end(), x);
```

👉 Must be **sorted**

* `lower_bound` → first ≥ x
* `upper_bound` → first > x

Count occurrences:

```cpp
int cnt = upper_bound(v.begin(), v.end(), x) - lower_bound(v.begin(), v.end(), x);
```

---

# ⚡ 5. All Permutations

```cpp
sort(v.begin(), v.end());
do {
    // process
} while (next_permutation(v.begin(), v.end()));
```

---

# ⚡ 6. Reverse Quickly

```cpp
reverse(v.begin(), v.end());
```

---

# ⚡ 7. Min / Max Element

```cpp
*min_element(v.begin(), v.end());
*max_element(v.begin(), v.end());
```

---

# ⚡ 8. Accumulate (Sum)

```cpp
accumulate(v.begin(), v.end(), 0);
```

---

# ⚡ 9. Lambda Sorting (VERY IMPORTANT)

```cpp
sort(v.begin(), v.end(), [](pair<int,int> a, pair<int,int> b){
    return a.second < b.second;
});
```

👉 Sort by second value

---

# ⚡ 10. Custom Comparator Trick (Descending)

```cpp
sort(v.begin(), v.end(), greater<int>());
```

---

# ⚡ 11. Two Pointer Technique

```cpp
int l = 0, r = n - 1;
while (l < r) {
    if (condition) l++;
    else r--;
}
```

👉 Used in:

* Two sum (sorted)
* Sliding window
* Palindrome

---

# ⚡ 12. Sliding Window (Subarray problems)

```cpp
int l = 0;
for (int r = 0; r < n; r++) {
    while (invalid) {
        l++;
    }
}
```

👉 Best for:

* Longest substring
* Subarray sum

---

# ⚡ 13. Fast I/O (IMPORTANT in CP)

```cpp
ios::sync_with_stdio(false);
cin.tie(NULL);
```

---

# ⚡ 14. Prefix Sum Trick

```cpp
prefix[i] = prefix[i-1] + v[i];
```

Range sum:

```cpp
sum(l, r) = prefix[r] - prefix[l-1];
```

---

# ⚡ 15. Difference Array (Range update)

```cpp
diff[l] += val;
diff[r+1] -= val;
```

---

# ⚡ 16. Set Trick (Unique + Sorted)

```cpp
set<int> st(v.begin(), v.end());
```

---

# ⚡ 17. Multiset (Duplicates + Sorted)

```cpp
multiset<int> ms;
ms.insert(x);
ms.erase(ms.find(x)); // erase one occurrence
```

---

# ⚡ 18. Priority Queue (Heap)

```cpp
priority_queue<int> pq; // max heap
priority_queue<int, vector<int>, greater<int>> pq; // min heap
```

---

# ⚡ 19. Bit Tricks

Check power of 2:

```cpp
(x & (x - 1)) == 0
```

Count bits:

```cpp
__builtin_popcount(x);
```

---

# ⚡ 20. GCD / LCM

```cpp
__gcd(a, b);
lcm = (a / __gcd(a,b)) * b;
```

---

# ⚡ 21. Kadane’s Algorithm (Max subarray)

```cpp
int sum = 0, mx = INT_MIN;
for (int x : v) {
    sum = max(x, sum + x);
    mx = max(mx, sum);
}
```

---

# ⚡ 22. Coordinate Compression

```cpp
vector<int> temp = v;
sort(temp.begin(), temp.end());
temp.erase(unique(temp.begin(), temp.end()), temp.end());

for (int &x : v) {
    x = lower_bound(temp.begin(), temp.end(), x) - temp.begin();
}
```

---

# ⚡ 23. Map Sorting Trick

```cpp
vector<pair<int,int>> v(mp.begin(), mp.end());
sort(v.begin(), v.end());
```

---

# ⚡ 24. Erase While Iterating (Safe way)

```cpp
for (auto it = st.begin(); it != st.end(); ) {
    if (*it == x) it = st.erase(it);
    else it++;
}
```

---

# ⚡ 25. Check Subsequence

```cpp
int j = 0;
for (int i = 0; i < s.size(); i++) {
    if (s[i] == t[j]) j++;
}
```

---

# 💡 Final Advice (Important)

Don’t just memorize. Practice on:

* Codeforces
* AtCoder
* LeetCode

---

If you want next level 🚀
I can give you:

* **Full CP template (ready for contest)**
* **Top 50 must-solve problems**
* **Pattern-wise roadmap (2-pointer, DP, graphs, etc.)**

Just tell me 👍
