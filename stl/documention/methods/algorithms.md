# STL `<algorithm>` & `<numeric>` — Complete Reference

> All functions use iterator pairs as range. Functions marked `📦 <numeric>` require `#include <numeric>`.

---

## 1. Sorting

| Function | Description |
|---|---|
| `sort` | Sorts in ascending order (or custom comparator) |
| `stable_sort` | Sort preserving relative order of equal elements |
| `partial_sort` | Sorts only first N elements |
| `nth_element` | Places correct element at nth position |
| `is_sorted` | Returns `true` if range is sorted |
| `is_sorted_until` | Iterator to first unsorted element |

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v{5, 2, 8, 1, 9, 3};

// sort
sort(v.begin(), v.end());
// v → {1, 2, 3, 5, 8, 9}

// stable_sort
stable_sort(v.begin(), v.end(), greater<int>());
// v → {9, 8, 5, 3, 2, 1}  (equal elements keep relative order)

// partial_sort — only first 3 sorted
partial_sort(v.begin(), v.begin() + 3, v.end());
// v → {1, 2, 3, 9, 8, 5}

// nth_element — v[2] = 3rd smallest
nth_element(v.begin(), v.begin() + 2, v.end());
// v[2] == 3

// is_sorted
bool ok = is_sorted(v.begin(), v.end());
// ok == true

// is_sorted_until
vector<int> u{1, 2, 5, 3, 4};
auto it = is_sorted_until(u.begin(), u.end());
// *it == 3
```

---

## 2. Searching

| Function | Description |
|---|---|
| `find` | First occurrence of value |
| `find_if` | First element satisfying predicate |
| `find_if_not` | First element NOT satisfying predicate |
| `binary_search` | Returns `true` if value exists (sorted range) |
| `lower_bound` | Iterator to first element `>=` value |
| `upper_bound` | Iterator to first element `>` value |
| `equal_range` | Pair of `[lower_bound, upper_bound]` |
| `search` | Finds a subsequence inside a range |
| `adjacent_find` | First pair of adjacent equal elements |

```cpp
vector<int> v{1, 2, 3, 4, 5};

// find
auto it = find(v.begin(), v.end(), 3);
// *it == 3

// find_if
auto it2 = find_if(v.begin(), v.end(), [](int x){ return x > 3; });
// *it2 == 4

// find_if_not
auto it3 = find_if_not(v.begin(), v.end(), [](int x){ return x < 4; });
// *it3 == 4

// binary_search (requires sorted range)
bool found = binary_search(v.begin(), v.end(), 3);
// found == true

// lower_bound
auto lo = lower_bound(v.begin(), v.end(), 3);
// *lo == 3

// upper_bound
auto hi = upper_bound(v.begin(), v.end(), 3);
// *hi == 4

// equal_range
auto [low, high] = equal_range(v.begin(), v.end(), 3);
// *low == 3, *high == 4

// search (find subsequence)
vector<int> sub{3, 4};
auto pos = search(v.begin(), v.end(), sub.begin(), sub.end());
// *pos == 3

// adjacent_find
vector<int> w{1, 2, 2, 3};
auto adj = adjacent_find(w.begin(), w.end());
// *adj == 2
```

---

## 3. Counting

| Function | Description |
|---|---|
| `count` | Count elements equal to value |
| `count_if` | Count elements satisfying predicate |

```cpp
vector<int> v{1, 2, 3, 2, 1};

// count
int n = count(v.begin(), v.end(), 2);
// n == 2

// count_if
int evens = count_if(v.begin(), v.end(), [](int x){ return x % 2 == 0; });
// evens == 2
```

---

## 4. Modifying Algorithms

| Function | Description |
|---|---|
| `copy` | Copy range to another |
| `copy_if` | Copy elements satisfying predicate |
| `copy_backward` | Copy range starting from the end |
| `move` | Move elements to destination range |
| `transform` | Apply function, store result |
| `fill` | Assign value to every element |
| `fill_n` | Assign value to first N elements |
| `generate` | Fill with generator function |
| `replace` | Replace all old_val with new_val |
| `replace_if` | Replace elements satisfying predicate |
| `remove` | Logically remove elements equal to value |
| `remove_if` | Logically remove elements by predicate |
| `unique` | Remove consecutive duplicates |
| `reverse` | Reverse a range |
| `rotate` | Rotate elements left |
| `shuffle` | Randomly shuffle elements |
| `sample` | Pick N random elements (C++17) |
| `for_each` | Apply function for side effects |
| `swap_ranges` | Swap two ranges element-wise |
| `merge` | Merge two sorted ranges |
| `inplace_merge` | Merge two consecutive sorted sub-ranges |

```cpp
vector<int> v{1, 2, 3, 4, 5};

// copy
vector<int> dst(5);
copy(v.begin(), v.end(), dst.begin());
// dst == {1,2,3,4,5}

// copy_if
vector<int> out;
copy_if(v.begin(), v.end(), back_inserter(out), [](int x){ return x > 2; });
// out == {3,4,5}

// copy_backward
vector<int> b{1,2,3,4,5};
copy_backward(b.begin(), b.begin()+3, b.end());
// b == {1,2,1,2,3}

// transform
vector<int> sq(5);
transform(v.begin(), v.end(), sq.begin(), [](int x){ return x * x; });
// sq == {1,4,9,16,25}

// fill
vector<int> f(5);
fill(f.begin(), f.end(), 7);
// f == {7,7,7,7,7}

// fill_n
fill_n(f.begin(), 3, 0);
// f == {0,0,0,7,7}

// generate
int i = 0;
vector<int> g(5);
generate(g.begin(), g.end(), [&]{ return i++; });
// g == {0,1,2,3,4}

// replace
vector<int> r{1,2,3,2,1};
replace(r.begin(), r.end(), 2, 99);
// r == {1,99,3,99,1}

// replace_if
replace_if(r.begin(), r.end(), [](int x){ return x < 3; }, 0);
// 1s → 0

// remove + erase idiom
vector<int> rm{1,2,3,2,1};
rm.erase(remove(rm.begin(), rm.end(), 2), rm.end());
// rm == {1,3,1}

// remove_if
rm.erase(remove_if(rm.begin(), rm.end(), [](int x){ return x % 2 != 0; }), rm.end());
// removes odds

// unique (sort first for global dedup)
vector<int> u{1,1,2,3,3,3,4};
u.erase(unique(u.begin(), u.end()), u.end());
// u == {1,2,3,4}

// reverse
reverse(v.begin(), v.end());
// v == {5,4,3,2,1}

// rotate (bring v[2] to front)
vector<int> rot{1,2,3,4,5};
rotate(rot.begin(), rot.begin()+2, rot.end());
// rot == {3,4,5,1,2}

// shuffle
mt19937 rng(42);
shuffle(v.begin(), v.end(), rng);
// v → random order

// for_each
for_each(v.begin(), v.end(), [](int x){ cout << x << ' '; });

// swap_ranges
vector<int> a{1,2,3}, bb{4,5,6};
swap_ranges(a.begin(), a.end(), bb.begin());
// a=={4,5,6}, bb=={1,2,3}

// merge
vector<int> m1{1,3,5}, m2{2,4,6}, merged;
merge(m1.begin(),m1.end(), m2.begin(),m2.end(), back_inserter(merged));
// merged == {1,2,3,4,5,6}

// inplace_merge
vector<int> ip{1,3,5,2,4,6};
inplace_merge(ip.begin(), ip.begin()+3, ip.end());
// ip == {1,2,3,4,5,6}

// sample (C++17)
vector<int> smp;
sample(v.begin(), v.end(), back_inserter(smp), 3, rng);
// smp == 3 random elements
```

---

## 5. Logical / Comparison

| Function | Description |
|---|---|
| `all_of` | `true` if ALL elements satisfy predicate |
| `any_of` | `true` if ANY element satisfies predicate |
| `none_of` | `true` if NO element satisfies predicate |
| `equal` | `true` if two ranges are element-wise equal |
| `mismatch` | Iterators to first mismatch in two ranges |
| `lexicographical_compare` | `true` if first range is lex-less |

```cpp
vector<int> v{2, 4, 6, 8};

bool allEven  = all_of(v.begin(),  v.end(), [](int x){ return x%2==0; }); // true
bool anyOver5 = any_of(v.begin(),  v.end(), [](int x){ return x>5;    }); // true
bool noNeg    = none_of(v.begin(), v.end(), [](int x){ return x<0;    }); // true

vector<int> a{1,2,3}, b{1,9,3};
bool eq = equal(a.begin(), a.end(), b.begin());
// eq == false

auto [ia, ib] = mismatch(a.begin(), a.end(), b.begin());
// *ia == 2, *ib == 9

bool less = lexicographical_compare(a.begin(), a.end(), b.begin(), b.end());
// true because 2 < 9 at position 1
```

---

## 6. Partitioning

| Function | Description |
|---|---|
| `partition` | Elements satisfying predicate come first |
| `stable_partition` | Like partition, preserves relative order |
| `partition_point` | Iterator to start of second partition |
| `is_partitioned` | `true` if range is partitioned by predicate |

```cpp
vector<int> v{1,2,3,4,5};

// partition
partition(v.begin(), v.end(), [](int x){ return x%2==0; });
// evens first: {2,4,1,3,5} (order not guaranteed)

// stable_partition
stable_partition(v.begin(), v.end(), [](int x){ return x%2==0; });
// evens first, order preserved: {2,4,1,3,5}

// partition_point
auto pp = partition_point(v.begin(), v.end(), [](int x){ return x%2==0; });
// pp points to first odd

// is_partitioned
bool ok = is_partitioned(v.begin(), v.end(), [](int x){ return x%2==0; });
// ok == true
```

---

## 7. Permutations

| Function | Description |
|---|---|
| `next_permutation` | Transform to next lex permutation |
| `prev_permutation` | Transform to previous lex permutation |
| `is_permutation` | `true` if one range is a permutation of another |

```cpp
string s = "abc";

next_permutation(s.begin(), s.end());
// s == "acb"

prev_permutation(s.begin(), s.end());
// s == "abc"  (back to original)

vector<int> a{1,2,3}, b{3,1,2};
bool ok = is_permutation(a.begin(), a.end(), b.begin());
// ok == true
```

---

## 8. Min / Max

| Function | Description |
|---|---|
| `min` | Smaller of two values |
| `max` | Larger of two values |
| `minmax` | Pair `{min, max}` of two values |
| `min_element` | Iterator to smallest in range |
| `max_element` | Iterator to largest in range |
| `minmax_element` | Pair of iterators to min and max |
| `clamp` | Clamp value between `[lo, hi]` |

```cpp
int a = min(3, 7);           // 3
int b = max(3, 7);           // 7
auto [lo, hi] = minmax(3,7); // {3, 7}

vector<int> v{3,1,4,1,5,9};
auto mn = min_element(v.begin(), v.end()); // *mn == 1
auto mx = max_element(v.begin(), v.end()); // *mx == 9
auto [mnIt, mxIt] = minmax_element(v.begin(), v.end());

int clamped = clamp(10, 1, 5); // 5  (clamped to max bound)
```

---

## 9. Set Operations *(requires sorted input)*

| Function | Description |
|---|---|
| `set_union` | Elements in A ∪ B |
| `set_intersection` | Elements in A ∩ B |
| `set_difference` | Elements in A but not B |
| `set_symmetric_difference` | Elements in exactly one of A or B |
| `includes` | `true` if B is a subset of A |

```cpp
vector<int> a{1,2,3}, b{2,3,4}, out;

set_union(a.begin(),a.end(), b.begin(),b.end(), back_inserter(out));
// out == {1,2,3,4}

out.clear();
set_intersection(a.begin(),a.end(), b.begin(),b.end(), back_inserter(out));
// out == {2,3}

out.clear();
set_difference(a.begin(),a.end(), b.begin(),b.end(), back_inserter(out));
// out == {1}

out.clear();
set_symmetric_difference(a.begin(),a.end(), b.begin(),b.end(), back_inserter(out));
// out == {1,4}

bool sub = includes(a.begin(),a.end(), b.begin(),b.end());
// false — {2,3,4} is not a subset of {1,2,3}
```

---

## 10. Heap Operations

| Function | Description |
|---|---|
| `make_heap` | Rearrange range into a max-heap |
| `push_heap` | Insert new element into heap |
| `pop_heap` | Move max to end (call `pop_back` to remove) |
| `sort_heap` | Sort a heap into ascending order |
| `is_heap` | `true` if range satisfies heap property |
| `is_heap_until` | Iterator to first element violating heap |

```cpp
vector<int> v{3,1,4,1,5,9};

make_heap(v.begin(), v.end());
// v[0] == 9  (max at front)

v.push_back(7);
push_heap(v.begin(), v.end());
// heap property maintained with 7 inserted

pop_heap(v.begin(), v.end());
v.pop_back();
// 9 removed

bool ok = is_heap(v.begin(), v.end());
// ok == true

auto it = is_heap_until(v.begin(), v.end());
// it points to first element breaking heap

sort_heap(v.begin(), v.end());
// v now sorted ascending
```

---

## 11. Numeric Algorithms 📦 `<numeric>`

| Function | Description |
|---|---|
| `accumulate` | Sum (or custom fold) of a range |
| `iota` | Fill with incrementing sequence |
| `inner_product` | Dot product of two ranges |
| `partial_sum` | Prefix sums |
| `adjacent_difference` | Differences of adjacent elements |
| `reduce` | Like accumulate but parallelizable (C++17) |
| `exclusive_scan` | Exclusive prefix sum (C++17) |
| `inclusive_scan` | Inclusive prefix sum (C++17) |
| `gcd` | Greatest common divisor |
| `lcm` | Least common multiple |

```cpp
#include <numeric>

vector<int> v{1,2,3,4,5};

// accumulate
int sum = accumulate(v.begin(), v.end(), 0);
// sum == 15

// product via accumulate
int prod = accumulate(v.begin(), v.end(), 1, multiplies<int>());
// prod == 120

// iota
vector<int> seq(5);
iota(seq.begin(), seq.end(), 1);
// seq == {1,2,3,4,5}

// inner_product (dot product)
vector<int> a{1,2,3}, b{4,5,6};
int dot = inner_product(a.begin(), a.end(), b.begin(), 0);
// 1*4 + 2*5 + 3*6 == 32

// partial_sum
vector<int> ps(5);
partial_sum(v.begin(), v.end(), ps.begin());
// ps == {1,3,6,10,15}

// adjacent_difference
vector<int> ad(5);
adjacent_difference(v.begin(), v.end(), ad.begin());
// ad == {1,1,1,1,1}

// reduce (C++17, parallelizable)
int r = reduce(v.begin(), v.end(), 0);
// r == 15

// exclusive_scan (C++17)
vector<int> es(5);
exclusive_scan(v.begin(), v.end(), es.begin(), 0);
// es == {0,1,3,6,10}

// inclusive_scan (C++17)
vector<int> is_(5);
inclusive_scan(v.begin(), v.end(), is_.begin());
// is_ == {1,3,6,10,15}

// gcd / lcm
int g = gcd(12, 18); // 6
int l = lcm(4,  6);  // 12
```

---

## Quick Summary Table

| Category | Header | Key Functions |
|---|---|---|
| Sorting | `<algorithm>` | `sort`, `stable_sort`, `partial_sort`, `nth_element` |
| Searching | `<algorithm>` | `find`, `binary_search`, `lower_bound`, `upper_bound` |
| Counting | `<algorithm>` | `count`, `count_if` |
| Modifying | `<algorithm>` | `copy`, `transform`, `fill`, `replace`, `remove`, `reverse`, `rotate` |
| Logical | `<algorithm>` | `all_of`, `any_of`, `none_of`, `equal`, `mismatch` |
| Partitioning | `<algorithm>` | `partition`, `stable_partition`, `partition_point` |
| Permutations | `<algorithm>` | `next_permutation`, `prev_permutation`, `is_permutation` |
| Min/Max | `<algorithm>` | `min`, `max`, `clamp`, `min_element`, `max_element` |
| Set ops | `<algorithm>` | `set_union`, `set_intersection`, `set_difference` |
| Heap | `<algorithm>` | `make_heap`, `push_heap`, `pop_heap`, `sort_heap` |
| Numeric | `<numeric>` | `accumulate`, `iota`, `partial_sum`, `gcd`, `lcm` |
