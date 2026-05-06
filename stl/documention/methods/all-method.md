# C++ Standard Library — Complete Headers Reference

---

## 🔹 1. Input / Output

---

### `<iostream>`

| Object / Function | Description |
|---|---|
| `std::cin` | Standard input stream |
| `std::cout` | Standard output stream |
| `std::cerr` | Standard error stream (unbuffered) |
| `std::clog` | Standard error stream (buffered) |
| `std::wcin/wcout/wcerr/wclog` | Wide-character variants |
| `>>` | Extraction operator (input) |
| `<<` | Insertion operator (output) |
| `std::endl` | Insert newline + flush |
| `std::flush` | Flush the buffer |

```cpp
#include <iostream>

int main() {
    int x;
    std::cout << "Enter a number: ";
    std::cin >> x;
    std::cerr << "Debug: x = " << x << std::endl;
    std::cout << "You entered: " << x << std::flush;
}
```

---

### `<cstdio>`

| Function | Description |
|---|---|
| `printf(fmt, ...)` | Formatted print to stdout |
| `scanf(fmt, ...)` | Formatted read from stdin |
| `fprintf(file, fmt, ...)` | Print to file |
| `fscanf(file, fmt, ...)` | Read from file |
| `sprintf(buf, fmt, ...)` | Print to string buffer |
| `sscanf(buf, fmt, ...)` | Read from string buffer |
| `snprintf(buf, n, fmt, ...)` | Safe print to buffer (n bytes max) |
| `fgets(buf, n, file)` | Read line from file |
| `fputs(str, file)` | Write string to file |
| `fopen(path, mode)` | Open file |
| `fclose(file)` | Close file |
| `fread(buf, size, n, file)` | Read binary data |
| `fwrite(buf, size, n, file)` | Write binary data |
| `fseek(file, off, origin)` | Seek in file |
| `ftell(file)` | Get file position |
| `rewind(file)` | Rewind to start |
| `feof(file)` | Check end-of-file |
| `ferror(file)` | Check file error |
| `fflush(file)` | Flush file buffer |
| `remove(path)` | Delete file |
| `rename(old, new)` | Rename file |
| `getchar()` | Read char from stdin |
| `putchar(c)` | Write char to stdout |
| `gets_s(buf, n)` | Safe read line (C11) |
| `puts(str)` | Write string + newline |
| `perror(msg)` | Print error message |

```cpp
#include <cstdio>

int main() {
    char name[50];
    printf("Enter name: ");
    scanf("%49s", name);
    printf("Hello, %s!\n", name);

    FILE* f = fopen("out.txt", "w");
    if (f) {
        fprintf(f, "Name: %s\n", name);
        fclose(f);
    }

    char buf[64];
    snprintf(buf, sizeof(buf), "Value: %d", 42);
    puts(buf);
}
```

---

### `<cstdlib>`

| Function | Description |
|---|---|
| `atoi(str)` | String to int |
| `atol(str)` | String to long |
| `atof(str)` | String to double |
| `strtol(str, end, base)` | String to long with base |
| `strtoul(str, end, base)` | String to unsigned long |
| `strtod(str, end)` | String to double |
| `strtof(str, end)` | String to float |
| `strtoll(str, end, base)` | String to long long |
| `rand()` | Random int [0, RAND_MAX] |
| `srand(seed)` | Set random seed |
| `malloc(size)` | Allocate memory |
| `calloc(n, size)` | Allocate + zero memory |
| `realloc(ptr, size)` | Resize allocation |
| `free(ptr)` | Free memory |
| `exit(code)` | Exit program |
| `abort()` | Abnormal termination |
| `atexit(fn)` | Register exit handler |
| `system(cmd)` | Run shell command |
| `getenv(name)` | Get environment variable |
| `abs(n)` | Absolute value (int) |
| `labs(n)` | Absolute value (long) |
| `llabs(n)` | Absolute value (long long) |
| `div(a, b)` | Integer division + remainder |
| `ldiv(a, b)` | Long division + remainder |
| `qsort(arr, n, sz, cmp)` | Quick sort |
| `bsearch(key, arr, n, sz, cmp)` | Binary search |
| `mbstowcs(dst, src, n)` | Multibyte to wide char |
| `wcstombs(dst, src, n)` | Wide char to multibyte |

```cpp
#include <cstdlib>
#include <cstdio>

int cmp(const void* a, const void* b) {
    return *(int*)a - *(int*)b;
}

int main() {
    int arr[] = {5, 2, 8, 1, 9};
    qsort(arr, 5, sizeof(int), cmp);
    for (int i = 0; i < 5; i++) printf("%d ", arr[i]); // 1 2 5 8 9

    srand(42);
    printf("\nRandom: %d\n", rand() % 100);

    char* val = getenv("PATH");
    printf("PATH exists: %s\n", val ? "yes" : "no");

    int n = atoi("123");
    printf("atoi: %d\n", n);
}
```

---

### `<iomanip>`

| Manipulator | Description |
|---|---|
| `std::setw(n)` | Set field width |
| `std::setfill(c)` | Set fill character |
| `std::setprecision(n)` | Set decimal precision |
| `std::fixed` | Fixed-point notation |
| `std::scientific` | Scientific notation |
| `std::defaultfloat` | Default float format |
| `std::left` | Left-align |
| `std::right` | Right-align (default) |
| `std::internal` | Pad between sign and value |
| `std::boolalpha` | Print bools as true/false |
| `std::noboolalpha` | Print bools as 0/1 |
| `std::showbase` | Show 0x / 0 prefix |
| `std::noshowbase` | Hide prefix |
| `std::showpoint` | Always show decimal point |
| `std::showpos` | Show + for positives |
| `std::uppercase` | Use uppercase hex/sci |
| `std::hex` | Hex output |
| `std::oct` | Octal output |
| `std::dec` | Decimal output |
| `std::resetiosflags(f)` | Reset specific flags |
| `std::setiosflags(f)` | Set specific flags |
| `std::get_money(val)` | Read monetary value |
| `std::put_money(val)` | Write monetary value |
| `std::get_time(tm, fmt)` | Read time |
| `std::put_time(tm, fmt)` | Write time |

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double pi = 3.14159265358979;
    std::cout << std::fixed << std::setprecision(4) << pi << "\n";   // 3.1416
    std::cout << std::scientific << pi << "\n";                       // 3.1416e+00
    std::cout << std::setw(10) << std::setfill('*') << 42 << "\n";  // ********42
    std::cout << std::left << std::setw(10) << "hi" << "|\n";       // hi        |
    std::cout << std::boolalpha << true << "\n";                      // true
    std::cout << std::hex << std::showbase << 255 << "\n";           // 0xff
}
```

---

### `<ios>`

| Item | Description |
|---|---|
| `std::ios_base::fmtflags` | Format flags type |
| `stream.flags()` | Get/set all flags |
| `stream.setf(flags)` | Set flags |
| `stream.unsetf(flags)` | Clear flags |
| `stream.width(n)` | Get/set width |
| `stream.precision(n)` | Get/set precision |
| `stream.fill(c)` | Get/set fill char |
| `stream.good()` | No errors? |
| `stream.fail()` | Logical error? |
| `stream.bad()` | Read/write error? |
| `stream.eof()` | End of file? |
| `stream.clear()` | Clear error flags |
| `stream.rdstate()` | Get error state |
| `stream.exceptions(mask)` | Throw on error mask |
| `std::ios::in/out/app/ate/binary/trunc` | Open mode flags |
| `std::ios::beg/cur/end` | Seek origins |

```cpp
#include <iostream>
#include <ios>

int main() {
    std::cout.width(8);
    std::cout.fill('-');
    std::cout << 42 << "\n";  // ------42

    std::cout.precision(3);
    std::cout << std::fixed << 3.14159 << "\n";  // 3.142

    int x;
    std::cin >> x;
    if (std::cin.fail()) {
        std::cin.clear();
        std::cout << "Bad input\n";
    }
}
```

---

### `<istream>`

| Method | Description |
|---|---|
| `stream >> val` | Formatted extraction |
| `stream.get()` | Read one char |
| `stream.get(c)` | Read char into c |
| `stream.get(buf, n)` | Read up to n-1 chars |
| `stream.getline(buf, n)` | Read line into C-string |
| `stream.getline(buf, n, delim)` | Read until delim |
| `stream.read(buf, n)` | Read n bytes (binary) |
| `stream.readsome(buf, n)` | Read available bytes |
| `stream.peek()` | Peek next char |
| `stream.putback(c)` | Put char back |
| `stream.unget()` | Un-read last char |
| `stream.ignore(n, delim)` | Skip chars |
| `stream.gcount()` | Chars read by last unformatted read |
| `stream.tellg()` | Get read position |
| `stream.seekg(pos)` | Set read position |
| `stream.seekg(off, dir)` | Seek relative |
| `stream.sync()` | Sync with underlying device |

```cpp
#include <iostream>
#include <sstream>

int main() {
    std::istringstream ss("hello world 42");

    std::string w1, w2;
    int n;
    ss >> w1 >> w2 >> n;
    std::cout << w1 << " | " << w2 << " | " << n << "\n"; // hello | world | 42

    ss.clear(); ss.str("abc");
    char c = ss.get();
    std::cout << c << "\n";  // a

    ss.seekg(0);
    char buf[10];
    ss.getline(buf, 10);
    std::cout << buf << "\n";  // abc
}
```

---

### `<ostream>`

| Method | Description |
|---|---|
| `stream << val` | Formatted insertion |
| `stream.put(c)` | Write one char |
| `stream.write(buf, n)` | Write n bytes (binary) |
| `stream.flush()` | Flush buffer |
| `stream.tellp()` | Get write position |
| `stream.seekp(pos)` | Set write position |
| `stream.seekp(off, dir)` | Seek relative |
| `std::endl` | `\n` + flush |
| `std::ends` | Null terminator |
| `std::flush` | Flush without newline |

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream f("demo.bin", std::ios::binary);
    int arr[] = {1, 2, 3};
    f.write(reinterpret_cast<char*>(arr), sizeof(arr));  // binary write
    f.flush();

    std::cout.put('H').put('i') << std::endl;  // Hi

    std::cout << std::showpos << 3.14f << "\n"; // +3.14
}
```

---

## 🔹 2. Containers (STL)

---

### `<vector>`

| Method | Description |
|---|---|
| `v.push_back(x)` | Append element |
| `v.pop_back()` | Remove last |
| `v.emplace_back(...)` | Construct in-place at end |
| `v.insert(it, x)` | Insert before iterator |
| `v.insert(it, n, x)` | Insert n copies |
| `v.insert(it, first, last)` | Insert range |
| `v.emplace(it, ...)` | Construct in-place at pos |
| `v.erase(it)` | Remove at iterator |
| `v.erase(first, last)` | Remove range |
| `v.clear()` | Remove all |
| `v.resize(n)` | Resize (fill with 0) |
| `v.resize(n, val)` | Resize with value |
| `v.reserve(n)` | Reserve capacity |
| `v.shrink_to_fit()` | Reduce capacity to size |
| `v.size()` | Number of elements |
| `v.capacity()` | Allocated capacity |
| `v.empty()` | Is empty? |
| `v[i]` | Element access (unchecked) |
| `v.at(i)` | Element access (bounds-checked) |
| `v.front()` | First element |
| `v.back()` | Last element |
| `v.data()` | Raw pointer |
| `v.begin() / v.end()` | Iterators |
| `v.rbegin() / v.rend()` | Reverse iterators |
| `v.assign(n, val)` | Assign n copies |
| `v.assign(first, last)` | Assign from range |
| `v.swap(v2)` | Swap with another vector |
| `v.max_size()` | Max possible size |

```cpp
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5};
    v.push_back(9);
    v.insert(v.begin() + 2, 99);
    v.erase(v.begin());
    v.resize(4);

    for (int x : v) std::cout << x << " "; // 1 99 1 5
    std::cout << "\nSize: " << v.size() << ", Cap: " << v.capacity() << "\n";
}
```

---

### `<list>`

| Method | Description |
|---|---|
| `l.push_back(x)` | Append |
| `l.push_front(x)` | Prepend |
| `l.pop_back()` | Remove last |
| `l.pop_front()` | Remove first |
| `l.insert(it, x)` | Insert before iterator |
| `l.emplace(it, ...)` | Construct in-place |
| `l.emplace_back(...)` | Construct at end |
| `l.emplace_front(...)` | Construct at front |
| `l.erase(it)` | Remove at iterator |
| `l.erase(first, last)` | Remove range |
| `l.clear()` | Remove all |
| `l.remove(val)` | Remove all matching |
| `l.remove_if(pred)` | Remove matching predicate |
| `l.sort()` | Sort (stable) |
| `l.sort(cmp)` | Sort with comparator |
| `l.reverse()` | Reverse in-place |
| `l.unique()` | Remove consecutive dups |
| `l.unique(pred)` | Remove by predicate |
| `l.merge(l2)` | Merge sorted lists |
| `l.splice(it, l2)` | Move all of l2 into l at it |
| `l.splice(it, l2, it2)` | Move one element |
| `l.size()` | Number of elements |
| `l.empty()` | Is empty? |
| `l.front()` | First element |
| `l.back()` | Last element |
| `l.begin() / l.end()` | Iterators |
| `l.swap(l2)` | Swap |
| `l.assign(n, val)` | Assign |
| `l.resize(n)` | Resize |
| `l.max_size()` | Max size |

```cpp
#include <list>
#include <iostream>

int main() {
    std::list<int> l = {4, 2, 5, 1, 3};
    l.push_front(0);
    l.push_back(6);
    l.sort();
    l.unique();
    l.remove_if([](int x){ return x % 2 == 0; }); // remove evens
    for (int x : l) std::cout << x << " "; // 1 3 5
}
```

---

### `<deque>`

| Method | Description |
|---|---|
| `d.push_back(x)` | Append |
| `d.push_front(x)` | Prepend |
| `d.pop_back()` | Remove last |
| `d.pop_front()` | Remove first |
| `d.emplace_back(...)` | Construct at end |
| `d.emplace_front(...)` | Construct at front |
| `d.insert(it, x)` | Insert at iterator |
| `d.emplace(it, ...)` | Construct at iterator |
| `d.erase(it)` | Remove at iterator |
| `d.erase(first, last)` | Remove range |
| `d.clear()` | Remove all |
| `d.resize(n)` | Resize |
| `d[i]` | Access (unchecked) |
| `d.at(i)` | Access (bounds-checked) |
| `d.front()` | First element |
| `d.back()` | Last element |
| `d.size()` | Size |
| `d.empty()` | Is empty? |
| `d.begin() / d.end()` | Iterators |
| `d.shrink_to_fit()` | Reduce memory |
| `d.swap(d2)` | Swap |
| `d.assign(n, val)` | Assign |
| `d.max_size()` | Max size |

```cpp
#include <deque>
#include <iostream>

int main() {
    std::deque<int> d;
    for (int i = 1; i <= 3; i++) { d.push_back(i); d.push_front(i * 10); }
    // 30 20 10 1 2 3
    d.pop_front(); d.pop_back();
    for (int x : d) std::cout << x << " "; // 20 10 1 2
}
```

---

### `<array>`

| Method | Description |
|---|---|
| `a[i]` | Access (unchecked) |
| `a.at(i)` | Access (bounds-checked) |
| `a.front()` | First element |
| `a.back()` | Last element |
| `a.data()` | Raw pointer |
| `a.fill(val)` | Fill all with value |
| `a.swap(a2)` | Swap |
| `a.size()` | Size (compile-time) |
| `a.max_size()` | Same as size() |
| `a.empty()` | Always false (unless N=0) |
| `a.begin() / a.end()` | Iterators |
| `a.rbegin() / a.rend()` | Reverse iterators |
| `std::get<I>(a)` | Compile-time index access |

```cpp
#include <array>
#include <algorithm>
#include <iostream>

int main() {
    std::array<int, 5> a = {5, 3, 1, 4, 2};
    a.fill(0);  // all zeros

    std::array<int, 5> b = {5, 3, 1, 4, 2};
    std::sort(b.begin(), b.end());
    for (int x : b) std::cout << x << " "; // 1 2 3 4 5

    std::cout << std::get<2>(b) << "\n"; // 3
}
```

---

### `<set>`

| Method | Description |
|---|---|
| `s.insert(x)` | Insert element |
| `s.emplace(...)` | Construct in-place |
| `s.erase(x)` | Erase by value |
| `s.erase(it)` | Erase by iterator |
| `s.erase(first, last)` | Erase range |
| `s.find(x)` | Iterator to element (or end) |
| `s.count(x)` | 0 or 1 |
| `s.contains(x)` | bool (C++20) |
| `s.lower_bound(x)` | First element >= x |
| `s.upper_bound(x)` | First element > x |
| `s.equal_range(x)` | Pair of lower/upper bound |
| `s.clear()` | Remove all |
| `s.size()` | Size |
| `s.empty()` | Is empty? |
| `s.begin() / s.end()` | Iterators (sorted) |
| `s.rbegin() / s.rend()` | Reverse iterators |
| `s.swap(s2)` | Swap |
| `s.merge(s2)` | Merge from another set (C++17) |
| `s.extract(x)` | Extract node (C++17) |
| `s.max_size()` | Max size |
| `s.key_comp()` | Key comparator |
| `s.value_comp()` | Value comparator |
| `std::multiset` | Allows duplicates |

```cpp
#include <set>
#include <iostream>

int main() {
    std::set<int> s = {5, 1, 3, 1, 4}; // duplicates removed: {1,3,4,5}
    s.insert(2);
    s.erase(3);
    std::cout << s.count(4) << "\n"; // 1

    auto it = s.lower_bound(3);
    std::cout << *it << "\n"; // 4

    for (int x : s) std::cout << x << " "; // 1 2 4 5
}
```

---

### `<map>`

| Method | Description |
|---|---|
| `m[key]` | Access/insert |
| `m.at(key)` | Access (throws if missing) |
| `m.insert({k,v})` | Insert pair |
| `m.insert_or_assign(k,v)` | Insert or update (C++17) |
| `m.emplace(k, v)` | Construct in-place |
| `m.try_emplace(k, ...)` | Insert if not exists (C++17) |
| `m.erase(key)` | Erase by key |
| `m.erase(it)` | Erase by iterator |
| `m.erase(first, last)` | Erase range |
| `m.find(key)` | Iterator to key (or end) |
| `m.count(key)` | 0 or 1 |
| `m.contains(key)` | bool (C++20) |
| `m.lower_bound(key)` | First key >= key |
| `m.upper_bound(key)` | First key > key |
| `m.equal_range(key)` | Pair of bounds |
| `m.clear()` | Remove all |
| `m.size()` | Size |
| `m.empty()` | Is empty? |
| `m.begin() / m.end()` | Iterators |
| `m.rbegin() / m.rend()` | Reverse iterators |
| `m.swap(m2)` | Swap |
| `m.merge(m2)` | Merge (C++17) |
| `m.extract(key)` | Extract node (C++17) |
| `m.key_comp()` | Key comparator |
| `std::multimap` | Allows duplicate keys |

```cpp
#include <map>
#include <iostream>

int main() {
    std::map<std::string, int> freq;
    std::string words[] = {"apple", "banana", "apple", "cherry", "banana", "apple"};
    for (auto& w : words) freq[w]++;

    for (auto& [k, v] : freq) std::cout << k << ": " << v << "\n";
    // apple: 3, banana: 2, cherry: 1

    if (freq.contains("banana")) freq.erase("banana");
    std::cout << freq.size() << "\n"; // 2
}
```

---

### `<unordered_set>`

| Method | Description |
|---|---|
| `s.insert(x)` | Insert |
| `s.emplace(...)` | Construct in-place |
| `s.erase(x)` | Erase by value |
| `s.erase(it)` | Erase by iterator |
| `s.find(x)` | Iterator (or end) |
| `s.count(x)` | 0 or 1 |
| `s.contains(x)` | bool (C++20) |
| `s.clear()` | Remove all |
| `s.size()` | Size |
| `s.empty()` | Is empty? |
| `s.bucket_count()` | Number of buckets |
| `s.bucket(x)` | Bucket for element |
| `s.load_factor()` | Elements per bucket |
| `s.max_load_factor()` | Max load factor |
| `s.rehash(n)` | Set bucket count |
| `s.reserve(n)` | Reserve for n elements |
| `s.begin() / s.end()` | Iterators |
| `s.swap(s2)` | Swap |
| `s.merge(s2)` | Merge (C++17) |
| `std::unordered_multiset` | Allows duplicates |

```cpp
#include <unordered_set>
#include <iostream>

int main() {
    std::unordered_set<int> s = {3, 1, 4, 1, 5, 9, 2, 6};
    // duplicates removed, O(1) average lookup
    s.insert(7);
    s.erase(4);

    std::cout << s.contains(5) << "\n"; // 1
    std::cout << "Buckets: " << s.bucket_count() << "\n";
    for (int x : s) std::cout << x << " "; // unordered
}
```

---

### `<unordered_map>`

| Method | Description |
|---|---|
| `m[key]` | Access/insert |
| `m.at(key)` | Access (throws) |
| `m.insert({k,v})` | Insert pair |
| `m.insert_or_assign(k,v)` | Insert or update (C++17) |
| `m.emplace(k, v)` | Construct in-place |
| `m.try_emplace(k, ...)` | Insert if not exists (C++17) |
| `m.erase(key)` | Erase by key |
| `m.find(key)` | Iterator or end |
| `m.count(key)` | 0 or 1 |
| `m.contains(key)` | bool (C++20) |
| `m.clear()` | Remove all |
| `m.size()` | Size |
| `m.empty()` | Is empty? |
| `m.bucket_count()` | Number of buckets |
| `m.load_factor()` | Load factor |
| `m.rehash(n)` | Rehash |
| `m.reserve(n)` | Reserve |
| `m.begin() / m.end()` | Iterators |
| `m.swap(m2)` | Swap |
| `std::unordered_multimap` | Allows duplicate keys |

```cpp
#include <unordered_map>
#include <iostream>

int main() {
    std::unordered_map<std::string, int> score;
    score["Alice"] = 95;
    score["Bob"] = 87;
    score.try_emplace("Alice", 100); // won't overwrite
    score.insert_or_assign("Bob", 90); // will overwrite

    for (auto& [k, v] : score) std::cout << k << ": " << v << "\n";
    std::cout << score.load_factor() << "\n";
}
```

---

### `<stack>`

| Method | Description |
|---|---|
| `s.push(x)` | Push element |
| `s.emplace(...)` | Construct in-place |
| `s.pop()` | Remove top |
| `s.top()` | Access top |
| `s.size()` | Size |
| `s.empty()` | Is empty? |
| `s.swap(s2)` | Swap |

```cpp
#include <stack>
#include <iostream>

int main() {
    std::stack<int> s;
    for (int i = 1; i <= 5; i++) s.push(i);
    while (!s.empty()) {
        std::cout << s.top() << " "; // 5 4 3 2 1
        s.pop();
    }
}
```

---

### `<queue>`

**`std::queue`**

| Method | Description |
|---|---|
| `q.push(x)` | Enqueue |
| `q.emplace(...)` | Construct in-place |
| `q.pop()` | Dequeue |
| `q.front()` | Access front |
| `q.back()` | Access back |
| `q.size()` | Size |
| `q.empty()` | Is empty? |
| `q.swap(q2)` | Swap |

**`std::priority_queue`**

| Method | Description |
|---|---|
| `pq.push(x)` | Insert |
| `pq.emplace(...)` | Construct in-place |
| `pq.pop()` | Remove top |
| `pq.top()` | Access max (or min) |
| `pq.size()` | Size |
| `pq.empty()` | Is empty? |
| `pq.swap(pq2)` | Swap |

```cpp
#include <queue>
#include <iostream>

int main() {
    // Regular queue (FIFO)
    std::queue<int> q;
    for (int i = 1; i <= 3; i++) q.push(i);
    while (!q.empty()) { std::cout << q.front() << " "; q.pop(); } // 1 2 3
    std::cout << "\n";

    // Max-heap (default)
    std::priority_queue<int> pq;
    for (int x : {3, 1, 4, 1, 5}) pq.push(x);
    while (!pq.empty()) { std::cout << pq.top() << " "; pq.pop(); } // 5 4 3 1 1

    // Min-heap
    std::priority_queue<int, std::vector<int>, std::greater<int>> minpq;
    for (int x : {3, 1, 4, 1, 5}) minpq.push(x);
    std::cout << "\n" << minpq.top() << "\n"; // 1
}
```

---

## 🔹 3. Algorithms & Utilities

---

### `<algorithm>`

| Function | Description |
|---|---|
| `std::sort(first, last)` | Sort range |
| `std::sort(first, last, cmp)` | Sort with comparator |
| `std::stable_sort(...)` | Stable sort |
| `std::partial_sort(first, mid, last)` | Sort first n elements |
| `std::nth_element(first, nth, last)` | Partition around nth |
| `std::binary_search(first, last, val)` | Bool search |
| `std::lower_bound(first, last, val)` | First >= val |
| `std::upper_bound(first, last, val)` | First > val |
| `std::equal_range(first, last, val)` | Both bounds |
| `std::find(first, last, val)` | Find value |
| `std::find_if(first, last, pred)` | Find by predicate |
| `std::find_if_not(...)` | Find where pred is false |
| `std::count(first, last, val)` | Count occurrences |
| `std::count_if(first, last, pred)` | Count by predicate |
| `std::max(a, b)` | Maximum |
| `std::min(a, b)` | Minimum |
| `std::max_element(first, last)` | Iterator to max |
| `std::min_element(first, last)` | Iterator to min |
| `std::minmax(a, b)` | Pair {min, max} |
| `std::clamp(v, lo, hi)` | Clamp value (C++17) |
| `std::reverse(first, last)` | Reverse range |
| `std::rotate(first, mid, last)` | Rotate range |
| `std::shuffle(first, last, rng)` | Random shuffle |
| `std::next_permutation(first, last)` | Next permutation |
| `std::prev_permutation(first, last)` | Previous permutation |
| `std::unique(first, last)` | Remove consecutive dups |
| `std::unique_copy(...)` | Copy unique |
| `std::remove(first, last, val)` | Remove (doesn't resize) |
| `std::remove_if(first, last, pred)` | Remove by predicate |
| `std::replace(first, last, old, new)` | Replace values |
| `std::replace_if(...)` | Replace by predicate |
| `std::fill(first, last, val)` | Fill with value |
| `std::fill_n(first, n, val)` | Fill n elements |
| `std::generate(first, last, gen)` | Fill with generator |
| `std::copy(first, last, dest)` | Copy range |
| `std::copy_if(first, last, dest, pred)` | Conditional copy |
| `std::copy_n(first, n, dest)` | Copy n elements |
| `std::move(first, last, dest)` | Move range |
| `std::transform(first, last, dest, fn)` | Apply function |
| `std::for_each(first, last, fn)` | Apply for each |
| `std::accumulate(first, last, init)` | Sum (in `<numeric>`) |
| `std::all_of(first, last, pred)` | All satisfy pred? |
| `std::any_of(first, last, pred)` | Any satisfy pred? |
| `std::none_of(first, last, pred)` | None satisfy pred? |
| `std::equal(first1, last1, first2)` | Ranges equal? |
| `std::mismatch(first1, last1, first2)` | First mismatch |
| `std::lexicographical_compare(...)` | Lexicographic < |
| `std::merge(f1, l1, f2, l2, dest)` | Merge sorted ranges |
| `std::inplace_merge(first, mid, last)` | Merge in-place |
| `std::set_union(...)` | Set union |
| `std::set_intersection(...)` | Set intersection |
| `std::set_difference(...)` | Set difference |
| `std::set_symmetric_difference(...)` | Symmetric difference |
| `std::is_sorted(first, last)` | Check sorted? |
| `std::is_permutation(f1,l1,f2)` | Is permutation? |
| `std::partition(first, last, pred)` | Partition range |
| `std::stable_partition(...)` | Stable partition |
| `std::is_partitioned(...)` | Check partitioned? |
| `std::heap operations` | make/push/pop/sort_heap |
| `std::swap(a, b)` | Swap two values |
| `std::iter_swap(it1, it2)` | Swap via iterators |
| `std::sample(...)` | Random sample (C++17) |

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {5, 2, 8, 1, 9, 3, 7, 4, 6};

    std::sort(v.begin(), v.end());
    auto it = std::lower_bound(v.begin(), v.end(), 5);
    std::cout << "lower_bound(5): " << *it << "\n"; // 5

    std::reverse(v.begin(), v.end());
    std::cout << "Max: " << *std::max_element(v.begin(), v.end()) << "\n"; // 9

    std::vector<int> even;
    std::copy_if(v.begin(), v.end(), std::back_inserter(even),
                 [](int x){ return x % 2 == 0; });
    for (int x : even) std::cout << x << " "; // 8 6 4 2

    std::cout << "\nSorted? " << std::is_sorted(v.begin(), v.end()) << "\n"; // 0

    std::next_permutation(v.begin(), v.end());
    std::cout << "any_of > 8: " << std::any_of(v.begin(), v.end(), [](int x){ return x > 8; }) << "\n"; // 1
}
```

---

### `<functional>`

| Item | Description |
|---|---|
| `std::function<R(Args...)>` | Polymorphic callable wrapper |
| `std::bind(fn, args...)` | Bind arguments |
| `std::placeholders::_1, _2...` | Bind placeholders |
| `std::ref(x)` | Reference wrapper |
| `std::cref(x)` | Const reference wrapper |
| `std::plus<T>` | `a + b` |
| `std::minus<T>` | `a - b` |
| `std::multiplies<T>` | `a * b` |
| `std::divides<T>` | `a / b` |
| `std::modulus<T>` | `a % b` |
| `std::negate<T>` | `-a` |
| `std::equal_to<T>` | `a == b` |
| `std::not_equal_to<T>` | `a != b` |
| `std::less<T>` | `a < b` |
| `std::greater<T>` | `a > b` |
| `std::less_equal<T>` | `a <= b` |
| `std::greater_equal<T>` | `a >= b` |
| `std::logical_and<T>` | `a && b` |
| `std::logical_or<T>` | `a \|\| b` |
| `std::logical_not<T>` | `!a` |
| `std::not_fn(fn)` | Negate callable (C++17) |
| `std::mem_fn(&Class::method)` | Wrap member function |
| `std::hash<T>` | Hash functor |
| `std::invoke(fn, args...)` | Invoke callable (C++17) |

```cpp
#include <functional>
#include <algorithm>
#include <vector>
#include <iostream>

int add(int a, int b) { return a + b; }

int main() {
    std::function<int(int, int)> fn = add;
    std::cout << fn(3, 4) << "\n"; // 7

    auto add5 = std::bind(add, std::placeholders::_1, 5);
    std::cout << add5(10) << "\n"; // 15

    std::vector<int> v = {3, 1, 4, 1, 5};
    std::sort(v.begin(), v.end(), std::greater<int>());
    for (int x : v) std::cout << x << " "; // 5 4 3 1 1

    auto pred = std::not_fn([](int x){ return x > 3; });
    for (int x : v) if (pred(x)) std::cout << x << " "; // 3 1 1
}
```

---

### `<utility>`

| Item | Description |
|---|---|
| `std::pair<T1,T2>` | Pair of two values |
| `std::make_pair(a, b)` | Create pair |
| `p.first / p.second` | Access pair elements |
| `std::get<I>(p)` | Get by index |
| `std::swap(a, b)` | Swap values |
| `std::move(x)` | Cast to rvalue |
| `std::forward<T>(x)` | Perfect forwarding |
| `std::exchange(obj, new)` | Replace and return old (C++14) |
| `std::as_const(x)` | Const reference cast (C++17) |
| `std::to_underlying(e)` | Enum to underlying type (C++23) |
| `std::integer_sequence<T,...>` | Compile-time int sequence |
| `std::make_index_sequence<N>` | Index sequence 0..N-1 |
| `std::declval<T>()` | Unevaluated expression helper |
| `std::in_range<T>(n)` | Check range safety (C++20) |
| `std::cmp_less(a, b)` | Safe signed/unsigned compare (C++20) |

```cpp
#include <utility>
#include <iostream>

int main() {
    auto p = std::make_pair(42, "hello");
    std::cout << p.first << " " << p.second << "\n"; // 42 hello

    int a = 1, b = 2;
    std::swap(a, b);
    std::cout << a << " " << b << "\n"; // 2 1

    int old = std::exchange(a, 99);
    std::cout << "old: " << old << ", new: " << a << "\n"; // old: 2, new: 99

    std::string s = "move me";
    std::string s2 = std::move(s); // s is now empty
    std::cout << s2 << " | '" << s << "'\n"; // move me | ''
}
```

---

### `<tuple>`

| Item | Description |
|---|---|
| `std::tuple<T...>` | N-element heterogeneous tuple |
| `std::make_tuple(...)` | Create tuple |
| `std::get<I>(t)` | Get by index |
| `std::get<T>(t)` | Get by type (if unique) (C++14) |
| `std::tie(a,b,c)` | Unpack into variables |
| `std::ignore` | Ignore element in tie |
| `std::tuple_size<T>` | Number of elements |
| `std::tuple_element<I,T>` | Type of element I |
| `std::tuple_cat(t1, t2)` | Concatenate tuples |
| `std::apply(fn, t)` | Call fn with tuple args (C++17) |
| `std::make_from_tuple<T>(t)` | Construct T from tuple (C++17) |

```cpp
#include <tuple>
#include <iostream>

int main() {
    auto t = std::make_tuple(1, 3.14, std::string("hi"));
    std::cout << std::get<0>(t) << " " << std::get<1>(t) << " " << std::get<2>(t) << "\n";
    // 1 3.14 hi

    int x; double y; std::string z;
    std::tie(x, y, z) = t;
    std::cout << x << " " << y << " " << z << "\n"; // 1 3.14 hi

    auto t2 = std::tuple_cat(t, std::make_tuple(99, 'A'));
    std::cout << std::get<3>(t2) << "\n"; // 99

    std::apply([](auto... args){ ((std::cout << args << " "), ...); std::cout << "\n"; }, t);
}
```

---

### `<limits>`

| Item | Description |
|---|---|
| `std::numeric_limits<T>::min()` | Smallest value |
| `std::numeric_limits<T>::max()` | Largest value |
| `std::numeric_limits<T>::lowest()` | Most negative |
| `std::numeric_limits<T>::infinity()` | Float infinity |
| `std::numeric_limits<T>::quiet_NaN()` | NaN |
| `std::numeric_limits<T>::epsilon()` | Machine epsilon |
| `std::numeric_limits<T>::digits` | Mantissa digits |
| `std::numeric_limits<T>::digits10` | Decimal digits |
| `std::numeric_limits<T>::is_signed` | Is signed? |
| `std::numeric_limits<T>::is_integer` | Is integer? |
| `std::numeric_limits<T>::is_exact` | Exact representation? |
| `std::numeric_limits<T>::has_infinity` | Has infinity? |

```cpp
#include <limits>
#include <iostream>

int main() {
    std::cout << "int max: " << std::numeric_limits<int>::max() << "\n";       // 2147483647
    std::cout << "int min: " << std::numeric_limits<int>::min() << "\n";       // -2147483648
    std::cout << "long long max: " << std::numeric_limits<long long>::max() << "\n"; // 9223372036854775807
    std::cout << "double eps: " << std::numeric_limits<double>::epsilon() << "\n";
    std::cout << "float inf: " << std::numeric_limits<float>::infinity() << "\n";
    std::cout << "double NaN: " << std::numeric_limits<double>::quiet_NaN() << "\n";
}
```

---

### `<numeric>`

| Function | Description |
|---|---|
| `std::accumulate(first, last, init)` | Sum / fold |
| `std::accumulate(first, last, init, op)` | Custom fold |
| `std::reduce(first, last)` | Parallel-friendly accumulate (C++17) |
| `std::reduce(first, last, init, op)` | With init and op |
| `std::inner_product(f1,l1,f2,init)` | Dot product |
| `std::partial_sum(first, last, dest)` | Prefix sums |
| `std::exclusive_scan(...)` | Exclusive prefix sum (C++17) |
| `std::inclusive_scan(...)` | Inclusive prefix sum (C++17) |
| `std::adjacent_difference(f,l,dest)` | Differences between adjacent |
| `std::iota(first, last, val)` | Fill with incrementing values |
| `std::gcd(a, b)` | GCD (C++17) |
| `std::lcm(a, b)` | LCM (C++17) |
| `std::midpoint(a, b)` | Safe midpoint (C++20) |
| `std::lerp(a, b, t)` | Linear interpolation (C++20) |
| `std::transform_reduce(...)` | Map-reduce (C++17) |

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    int sum = std::accumulate(v.begin(), v.end(), 0);
    std::cout << "Sum: " << sum << "\n"; // 15

    int product = std::accumulate(v.begin(), v.end(), 1, std::multiplies<int>());
    std::cout << "Product: " << product << "\n"; // 120

    std::vector<int> ps;
    std::partial_sum(v.begin(), v.end(), std::back_inserter(ps));
    for (int x : ps) std::cout << x << " "; // 1 3 6 10 15

    std::vector<int> w(5);
    std::iota(w.begin(), w.end(), 10); // 10 11 12 13 14
    for (int x : w) std::cout << x << " ";

    std::cout << "\ngcd(12,8): " << std::gcd(12, 8) << "\n"; // 4
    std::cout << "lcm(4,6): " << std::lcm(4, 6) << "\n";    // 12
}
```

---

### `<iterator>`

| Item | Description |
|---|---|
| `std::back_inserter(c)` | Output iterator that push_backs |
| `std::front_inserter(c)` | Output iterator that push_fronts |
| `std::inserter(c, it)` | Output iterator that inserts |
| `std::make_move_iterator(it)` | Move-semantics wrapper |
| `std::advance(it, n)` | Advance iterator by n |
| `std::next(it, n=1)` | Return advanced copy |
| `std::prev(it, n=1)` | Return decremented copy |
| `std::distance(first, last)` | Distance between iterators |
| `std::begin(c) / std::end(c)` | Range begin/end |
| `std::rbegin(c) / std::rend(c)` | Reverse range |
| `std::cbegin(c) / std::cend(c)` | Const iterators |
| `std::istream_iterator<T>` | Read from stream |
| `std::ostream_iterator<T>` | Write to stream |
| `std::reverse_iterator<It>` | Reverse adapter |
| `std::iterator_traits<It>` | Iterator properties |
| `std::input_iterator_tag` | Iterator category tags |

```cpp
#include <iterator>
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v = {1, 2, 3};
    std::vector<int> v2;

    std::copy(v.begin(), v.end(), std::back_inserter(v2));

    auto it = v.begin();
    std::advance(it, 2);
    std::cout << *it << "\n"; // 3

    std::cout << std::distance(v.begin(), it) << "\n"; // 2

    // Read ints from stream
    // std::istream_iterator<int> in(std::cin), end;
    // std::copy(in, end, std::back_inserter(v));

    // Write to stream with separator
    std::copy(v.begin(), v.end(), std::ostream_iterator<int>(std::cout, " ")); // 1 2 3
}
```

---

## 🔹 4. Strings & Characters

---

### `<string>`

| Method/Function | Description |
|---|---|
| `s.length() / s.size()` | Length |
| `s.empty()` | Is empty? |
| `s.clear()` | Clear string |
| `s.push_back(c)` | Append char |
| `s.pop_back()` | Remove last char |
| `s.append(str)` | Append string |
| `s.append(n, c)` | Append n copies of char |
| `s += str` | Append |
| `s.insert(pos, str)` | Insert at position |
| `s.insert(it, c)` | Insert char at iterator |
| `s.erase(pos, len)` | Erase substring |
| `s.erase(it)` | Erase at iterator |
| `s.replace(pos, len, str)` | Replace portion |
| `s.substr(pos, len)` | Extract substring |
| `s.find(str, pos=0)` | Find first occurrence |
| `s.rfind(str, pos)` | Find last occurrence |
| `s.find_first_of(chars)` | First of any char |
| `s.find_last_of(chars)` | Last of any char |
| `s.find_first_not_of(chars)` | First not in set |
| `s.find_last_not_of(chars)` | Last not in set |
| `s.compare(str)` | Lexicographic compare |
| `s[i]` | Access char (unchecked) |
| `s.at(i)` | Access char (bounds-checked) |
| `s.front()` | First char |
| `s.back()` | Last char |
| `s.c_str()` | C-string pointer |
| `s.data()` | Non-const pointer (C++17) |
| `s.reserve(n)` | Reserve capacity |
| `s.shrink_to_fit()` | Release extra memory |
| `s.resize(n)` | Resize |
| `s.swap(s2)` | Swap |
| `std::to_string(val)` | Number to string |
| `std::stoi(str)` | String to int |
| `std::stol(str)` | String to long |
| `std::stoll(str)` | String to long long |
| `std::stod(str)` | String to double |
| `std::stof(str)` | String to float |
| `std::stoul(str)` | String to unsigned long |
| `std::stoull(str)` | String to unsigned long long |
| `std::string_literals::operator""s` | String literal suffix (C++14) |
| `std::string_view` | Non-owning string view (C++17) |
| `s.starts_with(str)` | Check prefix (C++20) |
| `s.ends_with(str)` | Check suffix (C++20) |
| `s.contains(str)` | Check substring (C++23) |

```cpp
#include <string>
#include <iostream>

int main() {
    std::string s = "Hello, World!";
    std::cout << s.substr(7, 5) << "\n"; // World
    std::cout << s.find("World") << "\n"; // 7
    s.replace(7, 5, "C++");
    std::cout << s << "\n"; // Hello, C++!

    std::string rev = s;
    std::reverse(rev.begin(), rev.end());
    std::cout << rev << "\n";

    std::cout << std::to_string(3.14) << "\n"; // 3.140000
    int n = std::stoi("42abc"); // stops at 'a'
    std::cout << n << "\n"; // 42

    std::cout << s.starts_with("Hello") << "\n"; // 1
}
```

---

### `<cstring>`

| Function | Description |
|---|---|
| `strlen(s)` | String length |
| `strcpy(dst, src)` | Copy string |
| `strncpy(dst, src, n)` | Copy n chars |
| `strcat(dst, src)` | Concatenate |
| `strncat(dst, src, n)` | Concatenate n chars |
| `strcmp(s1, s2)` | Compare strings |
| `strncmp(s1, s2, n)` | Compare n chars |
| `strcasecmp(s1, s2)` | Case-insensitive compare (POSIX) |
| `strchr(s, c)` | Find first char |
| `strrchr(s, c)` | Find last char |
| `strstr(s, sub)` | Find substring |
| `strpbrk(s, chars)` | Find first of set |
| `strspn(s, chars)` | Length of leading match |
| `strcspn(s, chars)` | Length until mismatch |
| `strtok(s, delim)` | Tokenize (modifies!) |
| `memcpy(dst, src, n)` | Copy n bytes |
| `memmove(dst, src, n)` | Copy n bytes (overlap safe) |
| `memset(dst, val, n)` | Set n bytes |
| `memcmp(s1, s2, n)` | Compare n bytes |
| `memchr(s, c, n)` | Find byte in memory |

```cpp
#include <cstring>
#include <cstdio>

int main() {
    char buf[50] = "Hello";
    strcat(buf, ", World!");
    printf("len=%zu, str=%s\n", strlen(buf), buf); // len=13, str=Hello, World!

    char* found = strstr(buf, "World");
    printf("Found: %s\n", found); // World!

    char copy[50];
    strcpy(copy, buf);

    // Tokenize
    char csv[] = "a,b,c,d";
    char* tok = strtok(csv, ",");
    while (tok) { printf("%s ", tok); tok = strtok(nullptr, ","); }
    // a b c d

    memset(copy, 0, sizeof(copy));
    printf("Cleared: %d\n", (int)strlen(copy)); // 0
}
```

---

### `<cctype>`

| Function | Description |
|---|---|
| `isalpha(c)` | Is letter? |
| `isdigit(c)` | Is digit? |
| `isalnum(c)` | Is letter or digit? |
| `isspace(c)` | Is whitespace? |
| `isupper(c)` | Is uppercase? |
| `islower(c)` | Is lowercase? |
| `ispunct(c)` | Is punctuation? |
| `isprint(c)` | Is printable? |
| `isgraph(c)` | Is printable (not space)? |
| `iscntrl(c)` | Is control char? |
| `isxdigit(c)` | Is hex digit? |
| `isblank(c)` | Is space or tab? |
| `toupper(c)` | Convert to uppercase |
| `tolower(c)` | Convert to lowercase |

```cpp
#include <cctype>
#include <string>
#include <iostream>

int main() {
    std::string s = "Hello World 123!";
    int letters = 0, digits = 0, spaces = 0;
    for (char c : s) {
        if (std::isalpha(c)) letters++;
        else if (std::isdigit(c)) digits++;
        else if (std::isspace(c)) spaces++;
    }
    std::cout << "Letters: " << letters << ", Digits: " << digits << ", Spaces: " << spaces << "\n";
    // Letters: 10, Digits: 3, Spaces: 2

    for (char& c : s) c = std::toupper(c);
    std::cout << s << "\n"; // HELLO WORLD 123!
}
```

---

## 🔹 5. Math & Numbers

---

### `<cmath>`

| Function | Description |
|---|---|
| `std::abs(x)` | Absolute value |
| `std::fabs(x)` | Absolute value (float) |
| `std::sqrt(x)` | Square root |
| `std::cbrt(x)` | Cube root (C++11) |
| `std::pow(x, y)` | x to the power y |
| `std::exp(x)` | e^x |
| `std::exp2(x)` | 2^x |
| `std::log(x)` | Natural log |
| `std::log2(x)` | Base-2 log |
| `std::log10(x)` | Base-10 log |
| `std::sin(x)` | Sine |
| `std::cos(x)` | Cosine |
| `std::tan(x)` | Tangent |
| `std::asin(x)` | Arc sine |
| `std::acos(x)` | Arc cosine |
| `std::atan(x)` | Arc tangent |
| `std::atan2(y, x)` | Arc tangent (y/x) |
| `std::sinh/cosh/tanh` | Hyperbolic functions |
| `std::ceil(x)` | Ceiling |
| `std::floor(x)` | Floor |
| `std::round(x)` | Round to nearest |
| `std::trunc(x)` | Truncate toward zero |
| `std::fmod(x, y)` | Floating point remainder |
| `std::remainder(x, y)` | IEEE remainder |
| `std::fma(x, y, z)` | Fused multiply-add |
| `std::hypot(x, y)` | sqrt(x²+y²) |
| `std::hypot(x, y, z)` | 3D hypotenuse (C++17) |
| `std::ldexp(x, exp)` | x * 2^exp |
| `std::frexp(x, &exp)` | Split into mantissa/exponent |
| `std::modf(x, &ipart)` | Split integer/fractional |
| `std::isinf(x)` | Is infinity? |
| `std::isnan(x)` | Is NaN? |
| `std::isfinite(x)` | Is finite? |
| `std::isnormal(x)` | Is normal (not denormal/0/inf/nan)? |
| `std::signbit(x)` | Is negative? |
| `std::copysign(x, y)` | Copy sign of y to x |
| `M_PI` | π (non-standard, widely available) |

```cpp
#include <cmath>
#include <iostream>

int main() {
    std::cout << std::sqrt(2.0) << "\n";         // 1.41421
    std::cout << std::pow(2.0, 10) << "\n";      // 1024
    std::cout << std::log2(1024) << "\n";         // 10
    std::cout << std::sin(M_PI / 6) << "\n";     // 0.5
    std::cout << std::atan2(1.0, 1.0) << "\n";  // pi/4 = 0.785398
    std::cout << std::ceil(3.2) << "\n";         // 4
    std::cout << std::floor(3.9) << "\n";        // 3
    std::cout << std::round(3.5) << "\n";        // 4
    std::cout << std::hypot(3.0, 4.0) << "\n";  // 5
    std::cout << std::fma(2.0, 3.0, 4.0) << "\n"; // 10 (2*3+4)
    std::cout << std::isnan(0.0/0.0) << "\n";   // 1
}
```

---

### `<complex>`

| Item | Description |
|---|---|
| `std::complex<T>` | Complex number type |
| `c.real()` | Real part |
| `c.imag()` | Imaginary part |
| `std::abs(c)` | Magnitude |
| `std::arg(c)` | Phase angle |
| `std::norm(c)` | Squared magnitude |
| `std::conj(c)` | Conjugate |
| `std::polar(r, theta)` | Create from polar |
| `std::exp/log/sqrt/pow(c)` | Complex math |
| `std::sin/cos/tan(c)` | Complex trig |
| `+, -, *, /` | Arithmetic operators |
| `==, !=` | Comparison |
| Literals `1.0if, 1.0i, 1.0il` | Complex literals (C++14) |

```cpp
#include <complex>
#include <iostream>

int main() {
    using cd = std::complex<double>;
    cd a(3.0, 4.0), b(1.0, -2.0);

    std::cout << "a = " << a << "\n";          // (3,4)
    std::cout << "|a| = " << std::abs(a) << "\n";  // 5
    std::cout << "conj(a) = " << std::conj(a) << "\n"; // (3,-4)
    std::cout << "a * b = " << a * b << "\n";      // (11,-2)
    std::cout << "sqrt(a) = " << std::sqrt(a) << "\n";
    std::cout << "exp(i*pi) = " << std::exp(cd(0, M_PI)) << "\n"; // (-1,~0)
}
```

---

### `<random>`

| Item | Description |
|---|---|
| `std::mt19937` | Mersenne Twister (32-bit) |
| `std::mt19937_64` | Mersenne Twister (64-bit) |
| `std::random_device` | Hardware/OS entropy |
| `std::default_random_engine` | Implementation-defined engine |
| `std::minstd_rand` | Linear congruential |
| `engine.seed(val)` | Set seed |
| `engine()` | Generate raw value |
| `std::uniform_int_distribution<T>` | Uniform integer range |
| `std::uniform_real_distribution<T>` | Uniform real range |
| `std::normal_distribution<T>` | Gaussian (mean, stddev) |
| `std::bernoulli_distribution` | Bool with probability p |
| `std::binomial_distribution<T>` | Binomial |
| `std::poisson_distribution<T>` | Poisson |
| `std::exponential_distribution<T>` | Exponential |
| `std::discrete_distribution<T>` | Weighted discrete |
| `std::gamma_distribution<T>` | Gamma |
| `std::cauchy_distribution<T>` | Cauchy |
| `dist(engine)` | Generate sample |
| `dist.min() / dist.max()` | Range |
| `dist.reset()` | Reset state |

```cpp
#include <random>
#include <iostream>
#include <map>

int main() {
    std::mt19937 rng(std::random_device{}());

    std::uniform_int_distribution<int> dice(1, 6);
    std::map<int, int> freq;
    for (int i = 0; i < 6000; i++) freq[dice(rng)]++;
    for (auto& [k, v] : freq) std::cout << k << ": " << v << "\n"; // ~1000 each

    std::normal_distribution<double> gauss(0.0, 1.0);
    double sample = gauss(rng);
    std::cout << "Normal sample: " << sample << "\n";

    std::bernoulli_distribution coin(0.5);
    std::cout << "Coin flip: " << (coin(rng) ? "H" : "T") << "\n";
}
```

---

### `<ratio>`

| Item | Description |
|---|---|
| `std::ratio<Num, Den>` | Compile-time rational number |
| `std::ratio_add<R1, R2>` | R1 + R2 |
| `std::ratio_subtract<R1, R2>` | R1 - R2 |
| `std::ratio_multiply<R1, R2>` | R1 * R2 |
| `std::ratio_divide<R1, R2>` | R1 / R2 |
| `std::ratio_equal<R1, R2>` | R1 == R2 |
| `std::ratio_less<R1, R2>` | R1 < R2 |
| `r::num / r::den` | Access numerator/denominator |
| Predefined: `std::kilo, std::mega, std::milli, std::micro...` | SI prefixes |

```cpp
#include <ratio>
#include <iostream>

int main() {
    using third = std::ratio<1, 3>;
    using sixth = std::ratio<1, 6>;
    using sum = std::ratio_add<third, sixth>; // 1/3 + 1/6 = 1/2

    std::cout << sum::num << "/" << sum::den << "\n"; // 1/2

    std::cout << std::kilo::num << "\n"; // 1000
    std::cout << std::milli::den << "\n"; // 1000

    std::cout << std::ratio_less<sixth, third>::value << "\n"; // 1 (true)
}
```

---

## 🔹 6. Time & Date

---

### `<ctime>`

| Function/Type | Description |
|---|---|
| `std::time(nullptr)` | Current time as time_t |
| `std::time_t` | Calendar time type (seconds) |
| `std::clock()` | CPU ticks since start |
| `CLOCKS_PER_SEC` | Ticks per second |
| `std::difftime(t2, t1)` | Difference in seconds |
| `std::localtime(&t)` | Convert to local tm struct |
| `std::gmtime(&t)` | Convert to UTC tm struct |
| `std::mktime(&tm)` | tm to time_t |
| `std::strftime(buf, n, fmt, tm)` | Format time as string |
| `std::asctime(&tm)` | tm to C-string |
| `std::ctime(&t)` | time_t to C-string |
| `struct tm` | Broken-down time struct (sec, min, hour, mday, mon, year, wday, yday, isdst) |

```cpp
#include <ctime>
#include <cstdio>

int main() {
    std::time_t now = std::time(nullptr);
    std::tm* lt = std::localtime(&now);

    char buf[100];
    std::strftime(buf, sizeof(buf), "%Y-%m-%d %H:%M:%S", lt);
    printf("Now: %s\n", buf); // e.g. 2025-05-06 15:30:00

    printf("Weekday: %d\n", lt->tm_wday); // 0=Sun
    printf("Day of year: %d\n", lt->tm_yday);

    std::clock_t start = std::clock();
    volatile long sum = 0;
    for (int i = 0; i < 1000000; i++) sum += i;
    double ms = 1000.0 * (std::clock() - start) / CLOCKS_PER_SEC;
    printf("Elapsed: %.2f ms\n", ms);
}
```

---

### `<chrono>`

| Item | Description |
|---|---|
| `std::chrono::system_clock::now()` | Wall clock time |
| `std::chrono::steady_clock::now()` | Monotonic clock |
| `std::chrono::high_resolution_clock::now()` | Highest precision |
| `std::chrono::duration<Rep, Period>` | Duration type |
| `std::chrono::nanoseconds/microseconds/milliseconds/seconds/minutes/hours` | Duration types |
| `std::chrono::duration_cast<To>(d)` | Convert duration |
| `std::chrono::time_point<C, D>` | Point in time |
| `t2 - t1` | Duration between time points |
| `d.count()` | Numeric value of duration |
| `std::chrono::days/weeks/months/years` | C++20 duration types |
| `std::chrono::year_month_day` | Calendar type (C++20) |
| `std::chrono::zoned_time` | Time with timezone (C++20) |
| Duration literals: `1s, 1ms, 1us, 1ns, 1min, 1h` | (C++14, `using namespace std::chrono_literals`) |

```cpp
#include <chrono>
#include <iostream>
#include <thread>

int main() {
    using namespace std::chrono;
    using namespace std::chrono_literals;

    auto start = steady_clock::now();
    std::this_thread::sleep_for(50ms);
    auto end = steady_clock::now();

    auto elapsed = duration_cast<microseconds>(end - start);
    std::cout << "Elapsed: " << elapsed.count() << " us\n"; // ~50000 us

    auto now = system_clock::now();
    auto secs = duration_cast<seconds>(now.time_since_epoch());
    std::cout << "Unix time: " << secs.count() << "\n";

    duration<double> d = 2.5s;
    std::cout << d.count() << "s\n"; // 2.5
}
```

---

## 🔹 7. File Handling

---

### `<fstream>`

| Item | Description |
|---|---|
| `std::ifstream` | Input file stream |
| `std::ofstream` | Output file stream |
| `std::fstream` | Bidirectional file stream |
| `f.open(path, mode)` | Open file |
| `f.close()` | Close file |
| `f.is_open()` | Is file open? |
| `f.good() / fail() / bad() / eof()` | State checks |
| `f.clear()` | Clear error flags |
| `f >> val` | Read formatted |
| `f << val` | Write formatted |
| `f.get(c)` | Read char |
| `f.getline(buf, n)` | Read line into C-string |
| `std::getline(f, str)` | Read line into std::string |
| `f.read(buf, n)` | Binary read |
| `f.write(buf, n)` | Binary write |
| `f.seekg(pos)` | Set read position |
| `f.seekp(pos)` | Set write position |
| `f.tellg()` | Get read position |
| `f.tellp()` | Get write position |
| `f.flush()` | Flush buffer |
| Open modes: `ios::in, out, app, ate, binary, trunc` | |

```cpp
#include <fstream>
#include <string>
#include <iostream>

int main() {
    // Write
    std::ofstream ofs("test.txt");
    ofs << "Line 1\nLine 2\nLine 3\n";
    ofs.close();

    // Read line by line
    std::ifstream ifs("test.txt");
    std::string line;
    while (std::getline(ifs, line)) {
        std::cout << "> " << line << "\n";
    }

    // Get file size
    ifs.clear();
    ifs.seekg(0, std::ios::end);
    std::cout << "File size: " << ifs.tellg() << " bytes\n";

    // Binary read/write
    std::ofstream bin("data.bin", std::ios::binary);
    int arr[] = {1, 2, 3, 4, 5};
    bin.write(reinterpret_cast<char*>(arr), sizeof(arr));
    bin.close();

    std::ifstream bin2("data.bin", std::ios::binary);
    int readback[5];
    bin2.read(reinterpret_cast<char*>(readback), sizeof(readback));
    for (int x : readback) std::cout << x << " "; // 1 2 3 4 5
}
```

---

### `<sstream>`

| Item | Description |
|---|---|
| `std::istringstream` | Read from string |
| `std::ostringstream` | Write to string |
| `std::stringstream` | Bidirectional |
| `ss.str()` | Get/set string content |
| `ss.str(s)` | Set content |
| `ss >> val` | Extract value |
| `ss << val` | Insert value |
| `ss.clear()` | Clear error state |
| `std::getline(ss, s)` | Read line |
| All istream/ostream methods | Inherited |

```cpp
#include <sstream>
#include <string>
#include <vector>
#include <iostream>

int main() {
    // Build string
    std::ostringstream oss;
    oss << "Hello" << " " << 2025 << " " << 3.14;
    std::string s = oss.str();
    std::cout << s << "\n"; // Hello 2025 3.14

    // Parse string
    std::istringstream iss(s);
    std::string word; int year; double pi;
    iss >> word >> year >> pi;
    std::cout << word << " " << year << " " << pi << "\n";

    // Split by delimiter
    std::string csv = "alpha,beta,gamma,delta";
    std::istringstream ss(csv);
    std::vector<std::string> tokens;
    std::string tok;
    while (std::getline(ss, tok, ',')) tokens.push_back(tok);
    for (auto& t : tokens) std::cout << t << " "; // alpha beta gamma delta
}
```

---

## 🔹 8. Miscellaneous

---

### `<bitset>`

| Method | Description |
|---|---|
| `bs[i]` | Access bit i |
| `bs.set()` | Set all bits |
| `bs.set(i)` | Set bit i |
| `bs.reset()` | Clear all bits |
| `bs.reset(i)` | Clear bit i |
| `bs.flip()` | Toggle all bits |
| `bs.flip(i)` | Toggle bit i |
| `bs.test(i)` | Test bit i (bounds-checked) |
| `bs.any()` | Any bit set? |
| `bs.all()` | All bits set? |
| `bs.none()` | No bits set? |
| `bs.count()` | Count set bits |
| `bs.size()` | Total bits |
| `bs.to_ulong()` | Convert to unsigned long |
| `bs.to_ullong()` | Convert to unsigned long long |
| `bs.to_string()` | Convert to string |
| `&, \|, ^, ~, <<, >>` | Bitwise operators |

```cpp
#include <bitset>
#include <iostream>

int main() {
    std::bitset<8> b(0b10110100);
    std::cout << b << "\n";               // 10110100
    std::cout << b.count() << "\n";       // 4 (set bits)
    b.flip(0);
    std::cout << b.to_string() << "\n";   // 10110101
    std::cout << b.to_ulong() << "\n";    // 181

    std::bitset<8> mask(0b00001111);
    std::cout << (b & mask) << "\n";      // 00000101
}
```

---

### `<cassert>`

| Macro | Description |
|---|---|
| `assert(condition)` | Abort if condition is false |
| `NDEBUG` | Define to disable all asserts |
| `static_assert(cond, msg)` | Compile-time assert (C++11, in `<type_traits>`) |

```cpp
#include <cassert>
#include <iostream>

int divide(int a, int b) {
    assert(b != 0); // Program aborts if b == 0
    return a / b;
}

int main() {
    std::cout << divide(10, 2) << "\n"; // 5
    // divide(10, 0); // would abort with assertion failure

    static_assert(sizeof(int) >= 4, "int must be at least 4 bytes");
    std::cout << "Assertions passed\n";
}
```

---

### `<exception>`

| Item | Description |
|---|---|
| `std::exception` | Base class for all exceptions |
| `e.what()` | Error message |
| `std::terminate()` | Terminate program |
| `std::set_terminate(fn)` | Set terminate handler |
| `std::terminate_handler` | Function pointer type |
| `std::uncaught_exceptions()` | Count of uncaught exceptions (C++17) |
| `std::current_exception()` | Get current exception ptr |
| `std::rethrow_exception(ptr)` | Re-throw from exception_ptr |
| `std::make_exception_ptr(e)` | Create exception_ptr |
| `std::exception_ptr` | Opaque exception pointer type |
| `std::nested_exception` | Wraps nested exception |
| `std::throw_with_nested(e)` | Throw with nesting |
| `std::rethrow_if_nested(e)` | Re-throw nested |

```cpp
#include <exception>
#include <iostream>

int main() {
    std::set_terminate([](){
        std::cout << "Custom terminate called\n";
        std::abort();
    });

    try {
        throw std::exception();
    } catch (const std::exception& e) {
        std::cout << "Caught: " << e.what() << "\n"; // std::exception

        auto ptr = std::current_exception();
        std::cout << "Has exception_ptr: " << (bool)ptr << "\n"; // 1
    }
}
```

---

### `<stdexcept>`

| Exception Class | Description |
|---|---|
| `std::logic_error` | Logic errors (programming bugs) |
| `std::invalid_argument` | Invalid function argument |
| `std::domain_error` | Math domain error |
| `std::length_error` | Exceeds max length |
| `std::out_of_range` | Index out of range |
| `std::runtime_error` | Runtime errors |
| `std::range_error` | Range error |
| `std::overflow_error` | Arithmetic overflow |
| `std::underflow_error` | Arithmetic underflow |
| All inherit from `std::exception` | Use `.what()` for message |

```cpp
#include <stdexcept>
#include <iostream>
#include <vector>

double safeDivide(double a, double b) {
    if (b == 0) throw std::invalid_argument("Division by zero");
    return a / b;
}

int main() {
    try {
        std::vector<int> v = {1, 2, 3};
        std::cout << v.at(10) << "\n"; // throws out_of_range
    } catch (const std::out_of_range& e) {
        std::cout << "Out of range: " << e.what() << "\n";
    }

    try {
        safeDivide(5, 0);
    } catch (const std::invalid_argument& e) {
        std::cout << "Invalid arg: " << e.what() << "\n";
    }

    try {
        throw std::runtime_error("Something went wrong");
    } catch (const std::exception& e) { // catch all
        std::cout << "Exception: " << e.what() << "\n";
    }
}
```

---

### `<typeinfo>`

| Item | Description |
|---|---|
| `typeid(expr)` | Get type_info |
| `typeid(Type)` | Get type_info for type |
| `ti.name()` | Mangled type name |
| `ti == ti2` | Same type? |
| `ti != ti2` | Different type? |
| `ti.before(ti2)` | Ordering |
| `ti.hash_code()` | Hash of type (C++11) |
| `std::type_info` | Type info class |
| `std::bad_typeid` | Exception from null typeid |
| `std::type_index` | Hashable type wrapper (C++11) |

```cpp
#include <typeinfo>
#include <iostream>
#include <map>

int main() {
    int x = 5;
    double y = 3.14;
    std::string s = "hi";

    std::cout << typeid(x).name() << "\n";   // i (int)
    std::cout << typeid(y).name() << "\n";   // d (double)
    std::cout << typeid(s).name() << "\n";   // NSt...

    std::cout << (typeid(x) == typeid(int)) << "\n"; // 1
    std::cout << (typeid(x) == typeid(y)) << "\n";   // 0

    // Polymorphism
    struct Base { virtual ~Base() {} };
    struct Derived : Base {};
    Base* p = new Derived();
    std::cout << typeid(*p).name() << "\n"; // Derived
    delete p;
}
```

---

### `<memory>`

| Item | Description |
|---|---|
| `std::unique_ptr<T>` | Unique ownership smart pointer |
| `std::make_unique<T>(...)` | Create unique_ptr (C++14) |
| `std::shared_ptr<T>` | Shared ownership smart pointer |
| `std::make_shared<T>(...)` | Create shared_ptr |
| `std::weak_ptr<T>` | Non-owning observer |
| `p.get()` | Raw pointer |
| `p.reset(ptr)` | Release and replace |
| `p.release()` | Release ownership (unique_ptr) |
| `p.use_count()` | Reference count (shared_ptr) |
| `p.unique()` | Is only owner? (deprecated C++20) |
| `p.expired()` | Is weak_ptr expired? |
| `p.lock()` | weak_ptr to shared_ptr |
| `std::enable_shared_from_this<T>` | Get shared_ptr from this |
| `std::allocator<T>` | Default allocator |
| `std::allocate_shared<T>(alloc, ...)` | Shared ptr with allocator |
| `std::static_pointer_cast<T>(sp)` | Static cast shared_ptr |
| `std::dynamic_pointer_cast<T>(sp)` | Dynamic cast shared_ptr |
| `std::const_pointer_cast<T>(sp)` | Const cast shared_ptr |
| `std::addressof(obj)` | True address (even if & overloaded) |
| `std::uninitialized_copy/fill/...` | Uninitialized memory ops |
| `std::destroy(first, last)` | Destroy range (C++17) |
| `std::construct_at(ptr, ...)` | Construct at ptr (C++20) |

```cpp
#include <memory>
#include <iostream>

struct Node {
    int val;
    std::shared_ptr<Node> next;
    Node(int v) : val(v) { std::cout << "Node(" << v << ") created\n"; }
    ~Node() { std::cout << "Node(" << val << ") destroyed\n"; }
};

int main() {
    // unique_ptr: single owner
    auto u = std::make_unique<Node>(1);
    std::cout << u->val << "\n";
    // auto u2 = u; // ERROR: can't copy

    // shared_ptr: shared ownership
    auto s1 = std::make_shared<Node>(2);
    auto s2 = s1;
    std::cout << "use_count: " << s1.use_count() << "\n"; // 2

    // weak_ptr: no ownership
    std::weak_ptr<Node> w = s1;
    if (auto locked = w.lock()) std::cout << "weak lock ok: " << locked->val << "\n";
    s1.reset(); s2.reset(); // Node(2) destroyed
    std::cout << "expired: " << w.expired() << "\n"; // 1
}
```

---

### `<thread>`

| Item | Description |
|---|---|
| `std::thread t(fn, args...)` | Create thread |
| `t.join()` | Wait for thread to finish |
| `t.detach()` | Detach thread |
| `t.joinable()` | Can be joined? |
| `t.get_id()` | Thread ID |
| `std::this_thread::get_id()` | Current thread ID |
| `std::this_thread::sleep_for(dur)` | Sleep for duration |
| `std::this_thread::sleep_until(tp)` | Sleep until time point |
| `std::this_thread::yield()` | Yield to scheduler |
| `std::thread::hardware_concurrency()` | Number of CPU cores |
| `std::jthread` | Joinable thread with stop token (C++20) |
| `t.request_stop()` | Request stop (jthread, C++20) |

```cpp
#include <thread>
#include <iostream>
#include <vector>

void worker(int id, int n) {
    for (int i = 0; i < n; i++) {
        // std::cout is not thread-safe without mutex but ok for demo
        std::this_thread::sleep_for(std::chrono::milliseconds(10));
    }
    std::cout << "Thread " << id << " done\n";
}

int main() {
    std::cout << "CPU cores: " << std::thread::hardware_concurrency() << "\n";

    std::vector<std::thread> threads;
    for (int i = 0; i < 4; i++)
        threads.emplace_back(worker, i, 3);

    for (auto& t : threads) t.join();
    std::cout << "All done\n";
}
```

---

### `<mutex>`

| Item | Description |
|---|---|
| `std::mutex` | Basic mutual exclusion |
| `m.lock()` | Acquire lock (blocks) |
| `m.unlock()` | Release lock |
| `m.try_lock()` | Try to acquire (non-blocking) |
| `std::recursive_mutex` | Same thread can lock multiple times |
| `std::timed_mutex` | Lock with timeout |
| `m.try_lock_for(dur)` | Try lock for duration |
| `m.try_lock_until(tp)` | Try lock until time point |
| `std::lock_guard<M>` | RAII lock (no unlock needed) |
| `std::unique_lock<M>` | Flexible RAII lock |
| `std::scoped_lock<M...>` | Multi-mutex RAII lock (C++17) |
| `std::lock(m1, m2)` | Lock multiple (deadlock-free) |
| `std::once_flag` | Used with call_once |
| `std::call_once(flag, fn)` | Execute once across threads |
| `std::shared_mutex` | Read-write lock (C++17) |
| `std::shared_lock<M>` | Shared (reader) lock (C++17) |

```cpp
#include <mutex>
#include <thread>
#include <iostream>
#include <vector>

std::mutex mtx;
int counter = 0;

void increment(int n) {
    for (int i = 0; i < n; i++) {
        std::lock_guard<std::mutex> lock(mtx); // auto unlock on scope exit
        counter++;
    }
}

int main() {
    std::vector<std::thread> threads;
    for (int i = 0; i < 4; i++)
        threads.emplace_back(increment, 1000);
    for (auto& t : threads) t.join();

    std::cout << "Counter: " << counter << "\n"; // 4000

    // call_once example
    std::once_flag flag;
    for (int i = 0; i < 3; i++)
        std::call_once(flag, [](){ std::cout << "Initialized once\n"; });
}
```

---

### `<future>`

| Item | Description |
|---|---|
| `std::async(policy, fn, args...)` | Run async task |
| `std::launch::async` | New thread |
| `std::launch::deferred` | Lazy evaluation |
| `std::future<T>` | Future result |
| `f.get()` | Get result (blocks) |
| `f.wait()` | Wait for result |
| `f.wait_for(dur)` | Wait with timeout |
| `f.wait_until(tp)` | Wait until time point |
| `f.valid()` | Has shared state? |
| `std::promise<T>` | Manually set future value |
| `p.set_value(val)` | Set the value |
| `p.set_exception(ptr)` | Set exception |
| `p.get_future()` | Get associated future |
| `std::packaged_task<Sig>` | Wrap callable for future |
| `task.get_future()` | Get future |
| `task(args...)` | Execute task |
| `std::future_status::ready/timeout/deferred` | Wait status |
| `std::shared_future<T>` | Shareable future |

```cpp
#include <future>
#include <iostream>
#include <numeric>
#include <vector>

long long sum_range(int lo, int hi) {
    long long s = 0;
    for (int i = lo; i <= hi; i++) s += i;
    return s;
}

int main() {
    auto f1 = std::async(std::launch::async, sum_range, 1, 500000);
    auto f2 = std::async(std::launch::async, sum_range, 500001, 1000000);

    long long total = f1.get() + f2.get();
    std::cout << "Sum 1..1000000 = " << total << "\n"; // 500000500000

    // Promise/future
    std::promise<int> p;
    std::future<int> fut = p.get_future();
    std::thread t([&p](){ p.set_value(42); });
    std::cout << "Promise result: " << fut.get() << "\n"; // 42
    t.join();
}
```

---

### `<condition_variable>`

| Item | Description |
|---|---|
| `std::condition_variable` | Condition variable (works with unique_lock) |
| `cv.wait(lock)` | Wait (releases lock, re-acquires on wake) |
| `cv.wait(lock, pred)` | Wait with spurious-wakeup protection |
| `cv.wait_for(lock, dur)` | Wait with timeout |
| `cv.wait_until(lock, tp)` | Wait until time point |
| `cv.notify_one()` | Wake one waiting thread |
| `cv.notify_all()` | Wake all waiting threads |
| `std::condition_variable_any` | Works with any lockable |
| `std::cv_status::no_timeout` | Wait status: woken |
| `std::cv_status::timeout` | Wait status: timed out |
| `std::notify_all_at_thread_exit(cv, lock)` | Notify on exit |

```cpp
#include <condition_variable>
#include <mutex>
#include <thread>
#include <queue>
#include <iostream>

std::mutex mtx;
std::condition_variable cv;
std::queue<int> buffer;
bool done = false;

void producer() {
    for (int i = 0; i < 5; i++) {
        std::this_thread::sleep_for(std::chrono::milliseconds(10));
        { std::lock_guard<std::mutex> lk(mtx); buffer.push(i); }
        cv.notify_one();
    }
    { std::lock_guard<std::mutex> lk(mtx); done = true; }
    cv.notify_all();
}

void consumer() {
    while (true) {
        std::unique_lock<std::mutex> lk(mtx);
        cv.wait(lk, []{ return !buffer.empty() || done; });
        while (!buffer.empty()) {
            std::cout << "Got: " << buffer.front() << "\n";
            buffer.pop();
        }
        if (done) break;
    }
}

int main() {
    std::thread p(producer), c(consumer);
    p.join(); c.join();
}
```

---

*Reference covers C++11 through C++23. Some features require specific standard flags, e.g. `-std=c++17` or `-std=c++20`.*
