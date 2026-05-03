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















Handling “other symbols” (special characters) in C++ strings is very common in competitive programming (CP). The trick is to **understand how C++ treats characters + use the right STL tools**.

Let’s go step-by-step with **practical CP tricks** 👇

---

# 🔹 1. What are “other symbols”?

These include:

```
! @ # $ % ^ & * ( ) _ + - = { } [ ] | \ : ; " ' < > , . ? / ~
```

Also:

* whitespace → `' '`, `'\n'`, `'\t'`
* digits → `'0'–'9'`
* letters → `'a-z', 'A-Z'`

---

# 🔹 2. Check character type (MOST IMPORTANT)

Use `<cctype>` functions:

```cpp
#include <cctype>

char c = s[i];

if (isalpha(c))   // a-z, A-Z
if (isdigit(c))   // 0-9
if (isalnum(c))   // letter or digit
if (isspace(c))   // space, newline, tab
if (ispunct(c))   // SPECIAL SYMBOLS (!! important)
```

✅ **CP Trick:**

```cpp
if (!isalnum(c)) {
    // this is a symbol
}
```

---

# 🔹 3. Loop through string safely

```cpp
for (char c : s) {
    if (ispunct(c)) {
        cout << c << " ";
    }
}
```

---

# 🔹 4. Remove all special characters

```cpp
string clean = "";

for (char c : s) {
    if (isalnum(c)) clean += c;
}
```

---

# 🔹 5. Replace symbols

Example: replace all symbols with space

```cpp
for (char &c : s) {
    if (!isalnum(c)) c = ' ';
}
```

---

# 🔹 6. Count frequency of symbols

```cpp
map<char, int> freq;

for (char c : s) {
    if (ispunct(c)) freq[c]++;
}
```

---

# 🔹 7. Fast trick using ASCII (VERY IMPORTANT in CP)

ASCII ranges:

```
'a'–'z' → 97–122  
'A'–'Z' → 65–90  
'0'–'9' → 48–57  
```

### Detect symbol using ASCII:

```cpp
if (!( (c >= 'a' && c <= 'z') ||
       (c >= 'A' && c <= 'Z') ||
       (c >= '0' && c <= '9') )) {
    // symbol
}
```

⚡ Faster than `isalnum()` in some cases.

---

# 🔹 8. Handle input with spaces & symbols

### ❌ Wrong:

```cpp
cin >> s;  // stops at space
```

### ✅ Correct:

```cpp
getline(cin, s);
```

---

# 🔹 9. Escape characters (VERY IMPORTANT)

Some symbols need escaping:

```cpp
string s = "He said \"Hello\"";
string path = "C:\\Users\\Name";
```

| Symbol  | Use  |
| ------- | ---- |
| `"`     | `\"` |
| `\`     | `\\` |
| newline | `\n` |
| tab     | `\t` |

---

# 🔹 10. Remove specific symbols (CP trick)

```cpp
s.erase(remove(s.begin(), s.end(), '#'), s.end());
```

Remove multiple:

```cpp
string res;
for (char c : s) {
    if (c != '#' && c != '@') res += c;
}
```

---

# 🔹 11. Regex (rare in CP, but powerful)

```cpp
#include <regex>

s = regex_replace(s, regex("[^a-zA-Z0-9]"), "");
```

⚠️ Slower → avoid in contests unless needed.

---

# 🔹 12. Convert case ignoring symbols

```cpp
for (char &c : s) {
    if (isalpha(c)) c = tolower(c);
}
```

---

# 🔹 13. Split string by symbols

```cpp
string temp = "";
vector<string> words;

for (char c : s) {
    if (isalnum(c)) temp += c;
    else {
        if (!temp.empty()) words.push_back(temp);
        temp = "";
    }
}
if (!temp.empty()) words.push_back(temp);
```

---

# 🔹 14. Most useful CP patterns

### ✅ Pattern 1: Clean string

```cpp
string clean;
for (char c : s)
    if (isalnum(c)) clean += tolower(c);
```

---

### ✅ Pattern 2: Palindrome ignoring symbols

```cpp
string t;
for (char c : s)
    if (isalnum(c)) t += tolower(c);

string rev = t;
reverse(rev.begin(), rev.end());

if (t == rev) cout << "YES";
```

---

### ✅ Pattern 3: Count only symbols

```cpp
int count = 0;
for (char c : s)
    if (ispunct(c)) count++;
```

---

# 🔥 Pro CP Tips

* Prefer `char` over `string[i]` when looping
* Use `&c` if modifying in-place
* `isalnum()` is safer than manual ASCII
* Avoid regex in contests (slow)
* Always use `getline()` when symbols + spaces are involved

---

If you want, I can give you:
✅ 20 real CP problems based on string + symbols
✅ or a **complete string template for contests** 🚀

