Here’s a **full A to Z guide to the C++ STL (Standard Template Library)** with **concepts, syntax, examples, and real use cases**.

---

# C++ STL Library — Full Detailed Guide

## 1. What is STL?

**STL** means **Standard Template Library**.
It is a built-in C++ library that gives you ready-made, reusable data structures and algorithms.

Instead of writing everything from scratch, STL lets you use:

* dynamic arrays
* linked lists
* stacks
* queues
* sets
* maps
* sorting
* searching
* useful helper tools

It saves time and makes code cleaner and faster.

---

# 2. Main Parts of STL

STL has 4 major parts:

## A. Containers

These store data.

Examples:

* `vector`
* `list`
* `deque`
* `stack`
* `queue`
* `priority_queue`
* `set`
* `multiset`
* `map`
* `multimap`
* `unordered_set`
* `unordered_map`

---

## B. Algorithms

These perform operations on data.

Examples:

* `sort()`
* `reverse()`
* `find()`
* `count()`
* `binary_search()`
* `max_element()`
* `min_element()`

---

## C. Iterators

These help move through elements of containers.

Examples:

* `begin()`
* `end()`
* `rbegin()`
* `rend()`

---

## D. Function Objects / Utilities

Helper tools like:

* `pair`
* `greater`
* `swap`
* `min`
* `max`

---

# 3. Why STL is Important

## Benefits

* faster coding
* less bugs
* optimized implementation
* easy to read
* useful in competitive programming
* useful in interviews
* useful in real projects

---

# 4. Header Files

Common headers:

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <deque>
#include <stack>
#include <queue>
#include <set>
#include <map>
#include <unordered_set>
#include <unordered_map>
#include <algorithm>
#include <iterator>
#include <utility>
#include <string>
using namespace std;
```

In competitive programming many use:

```cpp
#include <bits/stdc++.h>
using namespace std;
```

This includes almost everything, but for production code, specific headers are better.

---

# 5. Containers in STL

Containers are mainly 3 types:

## 1. Sequence Containers

Store elements in order.

* `vector`
* `list`
* `deque`
* `array`
* `forward_list`

## 2. Associative Containers

Store sorted unique or repeated keys.

* `set`
* `multiset`
* `map`
* `multimap`

## 3. Unordered Associative Containers

Store data using hash table.

* `unordered_set`
* `unordered_map`
* `unordered_multiset`
* `unordered_multimap`

## 4. Container Adaptors

Built using other containers.

* `stack`
* `queue`
* `priority_queue`

---

# 6. vector

## What is vector?

A `vector` is a dynamic array.
It can grow or shrink automatically.

## Why use vector?

* most commonly used STL container
* fast random access
* easy insertion at end
* great replacement for arrays in most cases

## Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;

    v.push_back(10);
    v.push_back(20);
    v.push_back(30);

    cout << v[0] << "\n";
    cout << v[1] << "\n";
    cout << v[2] << "\n";

    return 0;
}
```

## Output

```cpp
10
20
30
```

---

## Common vector functions

### `push_back()`

Adds element at end.

```cpp
v.push_back(5);
```

### `pop_back()`

Removes last element.

```cpp
v.pop_back();
```

### `size()`

Returns number of elements.

```cpp
cout << v.size();
```

### `empty()`

Checks if vector is empty.

```cpp
if (v.empty()) cout << "Empty";
```

### `clear()`

Removes all elements.

```cpp
v.clear();
```

### `front()` and `back()`

First and last element.

```cpp
cout << v.front();
cout << v.back();
```

### `at()`

Safer access than `[]`

```cpp
cout << v.at(1);
```

### `insert()`

Insert at position.

```cpp
v.insert(v.begin() + 1, 100);
```

### `erase()`

Remove element or range.

```cpp
v.erase(v.begin() + 2);
v.erase(v.begin(), v.begin() + 2);
```

### `resize()`

Change size.

```cpp
v.resize(5);
```

### `sort()`

Sort vector.

```cpp
sort(v.begin(), v.end());
```

---

## Full vector example

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {4, 2, 8, 1, 5};

    v.push_back(10);
    v.pop_back();

    sort(v.begin(), v.end());

    for (int x : v) {
        cout << x << " ";
    }

    return 0;
}
```

## Output

```cpp
1 2 4 5 8
```

---

## Use cases of vector

* storing student marks
* storing graph adjacency list
* storing dynamic input data
* competitive programming problems

---

# 7. array

## What is `array`?

Fixed-size array from STL.

```cpp
#include <array>
#include <iostream>
using namespace std;

int main() {
    array<int, 5> arr = {1, 2, 3, 4, 5};

    for (int x : arr) {
        cout << x << " ";
    }
}
```

## Use cases

* when size is fixed
* safer than normal C-style arrays

---

# 8. deque

## What is deque?

Double-ended queue.
Insertion/removal from both front and back is efficient.

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> dq;

    dq.push_back(10);
    dq.push_front(20);
    dq.push_back(30);

    for (int x : dq) {
        cout << x << " ";
    }
}
```

## Output

```cpp
20 10 30
```

## Important functions

* `push_back()`
* `push_front()`
* `pop_back()`
* `pop_front()`
* `front()`
* `back()`

## Use cases

* sliding window problems
* implementing queues
* when both-end operations are needed

---

# 9. list

## What is list?

Doubly linked list.

```cpp
#include <iostream>
#include <list>
using namespace std;

int main() {
    list<int> li = {10, 20, 30};

    li.push_front(5);
    li.push_back(40);

    for (int x : li) {
        cout << x << " ";
    }
}
```

## Output

```cpp
5 10 20 30 40
```

## Important functions

* `push_back()`
* `push_front()`
* `pop_back()`
* `pop_front()`
* `insert()`
* `erase()`
* `remove()`
* `sort()`
* `reverse()`

## Use cases

* frequent insert/delete in middle
* implementing custom linked-list style operations

## Note

Random access like `li[2]` is not allowed.

---

# 10. forward_list

Singly linked list.

```cpp
#include <iostream>
#include <forward_list>
using namespace std;

int main() {
    forward_list<int> fl = {1, 2, 3};
    fl.push_front(0);

    for (int x : fl) cout << x << " ";
}
```

## Use case

* memory-efficient linked list
* only forward traversal needed

---

# 11. stack

## What is stack?

LIFO = Last In First Out

Example from real life:

* stack of plates
* undo operations

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> st;

    st.push(10);
    st.push(20);
    st.push(30);

    cout << st.top() << "\n"; // 30

    st.pop();
    cout << st.top() << "\n"; // 20
}
```

## Important functions

* `push()`
* `pop()`
* `top()`
* `empty()`
* `size()`

## Use cases

* undo/redo
* parentheses matching
* DFS
* browser history

---

# 12. queue

## What is queue?

FIFO = First In First Out

Real life:

* line of people
* printer queue

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> q;

    q.push(10);
    q.push(20);
    q.push(30);

    cout << q.front() << "\n"; // 10
    cout << q.back() << "\n";  // 30

    q.pop();
    cout << q.front() << "\n"; // 20
}
```

## Important functions

* `push()`
* `pop()`
* `front()`
* `back()`
* `empty()`
* `size()`

## Use cases

* BFS
* task scheduling
* customer service systems

---

# 13. priority_queue

## What is priority_queue?

By default, it is a **max heap**.
Largest element stays on top.

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    priority_queue<int> pq;

    pq.push(10);
    pq.push(50);
    pq.push(20);

    cout << pq.top() << "\n"; // 50
}
```

---

## Min heap

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int main() {
    priority_queue<int, vector<int>, greater<int>> pq;

    pq.push(10);
    pq.push(50);
    pq.push(20);

    cout << pq.top() << "\n"; // 10
}
```

## Use cases

* Dijkstra’s algorithm
* task priority systems
* top K elements
* scheduling

---

# 14. set

## What is set?

Stores **unique** elements in **sorted order**.

```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;

    s.insert(30);
    s.insert(10);
    s.insert(20);
    s.insert(10);

    for (int x : s) {
        cout << x << " ";
    }
}
```

## Output

```cpp
10 20 30
```

Note: duplicate `10` is ignored.

## Important functions

* `insert()`
* `erase()`
* `find()`
* `count()`
* `size()`
* `empty()`

## Use cases

* storing unique values
* duplicate removal
* ordered unique data

---

# 15. multiset

Like `set`, but duplicates are allowed.

```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    multiset<int> ms;

    ms.insert(10);
    ms.insert(10);
    ms.insert(20);

    for (int x : ms) cout << x << " ";
}
```

## Output

```cpp
10 10 20
```

## Use cases

* frequency-like ordered storage
* when duplicates matter

---

# 16. unordered_set

Stores unique values, but not sorted.
Uses hashing.

```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int main() {
    unordered_set<int> us = {30, 10, 20, 10};

    for (int x : us) cout << x << " ";
}
```

Order is not guaranteed.

## Use cases

* fast lookup
* membership check
* removing duplicates quickly

---

# 17. map

## What is map?

Stores data as **key-value pairs**.
Keys are unique and sorted.

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<string, int> mp;

    mp["Alice"] = 90;
    mp["Bob"] = 85;
    mp["Charlie"] = 95;

    cout << mp["Bob"] << "\n";

    for (auto p : mp) {
        cout << p.first << " " << p.second << "\n";
    }
}
```

## Output

```cpp
85
Alice 90
Bob 85
Charlie 95
```

## Important functions

* `insert()`
* `erase()`
* `find()`
* `count()`
* `size()`

## Use cases

* student marks by name
* dictionary
* frequency counting
* config storage

---

# 18. multimap

Like map, but duplicate keys allowed.

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    multimap<int, string> mm;

    mm.insert({1, "apple"});
    mm.insert({1, "banana"});
    mm.insert({2, "orange"});

    for (auto p : mm) {
        cout << p.first << " " << p.second << "\n";
    }
}
```

---

# 19. unordered_map

Hash table version of map.
Faster average access, but not sorted.

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<string, int> ump;

    ump["apple"] = 3;
    ump["banana"] = 5;

    cout << ump["apple"] << "\n";
}
```

## Use cases

* frequency count
* caching
* fast key lookup

---

# 20. pair

## What is pair?

Stores two values together.

```cpp
#include <iostream>
#include <utility>
using namespace std;

int main() {
    pair<string, int> p = {"Alice", 90};

    cout << p.first << " " << p.second << "\n";
}
```

## Use cases

* coordinates `(x, y)`
* key-value
* returning two values from function

---

# 21. Iterators

Iterators are like pointers used to access container elements.

## Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30};

    vector<int>::iterator it;

    for (it = v.begin(); it != v.end(); it++) {
        cout << *it << " ";
    }
}
```

---

## Common iterator functions

* `begin()`
* `end()`
* `rbegin()`
* `rend()`

### Reverse traversal

```cpp
for (auto it = v.rbegin(); it != v.rend(); it++) {
    cout << *it << " ";
}
```

---

# 22. Algorithms in STL

Now the most powerful part: **algorithms**

Need:

```cpp
#include <algorithm>
```

---

## 1. sort()

```cpp
vector<int> v = {4, 2, 8, 1};
sort(v.begin(), v.end());
```

Descending:

```cpp
sort(v.begin(), v.end(), greater<int>());
```

---

## 2. reverse()

```cpp
reverse(v.begin(), v.end());
```

---

## 3. find()

```cpp
auto it = find(v.begin(), v.end(), 8);

if (it != v.end()) {
    cout << "Found";
}
```

---

## 4. count()

```cpp
int c = count(v.begin(), v.end(), 2);
cout << c;
```

---

## 5. binary_search()

Works on sorted data.

```cpp
sort(v.begin(), v.end());

if (binary_search(v.begin(), v.end(), 8)) {
    cout << "Yes";
}
```

---

## 6. max_element() and min_element()

```cpp
cout << *max_element(v.begin(), v.end()) << "\n";
cout << *min_element(v.begin(), v.end()) << "\n";
```

---

## 7. accumulate()

Need:

```cpp
#include <numeric>
```

```cpp
vector<int> v = {1, 2, 3, 4};
int sum = accumulate(v.begin(), v.end(), 0);
cout << sum;
```

---

## 8. next_permutation()

```cpp
string s = "abc";
next_permutation(s.begin(), s.end());
cout << s; // acb
```

---

## 9. prev_permutation()

```cpp
string s = "cba";
prev_permutation(s.begin(), s.end());
cout << s;
```

---

## 10. lower_bound() and upper_bound()

Used on sorted data.

```cpp
vector<int> v = {1, 2, 2, 2, 5, 7};

auto lb = lower_bound(v.begin(), v.end(), 2);
auto ub = upper_bound(v.begin(), v.end(), 2);

cout << lb - v.begin() << "\n"; // first 2
cout << ub - v.begin() << "\n"; // first greater than 2
```

---

# 23. Useful numeric functions

Need:

```cpp
#include <numeric>
```

## gcd

```cpp
cout << gcd(12, 18); // 6
```

## lcm

```cpp
cout << lcm(12, 18); // 36
```

---

# 24. Lambda Functions with STL

Very useful for custom sorting.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<pair<int, int>> v = {{1, 5}, {2, 3}, {4, 1}};

    sort(v.begin(), v.end(), [](pair<int, int> a, pair<int, int> b) {
        return a.second < b.second;
    });

    for (auto p : v) {
        cout << p.first << " " << p.second << "\n";
    }
}
```

## Use case

* sort students by marks
* sort objects by custom rules

---

# 25. Comparison of Common STL Containers

## vector

* dynamic array
* fast random access
* fast push at end
* slow insert/delete in middle

## list

* fast insert/delete in middle
* slow random access

## deque

* fast insert/delete at both ends

## set

* sorted unique values

## unordered_set

* unique values, faster average lookup, no order

## map

* sorted key-value pairs

## unordered_map

* faster average key-value lookup, no order

---

# 26. Time Complexity Table

## vector

* access: `O(1)`
* push_back: `O(1)` average
* insert middle: `O(n)`
* erase middle: `O(n)`

## set / map

* insert: `O(log n)`
* search: `O(log n)`
* erase: `O(log n)`

## unordered_set / unordered_map

* insert: `O(1)` average
* search: `O(1)` average
* erase: `O(1)` average

## priority_queue

* push: `O(log n)`
* pop: `O(log n)`
* top: `O(1)`

---

# 27. Real-world and Problem-solving Use Cases

## A. Frequency counting

Use `map` or `unordered_map`

```cpp
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

int main() {
    string s = "banana";
    unordered_map<char, int> freq;

    for (char c : s) {
        freq[c]++;
    }

    for (auto p : freq) {
        cout << p.first << " -> " << p.second << "\n";
    }
}
```

---

## B. Remove duplicates

Use `set`

```cpp
vector<int> v = {1, 2, 2, 3, 4, 4};
set<int> s(v.begin(), v.end());

for (int x : s) cout << x << " ";
```

---

## C. Top K largest elements

Use `priority_queue`

```cpp
vector<int> v = {10, 4, 3, 50, 23, 90};

priority_queue<int> pq;

for (int x : v) pq.push(x);

int k = 3;
while (k--) {
    cout << pq.top() << " ";
    pq.pop();
}
```

---

## D. BFS in graph

Use `queue`

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

int main() {
    int n = 5;
    vector<vector<int>> graph(n);

    graph[0] = {1, 2};
    graph[1] = {0, 3};
    graph[2] = {0, 4};
    graph[3] = {1};
    graph[4] = {2};

    vector<bool> visited(n, false);
    queue<int> q;

    q.push(0);
    visited[0] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        cout << node << " ";

        for (int nei : graph[node]) {
            if (!visited[nei]) {
                visited[nei] = true;
                q.push(nei);
            }
        }
    }
}
```

---

## E. Dijkstra’s Algorithm

Use `priority_queue`

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

int main() {
    int n = 3;
    vector<vector<pair<int, int>>> graph(n);

    graph[0].push_back({1, 4});
    graph[0].push_back({2, 1});
    graph[2].push_back({1, 2});

    vector<int> dist(n, 1e9);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    dist[0] = 0;
    pq.push({0, 0});

    while (!pq.empty()) {
        auto [d, node] = pq.top();
        pq.pop();

        for (auto [nei, wt] : graph[node]) {
            if (d + wt < dist[nei]) {
                dist[nei] = d + wt;
                pq.push({dist[nei], nei});
            }
        }
    }

    for (int x : dist) cout << x << " ";
}
```

---

# 28. Common STL Interview Questions

## Difference between map and unordered_map?

* `map` is sorted
* `unordered_map` is not sorted
* `map` uses tree, `O(log n)`
* `unordered_map` uses hash table, average `O(1)`

## Difference between set and multiset?

* `set` stores unique elements
* `multiset` allows duplicates

## Difference between vector and array?

* `vector` dynamic size
* `array` fixed size

## Difference between list and vector?

* `vector` fast random access
* `list` fast insert/delete in middle

---

# 29. Common Mistakes

## 1. Using binary_search on unsorted data

Wrong:

```cpp
vector<int> v = {5, 1, 3};
binary_search(v.begin(), v.end(), 3); // wrong
```

Correct:

```cpp
sort(v.begin(), v.end());
binary_search(v.begin(), v.end(), 3);
```

---

## 2. Accessing empty container top/front/back

Wrong:

```cpp
stack<int> st;
cout << st.top();
```

Always check:

```cpp
if (!st.empty()) cout << st.top();
```

---

## 3. Iterator invalidation

For example, after `vector` insert or erase, old iterators may become invalid.

---

# 30. Most Important STL Containers to Master First

Learn these first:

1. `vector`
2. `pair`
3. `stack`
4. `queue`
5. `priority_queue`
6. `set`
7. `map`
8. `unordered_map`
9. `sort()`
10. `lower_bound()` and `upper_bound()`

These are enough for most coding interviews and competitive programming problems.

---

# 31. Full Combined Example

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {5, 2, 8, 2, 1, 9};

    sort(v.begin(), v.end());

    cout << "Sorted vector: ";
    for (int x : v) cout << x << " ";
    cout << "\n";

    set<int> s(v.begin(), v.end());
    cout << "Unique sorted values: ";
    for (int x : s) cout << x << " ";
    cout << "\n";

    unordered_map<int, int> freq;
    for (int x : v) freq[x]++;

    cout << "Frequency:\n";
    for (auto p : freq) {
        cout << p.first << " -> " << p.second << "\n";
    }

    priority_queue<int> pq;
    for (int x : v) pq.push(x);

    cout << "Max element from heap: " << pq.top() << "\n";

    return 0;
}
```

---

# 32. STL Learning Roadmap

## Step 1

Learn:

* `vector`
* loops
* iterators
* `pair`

## Step 2

Learn:

* `stack`
* `queue`
* `deque`
* `priority_queue`

## Step 3

Learn:

* `set`
* `multiset`
* `map`
* `unordered_map`

## Step 4

Learn algorithms:

* `sort`
* `find`
* `count`
* `binary_search`
* `lower_bound`
* `upper_bound`
* `max_element`
* `min_element`

## Step 5

Practice with:

* frequency counting
* graph problems
* sorting custom objects
* greedy problems
* heap problems

---

# 33. Final Advice

For most beginners, this is the best order:

* `vector`
* `string`
* `pair`
* `set`
* `map`
* `stack`
* `queue`
* `priority_queue`
* `sort`
* `lower_bound`
* `upper_bound`
* `unordered_map`

If you master these well, you can solve a huge number of problems.

---

# 34. Quick Cheat Sheet

## vector

```cpp
vector<int> v;
v.push_back(10);
v.pop_back();
v.size();
sort(v.begin(), v.end());
```

## set

```cpp
set<int> s;
s.insert(5);
s.erase(5);
s.find(5);
```

## map

```cpp
map<string, int> mp;
mp["a"] = 10;
cout << mp["a"];
```

## stack

```cpp
stack<int> st;
st.push(1);
st.pop();
st.top();
```

## queue

```cpp
queue<int> q;
q.push(1);
q.pop();
q.front();
```

## priority_queue

```cpp
priority_queue<int> pq;
pq.push(10);
pq.top();
```

---

I can also make this into a **clean exam note / PDF-style document**, or give you **50 STL practice problems from easy to advanced**.
