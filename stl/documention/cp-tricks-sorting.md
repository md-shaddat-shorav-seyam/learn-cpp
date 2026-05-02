Alright — this is a **core competitive programming (CP)** topic. If you master sorting with `map`, `vector<pair>`, and custom comparators, you’ll unlock a lot of problems.

I’ll keep it **practical + CP-focused**, not just theory.

---

# 🔹 1. Sorting `vector<int>`

Basic:

```cpp
vector<int> v = {5, 2, 9, 1};

sort(v.begin(), v.end()); // ascending
sort(v.rbegin(), v.rend()); // descending
```

---

# 🔹 2. Sorting `vector<pair<int,int>>`

### ✅ Default behavior

```cpp
vector<pair<int,int>> v = {{2,3}, {1,5}, {2,1}};
sort(v.begin(), v.end());
```

➡️ Sorts:

* First by `.first`
* If equal → by `.second`

Result:

```
{1,5}, {2,1}, {2,3}
```

---

### ✅ Custom sorting (VERY IMPORTANT for CP)

### 🔸 Sort by second

```cpp
sort(v.begin(), v.end(), [](pair<int,int> a, pair<int,int> b){
    return a.second < b.second;
});
```

---

### 🔸 Sort by second descending

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

### 🔸 Multi-condition sorting (CP GOLD)

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    if(a.first == b.first)
        return a.second > b.second; // second descending
    return a.first < b.first; // first ascending
});
```

---

# 🔹 3. Sorting `vector<pair<string,int>>`

```cpp
vector<pair<string,int>> v = {{"apple",3}, {"banana",1}, {"apple",5}};
```

### 🔸 Sort by string

```cpp
sort(v.begin(), v.end());
```

---

### 🔸 Sort by frequency (int)

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

# 🔹 4. Sorting `map<string,int>`

⚠️ Important:

* `map` is **always sorted by key (string)** automatically.

```cpp
map<string,int> mp;
```

You **CANNOT change its sorting directly**.

---

## 🔸 Trick: Convert map → vector

```cpp
map<string,int> mp = {{"a",5}, {"c",2}, {"b",8}};

vector<pair<string,int>> v(mp.begin(), mp.end());
```

---

### 🔸 Sort by value (VERY COMMON CP)

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

# 🔹 5. Sorting `unordered_map`

Same trick:

```cpp
unordered_map<string,int> mp;

vector<pair<string,int>> v(mp.begin(), mp.end());
sort(v.begin(), v.end(), ...);
```

---

# 🔹 6. Using `set` / `multiset` for sorting (CP Trick)

### 🔸 Auto sorting

```cpp
set<int> s = {5,1,3}; // always sorted
```

---

### 🔸 Custom comparator

```cpp
set<int, greater<int>> s; // descending
```

---

### 🔸 Pair inside set

```cpp
set<pair<int,int>> s;
```

➡️ Automatically sorted like vector pair

---

# 🔹 7. CP Tricks (IMPORTANT)

## 🔸 Trick 1: Frequency sorting

```cpp
vector<int> arr = {1,1,2,3,3,3};

map<int,int> freq;
for(int x : arr) freq[x]++;

vector<pair<int,int>> v(freq.begin(), freq.end());

sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

## 🔸 Trick 2: Index + value sorting

```cpp
vector<int> a = {50, 10, 40};

vector<pair<int,int>> v;
for(int i=0;i<a.size();i++){
    v.push_back({a[i], i});
}

sort(v.begin(), v.end());
```

---

## 🔸 Trick 3: Stable sorting (VERY USEFUL)

```cpp
stable_sort(v.begin(), v.end(), cmp);
```

➡️ Keeps original order if equal

---

## 🔸 Trick 4: Reverse after sort

```cpp
sort(v.begin(), v.end());
reverse(v.begin(), v.end());
```

---

## 🔸 Trick 5: Sort only part

```cpp
sort(v.begin()+l, v.begin()+r);
```

---

## 🔸 Trick 6: Custom struct sorting (Advanced CP)

```cpp
struct Node {
    int x, y;
};

bool cmp(Node a, Node b){
    return a.x < b.x;
}

sort(v.begin(), v.end(), cmp);
```

---

# 🔹 8. Most Used CP Patterns (MEMORIZE)

### ⭐ Pattern 1: Sort by value descending

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

### ⭐ Pattern 2: Sort by first asc, second desc

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    if(a.first == b.first)
        return a.second > b.second;
    return a.first < b.first;
});
```

---

### ⭐ Pattern 3: Sort array in descending

```cpp
sort(a.rbegin(), a.rend());
```

---

# 🔥 Final CP Advice

In competitive programming:

* ❗ 70% problems → use `vector<pair<>> + sort`
* ❗ `map` → use for counting
* ❗ Convert to vector → then sort
* ❗ Learn **lambda functions** deeply

---

If you want next level 🚀
I can show you:

* Top 20 sorting problems (LeetCode + Codeforces style)
* Or give you a **CP template** with all comparators ready

Just tell me 👍
Good — this is exactly what strong CP coders do: **keep a ready template** so you don’t rewrite comparators in contests.

Below is a **clean, reusable CP template** with the most useful sorting patterns.

---

# 🚀 🔥 CP SORTING TEMPLATE (Copy-Paste Ready)

```cpp
#include <bits/stdc++.h>
using namespace std;

#define fast ios::sync_with_stdio(false); cin.tie(NULL);
#define ll long long
#define pii pair<int,int>
#define vi vector<int>
#define vpii vector<pair<int,int>>

/* ===================== BASIC COMPARATORS ===================== */

// sort by first ascending, second ascending (default)
bool cmp_default(pii a, pii b){
    if(a.first == b.first)
        return a.second < b.second;
    return a.first < b.first;
}

// sort by first ascending, second descending
bool cmp_first_asc_second_desc(pii a, pii b){
    if(a.first == b.first)
        return a.second > b.second;
    return a.first < b.first;
}

// sort by first descending, second ascending
bool cmp_first_desc_second_asc(pii a, pii b){
    if(a.first == b.first)
        return a.second < b.second;
    return a.first > b.first;
}

// sort by second ascending
bool cmp_second_asc(pii a, pii b){
    return a.second < b.second;
}

// sort by second descending
bool cmp_second_desc(pii a, pii b){
    return a.second > b.second;
}

// sort by sum of pair
bool cmp_sum(pii a, pii b){
    return (a.first + a.second) < (b.first + b.second);
}

// custom: even first, then odd
bool cmp_even_first(int a, int b){
    if(a % 2 == b % 2)
        return a < b;
    return (a % 2 == 0);
}


/* ===================== STRUCT SORT ===================== */

struct Node {
    int x, y;
};

// sort struct by x ascending
bool cmp_node_x(Node a, Node b){
    return a.x < b.x;
}

// sort struct by y descending
bool cmp_node_y_desc(Node a, Node b){
    return a.y > b.y;
}


/* ===================== LAMBDA SHORTCUTS ===================== */

// Example:
// sort(v.begin(), v.end(), [](auto a, auto b){
//     return a.second > b.second;
// });


/* ===================== UTILITY FUNCTIONS ===================== */

// print vector
template<typename T>
void print(vector<T> &v){
    for(auto x : v) cout << x << " ";
    cout << "\n";
}

// print pair vector
void print_pair(vector<pii> &v){
    for(auto [x,y] : v){
        cout << x << " " << y << "\n";
    }
}


/* ===================== MAIN ===================== */

int main(){
    fast;

    /* -------- vector<int> sorting -------- */
    vi a = {5,2,9,1};

    sort(a.begin(), a.end());          // ascending
    sort(a.rbegin(), a.rend());        // descending

    /* -------- vector<pair<int,int>> -------- */
    vpii v = {{2,3}, {1,5}, {2,1}};

    sort(v.begin(), v.end()); // default
    sort(v.begin(), v.end(), cmp_second_desc);
    sort(v.begin(), v.end(), cmp_first_asc_second_desc);

    /* -------- map sorting -------- */
    map<string,int> mp = {{"a",5}, {"c",2}, {"b",8}};

    vector<pair<string,int>> temp(mp.begin(), mp.end());

    // sort by value descending
    sort(temp.begin(), temp.end(), [](auto a, auto b){
        return a.second > b.second;
    });

    /* -------- frequency sort -------- */
    vi arr = {1,1,2,3,3,3};

    map<int,int> freq;
    for(int x : arr) freq[x]++;

    vector<pii> fv(freq.begin(), freq.end());

    sort(fv.begin(), fv.end(), cmp_second_desc);

    /* -------- partial sort -------- */
    sort(a.begin(), a.begin()+2);

    /* -------- stable sort -------- */
    stable_sort(v.begin(), v.end(), cmp_second_asc);

    return 0;
}
```

---

# 🧠 🔥 How to Use in Contest (Important)

Instead of remembering everything:

### ✅ Just remember these 3 patterns

**1. Value descending (MOST COMMON)**

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    return a.second > b.second;
});
```

---

**2. First asc, second desc**

```cpp
sort(v.begin(), v.end(), [](auto a, auto b){
    if(a.first == b.first)
        return a.second > b.second;
    return a.first < b.first;
});
```

---

**3. Simple descending**

```cpp
sort(v.rbegin(), v.rend());
```

---

# ⚡ Pro CP Tips

* Use **lambda** → faster to write in contests
* Use **vector<pair> instead of map** when sorting needed
* Use **stable_sort** when order matters
* Avoid overcomplicated comparators → bugs happen

---

If you want next level 🔥
I can give you:

* 💯 “Top 20 sorting tricks” used in Codeforces
* 🧩 Real contest problems where these comparators are used
* ⚔️ Practice set to master sorting in 2 days

Just tell me 👍
