// ============================================================
//  STL CONTAINER EXAMPLES — One example per method per container
//  Compile: g++ -std=c++20 -o stl_examples stl_examples.cpp

// ============================================================
```cpp
#include <bits/stdc++.h>
using namespace std;

// Helper: print a container
template<typename C>
void print(const string& label, const C& c) {
    cout << label << ": [ ";
    for (const auto& x : c) cout << x << " ";
    cout << "]\n";
}
```
// ============================================================
//  1. VECTOR
// ============================================================

```cpp
void demo_vector() {
    cout << "\n===== VECTOR =====\n";

    vector<int> v;

    // push_back()
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);
    print("push_back 10,20,30", v);                         // [10 20 30]

    // emplace_back()
    v.emplace_back(40);
    print("emplace_back 40", v);                            // [10 20 30 40]

    // emplace(it, val)
    v.emplace(v.begin() + 1, 15);
    print("emplace at [1]=15", v);                          // [10 15 20 30 40]

    // insert(it, val)
    v.insert(v.begin() + 2, 18);
    print("insert at [2]=18", v);                           // [10 15 18 20 30 40]

    // insert(it, n, val)
    v.insert(v.end(), 2, 99);
    print("insert 2x99 at end", v);                         // [10 15 18 20 30 40 99 99]

    // insert(it, first, last)  — insert range
    vector<int> src = {50, 60};
    v.insert(v.begin(), src.begin(), src.end());
    print("insert range at front", v);                      // [50 60 10 15 18 20 30 40 99 99]

    // erase(it)
    v.erase(v.begin());
    print("erase first element", v);                        // [60 10 15 18 20 30 40 99 99]

    // erase(first, last)
    v.erase(v.end() - 2, v.end());
    print("erase last 2 elements", v);                      // [60 10 15 18 20 30 40]

    // pop_back()
    v.pop_back();
    print("pop_back", v);                                   // [60 10 15 18 20 30]

    // operator[]
    cout << "v[2] = " << v[2] << "\n";                      // 15

    // at()
    cout << "v.at(3) = " << v.at(3) << "\n";               // 18

    // front()
    cout << "front() = " << v.front() << "\n";              // 60

    // back()
    cout << "back() = " << v.back() << "\n";                // 30

    // size()
    cout << "size() = " << v.size() << "\n";                // 6

    // capacity()
    cout << "capacity() = " << v.capacity() << "\n";

    // max_size()
    cout << "max_size() = " << v.max_size() << "\n";

    // empty()
    cout << "empty() = " << v.empty() << "\n";              // 0 (false)

    // reserve()
    v.reserve(100);
    cout << "after reserve(100), capacity = " << v.capacity() << "\n";

    // shrink_to_fit()
    v.shrink_to_fit();
    cout << "after shrink_to_fit(), capacity = " << v.capacity() << "\n";

    // data()
    int* ptr = v.data();
    cout << "data()[0] = " << ptr[0] << "\n";               // 60

    // assign(n, val)
    vector<int> v2;
    v2.assign(4, 7);
    print("assign(4, 7)", v2);                              // [7 7 7 7]

    // assign(first, last)
    vector<int> v3;
    v3.assign(v.begin(), v.begin() + 3);
    print("assign from range", v3);

    // resize()
    v3.resize(6, 0);
    print("resize(6, 0)", v3);                              // pads with 0s

    // swap()
    vector<int> va = {1, 2}, vb = {9, 8, 7};
    va.swap(vb);
    print("va after swap", va);                             // [9 8 7]
    print("vb after swap", vb);                             // [1 2]

    // clear()
    va.clear();
    cout << "after clear(), size = " << va.size() << "\n";  // 0

    // begin() / end()
    vector<int> vi = {3, 1, 4, 1, 5};
    cout << "begin()=*it: " << *vi.begin() << "\n";         // 3

    // rbegin() / rend()
    cout << "rbegin()=*it: " << *vi.rbegin() << "\n";       // 5

    // cbegin() / cend() (const iterators)
    const vector<int> cv = {10, 20};
    cout << "cbegin(): " << *cv.cbegin() << "\n";           // 10
}
```
// ============================================================
//  2. DEQUE
// ============================================================


```cpp
void demo_deque() {
    cout << "\n===== DEQUE =====\n";

    deque<int> d;

    // push_back()
    d.push_back(30);
    d.push_back(40);
    print("push_back 30,40", d);                            // [30 40]

    // push_front()
    d.push_front(20);
    d.push_front(10);
    print("push_front 20,10", d);                           // [10 20 30 40]

    // emplace_back()
    d.emplace_back(50);
    print("emplace_back 50", d);                            // [10 20 30 40 50]

    // emplace_front()
    d.emplace_front(5);
    print("emplace_front 5", d);                            // [5 10 20 30 40 50]

    // emplace(it, val)
    d.emplace(d.begin() + 2, 15);
    print("emplace at [2]=15", d);                          // [5 10 15 20 30 40 50]

    // insert(it, val)
    d.insert(d.begin() + 1, 8);
    print("insert at [1]=8", d);                            // [5 8 10 15 20 30 40 50]

    // erase(it)
    d.erase(d.begin());
    print("erase first", d);                                // [8 10 15 20 30 40 50]

    // erase(first, last)
    d.erase(d.end() - 2, d.end());
    print("erase last 2", d);                               // [8 10 15 20 30]

    // pop_back()
    d.pop_back();
    print("pop_back", d);                                   // [8 10 15 20]

    // pop_front()
    d.pop_front();
    print("pop_front", d);                                  // [10 15 20]

    // operator[]
    cout << "d[1] = " << d[1] << "\n";                      // 15

    // at()
    cout << "d.at(2) = " << d.at(2) << "\n";               // 20

    // front() / back()
    cout << "front=" << d.front() << " back=" << d.back() << "\n";

    // size() / empty() / max_size()
    cout << "size=" << d.size() << " empty=" << d.empty() << "\n";

    // resize()
    d.resize(6, 99);
    print("resize(6,99)", d);                               // [10 15 20 99 99 99]

    // assign(n, val)
    d.assign(3, 1);
    print("assign(3,1)", d);                                // [1 1 1]

    // shrink_to_fit()
    d.shrink_to_fit();
    cout << "shrink_to_fit() called\n";

    // swap()
    deque<int> d2 = {7, 8};
    d.swap(d2);
    print("d after swap", d);                               // [7 8]

    // clear()
    d.clear();
    cout << "after clear(), size=" << d.size() << "\n";

    // begin/end, rbegin/rend
    deque<int> di = {1, 2, 3};
    cout << "*begin=" << *di.begin() << " *rbegin=" << *di.rbegin() << "\n";
}
```
// ============================================================
//  3. LIST
// ============================================================

```cpp
void demo_list() {
    cout << "\n===== LIST =====\n";

    list<int> L;

    // push_back()
    L.push_back(10);
    L.push_back(30);
    print("push_back 10,30", L);                            // [10 30]

    // push_front()
    L.push_front(5);
    print("push_front 5", L);                               // [5 10 30]

    // emplace_back()
    L.emplace_back(40);
    print("emplace_back 40", L);                            // [5 10 30 40]

    // emplace_front()
    L.emplace_front(1);
    print("emplace_front 1", L);                            // [1 5 10 30 40]

    // emplace(it, val)
    auto it = next(L.begin(), 2);
    L.emplace(it, 8);
    print("emplace at pos 2 = 8", L);                      // [1 5 8 10 30 40]

    // insert(it, val)
    L.insert(L.end(), 50);
    print("insert 50 at end", L);                           // [1 5 8 10 30 40 50]

    // erase(it)
    L.erase(L.begin());
    print("erase first", L);                                // [5 8 10 30 40 50]

    // pop_back()
    L.pop_back();
    print("pop_back", L);                                   // [5 8 10 30 40]

    // pop_front()
    L.pop_front();
    print("pop_front", L);                                  // [8 10 30 40]

    // front() / back()
    cout << "front=" << L.front() << " back=" << L.back() << "\n";

    // size() / empty()
    cout << "size=" << L.size() << " empty=" << L.empty() << "\n";

    // resize()
    L.resize(6, 0);
    print("resize(6,0)", L);                                // [8 10 30 40 0 0]

    // assign(n, val)
    L.assign(4, 3);
    print("assign(4,3)", L);                                // [3 3 3 3]

    // sort()
    list<int> ls = {5, 2, 8, 1, 9, 3};
    ls.sort();
    print("sort()", ls);                                    // [1 2 3 5 8 9]

    // sort(comparator)
    ls.sort(greater<int>());
    print("sort(greater)", ls);                             // [9 8 5 3 2 1]

    // reverse()
    ls.reverse();
    print("reverse()", ls);                                 // [1 2 3 5 8 9]

    // unique()  — removes consecutive duplicates
    list<int> lu = {1, 1, 2, 3, 3, 3, 4};
    lu.unique();
    print("unique()", lu);                                  // [1 2 3 4]

    // remove(val)
    list<int> lr = {1, 2, 3, 2, 4};
    lr.remove(2);
    print("remove(2)", lr);                                 // [1 3 4]

    // remove_if(pred)
    lr.remove_if([](int x){ return x > 2; });
    print("remove_if(>2)", lr);                             // [1]

    // merge()
    list<int> la = {1, 3, 5};
    list<int> lb = {2, 4, 6};
    la.merge(lb);
    print("merge()", la);                                   // [1 2 3 4 5 6]
    cout << "lb empty after merge: " << lb.empty() << "\n";

    // splice(it, other)  — move entire list
    list<int> lx = {10, 20};
    list<int> ly = {30, 40};
    lx.splice(lx.end(), ly);
    print("splice(end, ly)", lx);                           // [10 20 30 40]

    // splice(it, other, other_it)  — move one element
    list<int> lp = {1, 2, 3};
    list<int> lq = {7, 8, 9};
    lp.splice(lp.begin(), lq, next(lq.begin()));
    print("splice one element (8) into lp", lp);           // [8 1 2 3]

    // swap()
    list<int> l1 = {1, 2}, l2 = {9};
    l1.swap(l2);
    print("l1 after swap", l1);                            // [9]

    // clear()
    l1.clear();
    cout << "after clear(), size=" << l1.size() << "\n";

    // begin/end, rbegin/rend
    list<int> li = {10, 20, 30};
    cout << "*begin=" << *li.begin() << " *rbegin=" << *li.rbegin() << "\n";

    // max_size()
    cout << "max_size=" << li.max_size() << "\n";
}
```

// ============================================================
//  4. FORWARD_LIST
// ============================================================

```cpp
void demo_forward_list() {
    cout << "\n===== FORWARD_LIST =====\n";

    forward_list<int> fl;

    // push_front()
    fl.push_front(30);
    fl.push_front(20);
    fl.push_front(10);
    print("push_front 10,20,30", fl);                       // [10 20 30]

    // emplace_front()
    fl.emplace_front(5);
    print("emplace_front 5", fl);                           // [5 10 20 30]

    // insert_after(it, val)
    fl.insert_after(fl.begin(), 8);
    print("insert_after begin = 8", fl);                    // [5 8 10 20 30]

    // insert_after(it, n, val)
    fl.insert_after(fl.before_begin(), 2, 0);
    print("insert_after before_begin 2x0", fl);             // [0 0 5 8 10 20 30]

    // emplace_after(it, val)
    fl.emplace_after(fl.begin(), 1);
    print("emplace_after begin = 1", fl);                   // [0 1 0 5 8 10 20 30]

    // erase_after(it)  — erase element AFTER it
    fl.erase_after(fl.begin());
    print("erase_after begin", fl);                         // [0 0 5 8 10 20 30]

    // erase_after(first, last)
    auto fit = fl.begin();
    advance(fit, 1);
    auto fit2 = fl.begin();
    advance(fit2, 4);
    fl.erase_after(fit, fit2);
    print("erase_after range", fl);                         // [0 0 10 20 30]

    // pop_front()
    fl.pop_front();
    print("pop_front", fl);                                 // [0 10 20 30]

    // front()
    cout << "front=" << fl.front() << "\n";                 // 0

    // before_begin()  — iterator before the first element
    fl.insert_after(fl.before_begin(), -1);
    print("insert via before_begin = -1", fl);              // [-1 0 10 20 30]

    // empty()
    cout << "empty=" << fl.empty() << "\n";

    // max_size()
    cout << "max_size=" << fl.max_size() << "\n";

    // assign(n, val)
    fl.assign(4, 2);
    print("assign(4,2)", fl);                               // [2 2 2 2]

    // resize()
    fl.resize(6, 9);
    print("resize(6,9)", fl);                               // [2 2 2 2 9 9]

    // sort()
    forward_list<int> fls = {5, 1, 4, 2, 3};
    fls.sort();
    print("sort()", fls);                                   // [1 2 3 4 5]

    // sort(comparator)
    fls.sort(greater<int>());
    print("sort(greater)", fls);                            // [5 4 3 2 1]

    // reverse()
    fls.reverse();
    print("reverse()", fls);                                // [1 2 3 4 5]

    // unique()
    forward_list<int> flu = {1, 1, 2, 2, 3};
    flu.unique();
    print("unique()", flu);                                 // [1 2 3]

    // remove(val)
    forward_list<int> flr = {1, 2, 3, 2};
    flr.remove(2);
    print("remove(2)", flr);                                // [1 3]

    // remove_if(pred)
    flr.remove_if([](int x){ return x > 1; });
    print("remove_if(>1)", flr);                            // [1]

    // merge()
    forward_list<int> fla = {1, 3, 5};
    forward_list<int> flb = {2, 4};
    fla.merge(flb);
    print("merge()", fla);                                  // [1 2 3 4 5]

    // splice_after(it, other)
    forward_list<int> flx = {1, 2};
    forward_list<int> fly = {3, 4};
    flx.splice_after(flx.begin(), fly);
    print("splice_after begin", flx);                       // [1 3 4 2]

    // swap()
    forward_list<int> fl1 = {10}, fl2 = {20, 30};
    fl1.swap(fl2);
    print("fl1 after swap", fl1);                           // [20 30]

    // clear()
    fl1.clear();
    cout << "after clear(), empty=" << fl1.empty() << "\n";

    // begin() / end()
    forward_list<int> fli = {1, 2, 3};
    cout << "*begin=" << *fli.begin() << "\n";
}
```
// ============================================================
//  5. ARRAY
// ============================================================


```cpp
void demo_array() {
    cout << "\n===== ARRAY =====\n";

    array<int, 5> a = {3, 1, 4, 1, 5};

    // operator[]
    cout << "a[2] = " << a[2] << "\n";                      // 4

    // at()
    cout << "a.at(4) = " << a.at(4) << "\n";               // 5

    // front()
    cout << "front() = " << a.front() << "\n";              // 3

    // back()
    cout << "back() = " << a.back() << "\n";                // 5

    // data()
    int* p = a.data();
    cout << "data()[0] = " << p[0] << "\n";                 // 3

    // size()
    cout << "size() = " << a.size() << "\n";                // 5

    // max_size()
    cout << "max_size() = " << a.max_size() << "\n";        // 5

    // empty()
    cout << "empty() = " << a.empty() << "\n";              // 0

    // fill(val)
    a.fill(0);
    print("fill(0)", a);                                     // [0 0 0 0 0]

    // swap()
    array<int, 5> b = {1, 2, 3, 4, 5};
    a.swap(b);
    print("a after swap", a);                               // [1 2 3 4 5]

    // begin() / end()
    cout << "*begin=" << *a.begin() << "\n";

    // rbegin() / rend()
    cout << "*rbegin=" << *a.rbegin() << "\n";              // 5

    // cbegin() / cend()
    cout << "*cbegin=" << *a.cbegin() << "\n";

    // std::get<N>()  — compile-time index access
    cout << "get<2>(a) = " << get<2>(a) << "\n";            // 3
}
```
// ============================================================
//  6. SET
// ============================================================
```cpp
void demo_set() {
    cout << "\n===== SET =====\n";

    set<int> s;

    // insert(val)
    s.insert(30);
    s.insert(10);
    s.insert(20);
    s.insert(10);  // duplicate — ignored
    print("insert 30,10,20,10(dup)", s);                    // [10 20 30]

    // emplace(val)
    s.emplace(25);
    print("emplace(25)", s);                                // [10 20 25 30]

    // erase(val)
    s.erase(10);
    print("erase(10)", s);                                  // [20 25 30]

    // erase(it)
    s.erase(s.begin());
    print("erase(begin)", s);                               // [25 30]

    // erase(first, last)
    set<int> s2 = {1, 2, 3, 4, 5};
    s2.erase(s2.begin(), next(s2.begin(), 2));
    print("erase range (first 2)", s2);                     // [3 4 5]

    // find(key)
    auto it = s2.find(4);
    cout << "find(4) = " << (it != s2.end() ? *it : -1) << "\n"; // 4

    // count(key)
    cout << "count(3) = " << s2.count(3) << "\n";           // 1

    // contains(key) [C++20]
    cout << "contains(5) = " << s2.contains(5) << "\n";    // 1

    // lower_bound(key)
    set<int> s3 = {10, 20, 30, 40};
    cout << "*lower_bound(25) = " << *s3.lower_bound(25) << "\n"; // 30

    // upper_bound(key)
    cout << "*upper_bound(20) = " << *s3.upper_bound(20) << "\n"; // 30

    // equal_range(key)
    auto [lo, hi] = s3.equal_range(20);
    cout << "equal_range(20): lo=" << *lo << " hi=" << *hi << "\n";

    // size() / empty() / max_size()
    cout << "size=" << s3.size() << " empty=" << s3.empty() << "\n";

    // clear()
    s3.clear();
    cout << "after clear(), size=" << s3.size() << "\n";

    // swap()
    set<int> sa = {1, 2}, sb = {7, 8, 9};
    sa.swap(sb);
    print("sa after swap", sa);                             // [7 8 9]

    // merge() [C++17]
    set<int> sm1 = {1, 3, 5};
    set<int> sm2 = {2, 4, 5};  // 5 already in sm1 — stays in sm2
    sm1.merge(sm2);
    print("sm1 after merge", sm1);                          // [1 2 3 4 5]
    print("sm2 leftover (5 not moved)", sm2);               // [5]

    // extract() [C++17]
    set<int> se = {10, 20, 30};
    auto node = se.extract(20);
    cout << "extracted node value = " << node.value() << "\n"; // 20
    print("se after extract(20)", se);                      // [10 30]

    // key_comp()
    auto cmp = se.key_comp();
    cout << "key_comp()(1,2) = " << cmp(1, 2) << "\n";     // 1 (true)

    // value_comp()  — same as key_comp for set
    auto vcmp = se.value_comp();
    cout << "value_comp()(1,2) = " << vcmp(1, 2) << "\n";  // 1

    // begin/end, rbegin/rend
    set<int> si = {5, 10, 15};
    cout << "*begin=" << *si.begin() << " *rbegin=" << *si.rbegin() << "\n";
}
```
// ============================================================
//  7. MULTISET
// ============================================================
```cpp
void demo_multiset() {
    cout << "\n===== MULTISET =====\n";

    multiset<int> ms;

    // insert()
    ms.insert(10);
    ms.insert(10);
    ms.insert(20);
    ms.insert(30);
    print("insert 10,10,20,30", ms);                        // [10 10 20 30]

    // emplace()
    ms.emplace(15);
    print("emplace(15)", ms);                               // [10 10 15 20 30]

    // erase(val) — removes ALL occurrences
    ms.erase(10);
    print("erase(10) removes both 10s", ms);                // [15 20 30]

    // erase(it) — removes just one
    multiset<int> ms2 = {5, 5, 5};
    ms2.erase(ms2.find(5));  // erase only one 5
    print("erase one 5", ms2);                              // [5 5]

    // find()
    auto it = ms.find(20);
    cout << "find(20) = " << (it != ms.end() ? *it : -1) << "\n"; // 20

    // count()  — can be > 1
    multiset<int> ms3 = {3, 3, 3, 4};
    cout << "count(3) = " << ms3.count(3) << "\n";          // 3

    // contains() [C++20]
    cout << "contains(4) = " << ms3.contains(4) << "\n";   // 1

    // lower_bound / upper_bound / equal_range
    multiset<int> ms4 = {10, 20, 20, 30};
    cout << "*lower_bound(20) = " << *ms4.lower_bound(20) << "\n"; // 20
    cout << "*upper_bound(20) = " << *ms4.upper_bound(20) << "\n"; // 30
    auto [lo, hi] = ms4.equal_range(20);
    cout << "equal_range(20) count = " << distance(lo, hi) << "\n"; // 2

    // size / empty / clear / swap / merge / extract — same as set
    cout << "size=" << ms4.size() << "\n";

    // key_comp() / value_comp()
    auto cmp = ms4.key_comp();
    cout << "key_comp()(10,20)=" << cmp(10, 20) << "\n";

    // begin/end, rbegin/rend
    cout << "*begin=" << *ms4.begin() << " *rbegin=" << *ms4.rbegin() << "\n";
}
```
// ============================================================
//  8. MAP
// ============================================================

```cpp
void demo_map() {
    cout << "\n===== MAP =====\n";

    map<string, int> m;

    // operator[] (insert if key missing)
    m["alice"] = 10;
    m["bob"]   = 20;
    m["carol"] = 30;
    cout << "m[\"alice\"] = " << m["alice"] << "\n";         // 10

    // at()
    cout << "m.at(\"bob\") = " << m.at("bob") << "\n";      // 20

    // insert({key,val})
    m.insert({"dave", 40});
    cout << "after insert dave=40, size=" << m.size() << "\n"; // 4

    // insert_or_assign(key, val) [C++17]
    m.insert_or_assign("alice", 99);
    cout << "insert_or_assign alice=99: " << m["alice"] << "\n"; // 99

    // emplace(key, val)
    m.emplace("eve", 50);
    cout << "emplace eve=50: " << m["eve"] << "\n";          // 50

    // try_emplace(key, val) [C++17] — only inserts if key absent
    m.try_emplace("alice", 999);  // alice exists — no change
    m.try_emplace("frank", 60);
    cout << "try_emplace alice (no change)=" << m["alice"] << "\n"; // 99
    cout << "try_emplace frank=60: " << m["frank"] << "\n";  // 60

    // erase(key)
    m.erase("frank");
    cout << "after erase frank, size=" << m.size() << "\n";

    // erase(it)
    m.erase(m.begin());
    cout << "after erase begin, size=" << m.size() << "\n";

    // find(key)
    auto it = m.find("dave");
    if (it != m.end())
        cout << "find(dave) -> " << it->second << "\n";      // 40

    // count(key)
    cout << "count(dave) = " << m.count("dave") << "\n";    // 1
    cout << "count(xyz)  = " << m.count("xyz")  << "\n";    // 0

    // contains(key) [C++20]
    cout << "contains(eve) = " << m.contains("eve") << "\n"; // 1

    // lower_bound / upper_bound / equal_range
    map<int,string> mi = {{1,"a"},{3,"c"},{5,"e"}};
    cout << "lower_bound(3)->first = " << mi.lower_bound(3)->first << "\n"; // 3
    cout << "upper_bound(3)->first = " << mi.upper_bound(3)->first << "\n"; // 5
    auto [lo, hi] = mi.equal_range(3);
    cout << "equal_range(3): " << lo->first << " to " << hi->first << "\n";

    // size / empty / max_size
    cout << "size=" << m.size() << " empty=" << m.empty() << "\n";

    // clear()
    map<int,int> mc = {{1,1},{2,2}};
    mc.clear();
    cout << "after clear(), size=" << mc.size() << "\n";

    // swap()
    map<int,int> ma = {{1,1}}, mb = {{9,9},{8,8}};
    ma.swap(mb);
    cout << "ma after swap, size=" << ma.size() << "\n";    // 2

    // merge() [C++17]
    map<int,int> mm1 = {{1,1},{3,3}};
    map<int,int> mm2 = {{2,2},{3,99}};  // key 3 already in mm1
    mm1.merge(mm2);
    cout << "mm1 after merge size=" << mm1.size() << "\n";  // 3
    cout << "mm2 leftover (key 3) size=" << mm2.size() << "\n"; // 1

    // extract() [C++17]
    map<int,int> me = {{1,10},{2,20},{3,30}};
    auto node = me.extract(2);
    cout << "extracted: key=" << node.key() << " val=" << node.mapped() << "\n";

    // key_comp() / value_comp()
    auto kcmp = me.key_comp();
    cout << "key_comp()(1,3)=" << kcmp(1,3) << "\n";        // 1

    // begin/end, rbegin/rend
    map<int,int> miter = {{1,1},{2,2}};
    cout << "begin->first=" << miter.begin()->first << "\n";
    cout << "rbegin->first=" << miter.rbegin()->first << "\n";
}
```
// ============================================================
//  9. MULTIMAP
// ============================================================

```cpp
void demo_multimap() {
    cout << "\n===== MULTIMAP =====\n";

    multimap<string, int> mm;

    // insert({key,val}) — duplicates allowed
    mm.insert({"alice", 10});
    mm.insert({"alice", 20});
    mm.insert({"bob",   30});
    cout << "size after 3 inserts (incl dup key): " << mm.size() << "\n"; // 3

    // emplace(key, val)
    mm.emplace("carol", 40);

    // erase(key) — removes ALL with that key
    mm.erase("alice");
    cout << "after erase(alice), size=" << mm.size() << "\n"; // 2

    // erase(it) — removes just one
    multimap<string,int> mm2;
    mm2.insert({"x",1}); mm2.insert({"x",2});
    mm2.erase(mm2.find("x"));  // only one "x"
    cout << "after erase one x, size=" << mm2.size() << "\n"; // 1

    // find(key) — returns first match
    multimap<int,int> mmi;
    mmi.insert({1,100}); mmi.insert({1,200}); mmi.insert({2,300});
    auto it = mmi.find(1);
    cout << "find(1)->second = " << it->second << "\n";      // 100 (first)

    // count(key)
    cout << "count(1) = " << mmi.count(1) << "\n";           // 2

    // contains() [C++20]
    cout << "contains(2) = " << mmi.contains(2) << "\n";    // 1

    // equal_range(key) — all entries with that key
    auto [lo, hi] = mmi.equal_range(1);
    cout << "all values for key 1: ";
    for (auto i = lo; i != hi; ++i) cout << i->second << " ";
    cout << "\n";                                            // 100 200

    // lower_bound / upper_bound
    cout << "lower_bound(1)->first = " << mmi.lower_bound(1)->first << "\n"; // 1
    cout << "upper_bound(1)->first = " << mmi.upper_bound(1)->first << "\n"; // 2

    // size / empty / clear / swap / merge / extract / key_comp — same as map
    cout << "size=" << mmi.size() << " empty=" << mmi.empty() << "\n";

    multimap<int,int> mma = {{1,1}}, mmb = {{2,2}};
    mma.swap(mmb);
    cout << "mma after swap, first key=" << mma.begin()->first << "\n"; // 2

    // begin/end, rbegin/rend
    cout << "begin->first=" << mmi.begin()->first << "\n";
    cout << "rbegin->first=" << mmi.rbegin()->first << "\n";
}
```
// ============================================================
//  10. UNORDERED_SET
// ============================================================
```cpp
void demo_unordered_set() {
    cout << "\n===== UNORDERED_SET =====\n";

    unordered_set<int> us;

    // insert()
    us.insert(10);
    us.insert(20);
    us.insert(30);
    us.insert(10);  // duplicate — ignored
    cout << "size after 4 inserts (1 dup): " << us.size() << "\n"; // 3

    // emplace()
    us.emplace(40);
    cout << "size after emplace(40): " << us.size() << "\n"; // 4

    // erase(key)
    us.erase(10);
    cout << "after erase(10), size=" << us.size() << "\n";  // 3

    // erase(it)
    us.erase(us.begin());
    cout << "after erase(begin), size=" << us.size() << "\n";

    // find()
    auto it = us.find(30);
    cout << "find(30): " << (it != us.end() ? "found" : "not found") << "\n";

    // count()
    cout << "count(30) = " << us.count(30) << "\n";          // 0 or 1

    // contains() [C++20]
    us.insert(30);
    cout << "contains(30) = " << us.contains(30) << "\n";   // 1

    // equal_range()  — returns pair of iterators (range of 0 or 1 element)
    auto [lo, hi] = us.equal_range(30);
    cout << "equal_range(30) count = " << distance(lo, hi) << "\n"; // 1

    // size / empty / max_size
    cout << "size=" << us.size() << " empty=" << us.empty() << "\n";

    // clear()
    unordered_set<int> uc = {1,2,3};
    uc.clear();
    cout << "after clear(), size=" << uc.size() << "\n";

    // swap()
    unordered_set<int> ua = {1}, ub = {9,8};
    ua.swap(ub);
    cout << "ua size after swap=" << ua.size() << "\n";      // 2

    // bucket_count()
    cout << "bucket_count=" << us.bucket_count() << "\n";

    // bucket(key)
    us.insert(99);
    cout << "bucket(99) = " << us.bucket(99) << "\n";

    // bucket_size(n)
    size_t bn = us.bucket(99);
    cout << "bucket_size(that bucket) = " << us.bucket_size(bn) << "\n";

    // load_factor()
    cout << "load_factor = " << us.load_factor() << "\n";

    // max_load_factor()
    cout << "max_load_factor = " << us.max_load_factor() << "\n";

    // max_load_factor(val) — setter
    us.max_load_factor(0.5f);
    cout << "max_load_factor after set(0.5) = " << us.max_load_factor() << "\n";

    // rehash(n)
    us.rehash(20);
    cout << "after rehash(20), bucket_count=" << us.bucket_count() << "\n";

    // reserve(n)
    us.reserve(100);
    cout << "after reserve(100), bucket_count=" << us.bucket_count() << "\n";

    // hash_function()
    auto hf = us.hash_function();
    cout << "hash_function()(42) = " << hf(42) << "\n";

    // key_eq()
    auto eq = us.key_eq();
    cout << "key_eq()(10,10) = " << eq(10,10) << "\n";      // 1

    // merge() [C++17]
    unordered_set<int> um1 = {1,3};
    unordered_set<int> um2 = {2,3};  // 3 already in um1
    um1.merge(um2);
    cout << "um1 after merge size=" << um1.size() << "\n";   // 3

    // extract() [C++17]
    unordered_set<int> ue = {10,20,30};
    auto node = ue.extract(20);
    cout << "extracted node value=" << node.value() << "\n"; // 20

    // begin/end (global)
    unordered_set<int> ui = {5,10,15};
    cout << "begin iteration count: ";
    for (auto& x : ui) cout << x << " ";
    cout << "\n";

    // begin(n)/end(n) — bucket iteration
    unordered_set<int> ubi = {1,2,3,4,5};
    for (size_t i = 0; i < ubi.bucket_count(); ++i) {
        if (ubi.bucket_size(i) > 0) {
            cout << "bucket " << i << ": ";
            for (auto bit = ubi.begin(i); bit != ubi.end(i); ++bit)
                cout << *bit << " ";
            cout << "\n";
            break;  // just show one non-empty bucket
        }
    }
}
```
// ============================================================
//  11. UNORDERED_MULTISET
// ============================================================

```cpp

void demo_unordered_multiset() {
    cout << "\n===== UNORDERED_MULTISET =====\n";

    unordered_multiset<int> ums;

    // insert() — duplicates allowed
    ums.insert(10);
    ums.insert(10);
    ums.insert(20);
    cout << "size after inserts (dup ok): " << ums.size() << "\n"; // 3

    // emplace()
    ums.emplace(30);

    // erase(key) — removes ALL
    ums.erase(10);
    cout << "after erase(10), size=" << ums.size() << "\n"; // 2

    // find() / count() / contains()
    cout << "find(20): " << (ums.find(20) != ums.end() ? "found" : "no") << "\n";
    unordered_multiset<int> ums2 = {5,5,5,6};
    cout << "count(5) = " << ums2.count(5) << "\n";          // 3
    cout << "contains(6) = " << ums2.contains(6) << "\n";   // 1

    // equal_range()
    auto [lo, hi] = ums2.equal_range(5);
    cout << "equal_range(5) count=" << distance(lo,hi) << "\n"; // 3

    // bucket_count / bucket / bucket_size / load_factor — same as unordered_set
    cout << "bucket_count=" << ums2.bucket_count() << "\n";
    cout << "load_factor=" << ums2.load_factor() << "\n";

    // rehash / reserve
    ums2.rehash(50);
    ums2.reserve(100);

    // hash_function / key_eq
    auto hf = ums2.hash_function();
    cout << "hash(5)=" << hf(5) << "\n";

    // merge / extract — same semantics as unordered_set
    unordered_multiset<int> um1 = {1,2}, um2 = {2,3};
    um1.merge(um2);
    cout << "um1 after merge size=" << um1.size() << "\n";   // 4 (2 appears twice)

    // swap / clear
    unordered_multiset<int> ux = {1}, uy = {9,9};
    ux.swap(uy);
    cout << "ux size after swap=" << ux.size() << "\n";      // 2

    ux.clear();
    cout << "after clear(), empty=" << ux.empty() << "\n";
}
```
// ============================================================
//  12. UNORDERED_MAP
// ============================================================
```cpp
void demo_unordered_map() {
    cout << "\n===== UNORDERED_MAP =====\n";

    unordered_map<string,int> um;

    // operator[]
    um["alice"] = 10;
    um["bob"]   = 20;
    cout << "um[\"alice\"] = " << um["alice"] << "\n";       // 10

    // at()
    cout << "um.at(\"bob\") = " << um.at("bob") << "\n";    // 20

    // insert({key,val})
    um.insert({"carol", 30});
    cout << "size after insert carol: " << um.size() << "\n"; // 3

    // insert_or_assign(key,val) [C++17]
    um.insert_or_assign("alice", 99);
    cout << "alice after insert_or_assign(99)=" << um["alice"] << "\n"; // 99

    // emplace()
    um.emplace("dave", 40);

    // try_emplace(key, val) [C++17]
    um.try_emplace("alice", 999);  // key exists — no change
    um.try_emplace("eve", 50);
    cout << "alice unchanged=" << um["alice"] << "\n";       // 99
    cout << "eve=" << um["eve"] << "\n";                     // 50

    // erase(key)
    um.erase("carol");
    cout << "after erase carol, size=" << um.size() << "\n";

    // find()
    auto it = um.find("dave");
    if (it != um.end()) cout << "find(dave)=" << it->second << "\n"; // 40

    // count() / contains()
    cout << "count(dave)=" << um.count("dave") << "\n";      // 1
    cout << "contains(eve)=" << um.contains("eve") << "\n"; // 1

    // equal_range()
    auto [lo, hi] = um.equal_range("dave");
    cout << "equal_range(dave) count=" << distance(lo,hi) << "\n"; // 1

    // size / empty
    cout << "size=" << um.size() << " empty=" << um.empty() << "\n";

    // bucket_count / bucket / bucket_size / load_factor
    cout << "bucket_count=" << um.bucket_count() << "\n";
    size_t bn = um.bucket("dave");
    cout << "bucket(dave)=" << bn << " size=" << um.bucket_size(bn) << "\n";
    cout << "load_factor=" << um.load_factor() << "\n";
    cout << "max_load_factor=" << um.max_load_factor() << "\n";

    // rehash / reserve
    um.rehash(20);
    um.reserve(50);

    // hash_function / key_eq
    auto hf = um.hash_function();
    cout << "hash(\"alice\")=" << hf("alice") << "\n";

    // merge() [C++17]
    unordered_map<string,int> um1 = {{"x",1}};
    unordered_map<string,int> um2 = {{"y",2},{"x",9}};
    um1.merge(um2);
    cout << "um1 after merge size=" << um1.size() << "\n";   // 2

    // extract() [C++17]
    unordered_map<string,int> ue = {{"a",1},{"b",2}};
    auto node = ue.extract("a");
    cout << "extracted key=" << node.key() << " val=" << node.mapped() << "\n";

    // swap / clear
    unordered_map<string,int> ux = {{"z",0}};
    um.swap(ux);
    um.clear();
    cout << "after clear(), size=" << um.size() << "\n";

    // begin/end (global + bucket)
    unordered_map<string,int> umi = {{"p",1},{"q",2}};
    cout << "first pair: " << umi.begin()->first << "\n";
}
```
// ============================================================
//  13. UNORDERED_MULTIMAP
// ============================================================

```cpp
void demo_unordered_multimap() {
    cout << "\n===== UNORDERED_MULTIMAP =====\n";

    unordered_multimap<string,int> umm;

    // insert({key,val}) — duplicates allowed
    umm.insert({"alice", 1});
    umm.insert({"alice", 2});
    umm.insert({"bob",   3});
    cout << "size (alice twice): " << umm.size() << "\n";   // 3

    // emplace()
    umm.emplace("carol", 4);

    // erase(key) — removes ALL with that key
    umm.erase("alice");
    cout << "after erase alice, size=" << umm.size() << "\n"; // 2

    // find() — first match
    unordered_multimap<int,int> mm;
    mm.insert({1,10}); mm.insert({1,20}); mm.insert({2,30});
    auto it = mm.find(1);
    cout << "find(1)->second=" << it->second << "\n";        // 10 or 20

    // count()
    cout << "count(1)=" << mm.count(1) << "\n";              // 2

    // contains() [C++20]
    cout << "contains(2)=" << mm.contains(2) << "\n";       // 1

    // equal_range()
    auto [lo, hi] = mm.equal_range(1);
    cout << "equal_range(1) count=" << distance(lo,hi) << "\n"; // 2

    // bucket_count / bucket / load_factor / rehash / reserve — same
    cout << "bucket_count=" << mm.bucket_count() << "\n";
    mm.rehash(30);
    mm.reserve(50);

    // hash_function / key_eq
    auto hf = mm.hash_function();
    cout << "hash(1)=" << hf(1) << "\n";

    // merge / extract / swap / clear — same semantics
    unordered_multimap<int,int> um1 = {{1,1}}, um2 = {{1,2},{3,3}};
    um1.merge(um2);
    cout << "um1 after merge size=" << um1.size() << "\n";   // 3

    unordered_multimap<int,int> ux = {{5,5}}, uy = {{6,6}};
    ux.swap(uy);
    cout << "ux after swap, begin->first=" << ux.begin()->first << "\n"; // 6

    ux.clear();
    cout << "after clear(), size=" << ux.size() << "\n";

    // begin/end (global + bucket iteration)
    unordered_multimap<int,int> ui = {{1,1},{2,2},{3,3}};
    cout << "iterating: ";
    for (auto& [k,v] : ui) cout << k << ":" << v << " ";
    cout << "\n";
}
```
// ============================================================
//  14. STACK
// ============================================================
```cpp
void demo_stack() {
    cout << "\n===== STACK =====\n";

    stack<int> st;

    // push()
    st.push(10);
    st.push(20);
    st.push(30);
    cout << "push 10,20,30 — top=" << st.top() << "\n";      // 30

    // emplace()
    st.emplace(40);
    cout << "emplace(40) — top=" << st.top() << "\n";        // 40

    // top()
    cout << "top() = " << st.top() << "\n";                  // 40

    // pop()
    st.pop();
    cout << "after pop(), top=" << st.top() << "\n";         // 30

    // size()
    cout << "size() = " << st.size() << "\n";                // 3

    // empty()
    cout << "empty() = " << st.empty() << "\n";              // 0

    // swap()
    stack<int> st2;
    st2.push(99);
    st.swap(st2);
    cout << "after swap, top=" << st.top() << "\n";          // 99

    // stack on top of list (custom underlying)
    stack<int, list<int>> lst_stack;
    lst_stack.push(5);
    lst_stack.push(6);
    cout << "list-backed stack top=" << lst_stack.top() << "\n"; // 6
}
```
// ============================================================
//  15. QUEUE
// ============================================================

```cpp
void demo_queue() {
    cout << "\n===== QUEUE =====\n";

    queue<int> q;

    // push()
    q.push(10);
    q.push(20);
    q.push(30);
    cout << "push 10,20,30 — front=" << q.front() << " back=" << q.back() << "\n";

    // emplace()
    q.emplace(40);
    cout << "emplace(40) — back=" << q.back() << "\n";       // 40

    // front()
    cout << "front() = " << q.front() << "\n";               // 10

    // back()
    cout << "back() = " << q.back() << "\n";                 // 40

    // pop()  — removes front
    q.pop();
    cout << "after pop(), front=" << q.front() << "\n";      // 20

    // size()
    cout << "size() = " << q.size() << "\n";                 // 3

    // empty()
    cout << "empty() = " << q.empty() << "\n";               // 0

    // swap()
    queue<int> q2;
    q2.push(99);
    q.swap(q2);
    cout << "after swap, front=" << q.front() << "\n";       // 99
}
```
// ============================================================
//  16. PRIORITY_QUEUE
// ============================================================
```cpp
void demo_priority_queue() {
    cout << "\n===== PRIORITY_QUEUE =====\n";

    // Default: max-heap
    priority_queue<int> pq;

    // push()
    pq.push(10);
    pq.push(50);
    pq.push(30);
    cout << "push 10,50,30 — top=" << pq.top() << "\n";      // 50 (max)

    // emplace()
    pq.emplace(70);
    cout << "emplace(70) — top=" << pq.top() << "\n";        // 70

    // top()
    cout << "top() = " << pq.top() << "\n";                  // 70

    // pop()
    pq.pop();
    cout << "after pop(), top=" << pq.top() << "\n";         // 50

    // size()
    cout << "size() = " << pq.size() << "\n";                // 3

    // empty()
    cout << "empty() = " << pq.empty() << "\n";              // 0

    // swap()
    priority_queue<int> pq2;
    pq2.push(1);
    pq.swap(pq2);
    cout << "after swap, top=" << pq.top() << "\n";          // 1

    // Min-heap using greater<>
    priority_queue<int, vector<int>, greater<int>> minpq;
    minpq.push(30);
    minpq.push(10);
    minpq.push(20);
    cout << "min-heap top=" << minpq.top() << "\n";          // 10

    // Build from range (using vector initializer)
    vector<int> v = {5, 1, 4, 2, 8};
    priority_queue<int> pq3(v.begin(), v.end());
    cout << "built from range, top=" << pq3.top() << "\n";  // 8
}
```
// ============================================================
//  MAIN
// ============================================================
```cpp
int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    demo_vector();
    demo_deque();
    demo_list();
    demo_forward_list();
    demo_array();
    demo_set();
    demo_multiset();
    demo_map();
    demo_multimap();
    demo_unordered_set();
    demo_unordered_multiset();
    demo_unordered_map();
    demo_unordered_multimap();
    demo_stack();
    demo_queue();
    demo_priority_queue();

    cout << "\nAll demos complete.\n";
    return 0;
}
```
