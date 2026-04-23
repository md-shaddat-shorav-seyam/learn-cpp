Great—this is a **core topic in C++ (especially for competitive programming)**. I’ll break it down step by step with **concept + STL usage + patterns used in contests**.

---

# 🔷 1. Basic Set Concepts

### ✅ Union (A ∪ B)

All **unique elements** from both sets.

Example:
A = {1, 2, 3}, B = {3, 4, 5}
👉 Union = {1, 2, 3, 4, 5}

---

### ✅ Intersection (A ∩ B)

Elements **common in both sets**.

👉 Intersection = {3}

---

### ✅ Difference (A − B)

Elements in **A but NOT in B**

👉 A − B = {1, 2}
👉 B − A = {4, 5}

---

# 🔷 2. STL Containers Used

### ✔️ `set`

* Stores **unique elements**
* Sorted automatically

### ✔️ `unordered_set`

* Faster (O(1) avg)
* Not sorted

### ✔️ `multiset`

* Allows duplicates

---

# 🔷 3. C++ STL Algorithms

Header:

```cpp
#include <algorithm>
#include <set>
```

---

# 🔷 4. UNION in C++

### 🔹 Method 1: Using `set`

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    set<int> a = {1, 2, 3};
    set<int> b = {3, 4, 5};

    set<int> result;

    for (int x : a) result.insert(x);
    for (int x : b) result.insert(x);

    for (int x : result) cout << x << " ";
}
```

⏱ Complexity: O((n+m) log n)

---

### 🔹 Method 2: Using STL `set_union()`

```cpp
set_union(a.begin(), a.end(), b.begin(), b.end(),
          inserter(result, result.begin()));
```

⚠️ Important:

* Input must be **sorted**

---

# 🔷 5. INTERSECTION in C++

### 🔹 Method 1: Using set + loop

```cpp
for (int x : a) {
    if (b.count(x)) {
        result.insert(x);
    }
}
```

---

### 🔹 Method 2: Using STL `set_intersection()`

```cpp
set_intersection(a.begin(), a.end(), b.begin(), b.end(),
                 inserter(result, result.begin()));
```

---

# 🔷 6. DIFFERENCE in C++

### 🔹 A − B

```cpp
set_difference(a.begin(), a.end(), b.begin(), b.end(),
               inserter(result, result.begin()));
```

---

# 🔷 7. Using `vector` (IMPORTANT for CP)

In competitive programming, we often use **vector instead of set** for speed.

### ⚠️ Must sort first

```cpp
vector<int> a = {1, 2, 3};
vector<int> b = {3, 4, 5};

sort(a.begin(), a.end());
sort(b.begin(), b.end());

vector<int> result;
```

---

### ✔️ Union (vector)

```cpp
set_union(a.begin(), a.end(), b.begin(), b.end(),
          back_inserter(result));
```

---

### ✔️ Intersection

```cpp
set_intersection(a.begin(), a.end(), b.begin(), b.end(),
                 back_inserter(result));
```

---

### ✔️ Difference

```cpp
set_difference(a.begin(), a.end(), b.begin(), b.end(),
               back_inserter(result));
```

---

# 🔷 8. Competitive Programming Use Cases

## 🚀 1. Remove duplicates (Union idea)

```cpp
vector<int> v = {1,1,2,2,3};

sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());
```

---

## 🚀 2. Find common elements (Intersection)

👉 Example problem:

* Find common elements in two arrays

```cpp
unordered_set<int> s(a.begin(), a.end());

for (int x : b) {
    if (s.count(x)) cout << x << " ";
}
```

⏱ O(n)

---

## 🚀 3. Find missing elements (Difference)

👉 Example:

* Elements in A not in B

```cpp
for (int x : a) {
    if (!s.count(x)) cout << x << " ";
}
```

---

## 🚀 4. Two pointer technique (VERY IMPORTANT)

Used when arrays are sorted

### Intersection using 2 pointers:

```cpp
int i = 0, j = 0;

while (i < a.size() && j < b.size()) {
    if (a[i] == b[j]) {
        cout << a[i] << " ";
        i++; j++;
    }
    else if (a[i] < b[j]) i++;
    else j++;
}
```

⏱ O(n + m) → BEST

---

## 🚀 5. Frequency array / hashing

Used when values are small

```cpp
int freq[1000] = {0};

for (int x : a) freq[x]++;

for (int x : b) {
    if (freq[x]) cout << x;
}
```

---

# 🔷 9. Important Notes (VERY IMPORTANT)

### ⚠️ 1. Sorted requirement

* `set_union`, `set_intersection`, `set_difference`
  👉 Only works on **sorted data**

---

### ⚠️ 2. Duplicates behavior

* `set` → removes duplicates
* `vector` → keeps duplicates

Example:

```
A = {1,1,2}, B = {1,2,2}
```

👉 Intersection (vector):

```
{1,2}
```

👉 Intersection (multiset):

```
{1,2}
```

---

### ⚠️ 3. Output iterators

* `inserter()` → for set
* `back_inserter()` → for vector

---

# 🔷 10. When to Use What (CP Strategy)

| Situation               | Best Approach   |
| ----------------------- | --------------- |
| Need unique elements    | `set`           |
| Need speed              | `unordered_set` |
| Sorted arrays           | 2 pointers      |
| Large constraints       | hashing         |
| Need STL quick solution | `set_union` etc |

---

# 🔥 Summary

* Union → combine unique
* Intersection → common elements
* Difference → remove elements
* Use:

  * `set` → simple
  * `vector + sort` → faster
  * `two pointers` → optimal CP solution

---

If you want, I can give you:
✅ 20+ competitive problems (Codeforces style)
✅ or make a **cheat sheet PDF**
✅ or give **advanced tricks (bitmask + sets)**
