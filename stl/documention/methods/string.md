# C++ `std::string` STL Methods — Complete Reference with Examples

---

## 1. Capacity

### `size()` / `length()`
```cpp
string s = "hello";
cout << s.size();    // 5
cout << s.length();  // 5
```

### `empty()`
```cpp
string s = "";
cout << s.empty();  // 1 (true)
string t = "hi";
cout << t.empty();  // 0 (false)
```

### `capacity()`
```cpp
string s = "hello";
cout << s.capacity();  // >= 5
```

### `max_size()`
```cpp
string s;
cout << s.max_size();  // platform-defined maximum
```

### `resize()`
```cpp
string s = "hello";
s.resize(3);
cout << s;  // hel
s.resize(6, '!');
cout << s;  // hel!!!
```

### `reserve()`
```cpp
string s;
s.reserve(100);
cout << s.capacity();  // >= 100
```

### `shrink_to_fit()`
```cpp
string s = "hi";
s.reserve(100);
s.shrink_to_fit();
cout << s.capacity();  // ~2
```

---

## 2. Element Access

### `operator[]`
```cpp
string s = "hello";
cout << s[1];  // e
```

### `at()`
```cpp
string s = "hello";
cout << s.at(0);  // h
// s.at(10);      // throws std::out_of_range
```

### `front()`
```cpp
string s = "hello";
cout << s.front();  // h
```

### `back()`
```cpp
string s = "hello";
cout << s.back();  // o
```

### `c_str()` / `data()`
```cpp
string s = "hello";
const char* p = s.c_str();
printf("%s", p);  // hello
```

---

## 3. Modifiers

### `append()`
```cpp
string s = "hello";
s.append(" world");
cout << s;  // hello world
```

### `operator+=`
```cpp
string s = "foo";
s += "bar";
cout << s;  // foobar
```

### `push_back()`
```cpp
string s = "hell";
s.push_back('o');
cout << s;  // hello
```

### `pop_back()`
```cpp
string s = "hello";
s.pop_back();
cout << s;  // hell
```

### `insert()`
```cpp
string s = "helo";
s.insert(3, "l");
cout << s;  // hello
```

### `erase()`
```cpp
string s = "hello world";
s.erase(5, 6);  // pos, count
cout << s;      // hello
```

### `replace()`
```cpp
string s = "hello world";
s.replace(6, 5, "C++");
cout << s;  // hello C++
```

### `assign()`
```cpp
string s = "hello";
s.assign("world");
cout << s;  // world
```

### `clear()`
```cpp
string s = "hello";
s.clear();
cout << s.empty();  // 1
```

### `swap()`
```cpp
string a = "foo", b = "bar";
a.swap(b);
cout << a << " " << b;  // bar foo
```

---

## 4. Search

### `find()`
```cpp
string s = "hello world";
cout << s.find("world");  // 6
cout << s.find("xyz");    // string::npos
```

### `rfind()`
```cpp
string s = "abcabc";
cout << s.rfind("bc");  // 4
```

### `find_first_of()`
```cpp
string s = "hello";
cout << s.find_first_of("aeiou");  // 1  (finds 'e')
```

### `find_last_of()`
```cpp
string s = "hello";
cout << s.find_last_of("aeiou");  // 4  (finds 'o')
```

### `find_first_not_of()`
```cpp
string s = "   hello";
cout << s.find_first_not_of(' ');  // 3
```

### `find_last_not_of()`
```cpp
string s = "hello   ";
cout << s.find_last_not_of(' ');  // 4
```

---

## 5. Substrings & Compare

### `substr()`
```cpp
string s = "hello world";
cout << s.substr(6);     // world
cout << s.substr(0, 5);  // hello
```

### `compare()`
```cpp
string a = "abc", b = "abd";
cout << a.compare(b);  // < 0  (a comes before b)
cout << a.compare(a);  // 0   (equal)
cout << b.compare(a);  // > 0  (b comes after a)
```

---

## 6. Iterators

### `begin()` / `end()`
```cpp
string s = "hello";
for (auto it = s.begin(); it != s.end(); ++it)
    cout << *it;  // hello
```

### `rbegin()` / `rend()`
```cpp
string s = "hello";
for (auto it = s.rbegin(); it != s.rend(); ++it)
    cout << *it;  // olleh
```

### `cbegin()` / `cend()`
```cpp
string s = "hello";
for (auto it = s.cbegin(); it != s.cend(); ++it)
    cout << *it;  // hello (read-only)
```

---

## 7. Non-member / Global Functions

### `operator+`
```cpp
string a = "hello", b = " world";
string c = a + b;
cout << c;  // hello world
```

### `getline()`
```cpp
string s;
getline(cin, s);
cout << s;  // reads the full line including spaces
```

### `stoi()` / `stod()` / `stol()`
```cpp
string s = "42";
int n = stoi(s);
cout << n + 1;       // 43

double d = stod("3.14");
cout << d;           // 3.14

long l = stol("100000");
cout << l;           // 100000
```

### `to_string()`
```cpp
int n = 42;
string s = to_string(n);
cout << s + "!";  // 42!
```

---

> **Tip:** Always `#include <string>` (included via `<bits/stdc++.h>` in competitive programming).  
> Use `string::npos` to check if `find()` / `rfind()` failed: `if (s.find("x") == string::npos) { ... }`
