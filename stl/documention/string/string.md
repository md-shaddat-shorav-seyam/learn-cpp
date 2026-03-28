Here’s a full **A to Z guide to C++ `string` and its methods** in a clear exam-friendly way.

---

# C++ `string` complete guide

## 1. What is `string` in C++?

A `string` in C++ is a sequence of characters, like:

```cpp
string name = "Shorav";
```

It is part of the **Standard Library**, so you need:

```cpp
#include <iostream>
#include <string>
using namespace std;
```

---

# 2. Why use `string` instead of char array?

Old C style:

```cpp
char name[] = "Shorav";
```

Modern C++ style:

```cpp
string name = "Shorav";
```

### Advantages of `string`

* easier to use
* dynamic size
* many built-in methods
* easy concatenation
* safer than character arrays

---

# 3. Declaring strings

```cpp
string s1;
string s2 = "Hello";
string s3("World");
string s4(5, 'A');   // AAAAA
```

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1;
    string s2 = "Hello";
    string s3("World");
    string s4(5, 'A');

    cout << s1 << endl;
    cout << s2 << endl;
    cout << s3 << endl;
    cout << s4 << endl;

    return 0;
}
```

---

# 4. Input and output with string

## `cin`

Reads only one word until space.

```cpp
string name;
cin >> name;
```

If input is:

```cpp
Md Shaddat
```

Only `Md` will be stored.

## `getline()`

Reads full line including spaces.

```cpp
string fullName;
getline(cin, fullName);
```

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    getline(cin, name);
    cout << "Your name is: " << name << endl;
    return 0;
}
```

### Important issue with `cin` and `getline`

If you use `cin` before `getline`, leftover newline may cause problem.

```cpp
int age;
cin >> age;
cin.ignore();
getline(cin, name);
```

---

# 5. Accessing characters in string

You can access characters like array indexing.

```cpp
string s = "Hello";

cout << s[0] << endl; // H
cout << s[1] << endl; // e
```

Also:

```cpp
cout << s.at(2) << endl; // l
```

Difference:

* `s[i]` → no bounds checking
* `s.at(i)` → checks range, safer

---

# 6. Size and length

## `size()`

Returns number of characters.

```cpp
string s = "Hello";
cout << s.size();   // 5
```

## `length()`

Same as `size()`.

```cpp
cout << s.length(); // 5
```

---

# 7. Empty check

## `empty()`

```cpp
string s = "";
if (s.empty()) {
    cout << "String is empty";
}
```

---

# 8. Adding strings

## Concatenation using `+`

```cpp
string a = "Hello";
string b = " World";
string c = a + b;
cout << c;   // Hello World
```

## Concatenation using `append()`

```cpp
string a = "Hello";
a.append(" World");
cout << a;   // Hello World
```

---

# 9. Modifying string

## `push_back()`

Adds one character at end.

```cpp
string s = "Hell";
s.push_back('o');
cout << s;   // Hello
```

## `pop_back()`

Removes last character.

```cpp
string s = "Hello";
s.pop_back();
cout << s;   // Hell
```

---

# 10. Clear string

## `clear()`

```cpp
string s = "Hello";
s.clear();
cout << s.size();   // 0
```

---

# 11. Compare strings

## Using `==`

```cpp
string a = "apple";
string b = "apple";

if (a == b) {
    cout << "Equal";
}
```

## Using `compare()`

```cpp
string a = "apple";
string b = "banana";

cout << a.compare(b) << endl;
```

### `compare()` result

* `0` → equal
* negative → first string smaller
* positive → first string larger

Example:

```cpp
if (a.compare(b) == 0) {
    cout << "Equal";
}
```

---

# 12. Find characters or substring

## `find()`

```cpp
string s = "I love C++";
cout << s.find("love");   // 2
```

It returns starting index.

If not found:

```cpp
if (s.find("Java") == string::npos) {
    cout << "Not found";
}
```

### Example

```cpp
string s = "programming";
cout << s.find('g') << endl;   // first g position
```

---

# 13. Reverse find

## `rfind()`

Finds from right side.

```cpp
string s = "banana";
cout << s.rfind('a');   // 5
```

---

# 14. Substring

## `substr(pos, len)`

```cpp
string s = "programming";
cout << s.substr(0, 4);   // prog
cout << s.substr(4, 3);   // ram
```

If length omitted:

```cpp
cout << s.substr(3);   // gramming
```

---

# 15. Insert into string

## `insert()`

```cpp
string s = "Hllo";
s.insert(1, "e");
cout << s;   // Hello
```

Another example:

```cpp
string s = "I C++";
s.insert(2, "love ");
cout << s;   // I love C++
```

---

# 16. Erase part of string

## `erase(pos, len)`

```cpp
string s = "I love C++";
s.erase(2, 5);
cout << s;   // I C++
```

---

# 17. Replace part of string

## `replace(pos, len, newString)`

```cpp
string s = "I like Java";
s.replace(7, 4, "C++");
cout << s;   // I like C++
```

---

# 18. Swap strings

## `swap()`

```cpp
string a = "Hello";
string b = "World";

a.swap(b);

cout << a << endl; // World
cout << b << endl; // Hello
```

---

# 19. Front and back character

## `front()`

```cpp
string s = "Hello";
cout << s.front();   // H
```

## `back()`

```cpp
cout << s.back();    // o
```

---

# 20. C-style string conversion

## `c_str()`

Used when you need C-style character pointer.

```cpp
string s = "Hello";
const char* p = s.c_str();
cout << p;
```

---

# 21. Copy string content

## `copy()`

```cpp
string s = "Hello";
char arr[10];
s.copy(arr, 5, 0);
arr[5] = '\0';
cout << arr;   // Hello
```

---

# 22. Resize string

## `resize()`

```cpp
string s = "Hello";
s.resize(3);
cout << s;   // Hel
```

Increase size:

```cpp
string s = "Hi";
s.resize(5, 'x');
cout << s;   // Hixxx
```

---

# 23. Capacity-related methods

These are more advanced but useful.

## `capacity()`

Returns current allocated storage.

```cpp
string s = "Hello";
cout << s.capacity();
```

## `reserve()`

Reserves memory in advance.

```cpp
string s;
s.reserve(100);
cout << s.capacity();
```

## `shrink_to_fit()`

Tries to reduce unused memory.

```cpp
string s = "Hello world";
s.shrink_to_fit();
```

## `max_size()`

Returns maximum possible size.

```cpp
string s;
cout << s.max_size();
```

---

# 24. Iterating over string

## Using loop with index

```cpp
string s = "Hello";

for (int i = 0; i < s.size(); i++) {
    cout << s[i] << " ";
}
```

## Range-based loop

```cpp
for (char ch : s) {
    cout << ch << " ";
}
```

## Using iterator

```cpp
for (string::iterator it = s.begin(); it != s.end(); it++) {
    cout << *it << " ";
}
```

---

# 25. Begin and end

## `begin()`, `end()`

```cpp
string s = "Hello";
cout << *s.begin() << endl;   // H
```

## `rbegin()`, `rend()`

Reverse iteration.

```cpp
for (auto it = s.rbegin(); it != s.rend(); it++) {
    cout << *it;
}
```

Output:

```cpp
olleH
```

---

# 26. String to number conversion

## `stoi()` → string to int

```cpp
string s = "123";
int x = stoi(s);
cout << x + 10;   // 133
```

## `stol()` → string to long

```cpp
string s = "123456";
long x = stol(s);
```

## `stoll()` → string to long long

```cpp
string s = "9999999999";
long long x = stoll(s);
```

## `stof()` → string to float

```cpp
string s = "12.5";
float x = stof(s);
```

## `stod()` → string to double

```cpp
string s = "45.67";
double x = stod(s);
```

---

# 27. Number to string conversion

## `to_string()`

```cpp
int x = 123;
string s = to_string(x);
cout << s + "456";   // 123456
```

---

# 28. Lexicographical comparison

C++ compares strings dictionary-wise.

```cpp
cout << ("apple" < "banana");   // 1 (true)
cout << ("cat" > "car");        // 1
```

Rules:

* compares character by character
* based on ASCII/lexicographic order

---

# 29. Common useful character operations with string

These come from `<cctype>`.

```cpp
#include <cctype>
```

## `toupper()`

```cpp
char ch = 'a';
cout << char(toupper(ch));   // A
```

## `tolower()`

```cpp
char ch = 'A';
cout << char(tolower(ch));   // a
```

## `isalpha()`

```cpp
cout << isalpha('A');   // true
```

## `isdigit()`

```cpp
cout << isdigit('5');   // true
```

## `isalnum()`

```cpp
cout << isalnum('a');   // true
cout << isalnum('9');   // true
```

## `isspace()`

```cpp
cout << isspace(' ');   // true
```

---

# 30. Convert whole string to uppercase

```cpp
string s = "hello";

for (int i = 0; i < s.size(); i++) {
    s[i] = toupper(s[i]);
}

cout << s;   // HELLO
```

## Lowercase

```cpp
for (int i = 0; i < s.size(); i++) {
    s[i] = tolower(s[i]);
}
```

---

# 31. Reverse a string

## Method 1: `reverse()`

```cpp
#include <algorithm>

string s = "hello";
reverse(s.begin(), s.end());
cout << s;   // olleh
```

## Method 2: manual

```cpp
string s = "hello";
for (int i = s.size() - 1; i >= 0; i--) {
    cout << s[i];
}
```

---

# 32. Sort a string

```cpp
#include <algorithm>

string s = "dcab";
sort(s.begin(), s.end());
cout << s;   // abcd
```

Descending:

```cpp
sort(s.rbegin(), s.rend());
```

---

# 33. Count characters

```cpp
string s = "banana";
int cnt = count(s.begin(), s.end(), 'a');
cout << cnt;   // 3
```

---

# 34. Remove spaces from string

```cpp
string s = "I love C plus plus";
string result = "";

for (char ch : s) {
    if (ch != ' ') {
        result += ch;
    }
}

cout << result;   // IloveCplusplus
```

---

# 35. Palindrome check

A palindrome reads same forward and backward.

```cpp
string s = "madam";
string t = s;
reverse(t.begin(), t.end());

if (s == t) {
    cout << "Palindrome";
} else {
    cout << "Not palindrome";
}
```

---

# 36. Count vowels and consonants

```cpp
string s = "Hello World";
int vowels = 0, consonants = 0;

for (char ch : s) {
    ch = tolower(ch);
    if (isalpha(ch)) {
        if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
            vowels++;
        else
            consonants++;
    }
}

cout << "Vowels: " << vowels << endl;
cout << "Consonants: " << consonants << endl;
```

---

# 37. Remove a character from string

```cpp
string s = "banana";
s.erase(remove(s.begin(), s.end(), 'a'), s.end());
cout << s;   // bnn
```

---

# 38. Split words from sentence

Using `stringstream`

```cpp
#include <sstream>

string s = "I love C++ programming";
stringstream ss(s);
string word;

while (ss >> word) {
    cout << word << endl;
}
```

---

# 39. Join strings

```cpp
string a = "Hello";
string b = "World";
string result = a + " " + b;
cout << result;
```

---

# 40. Escape characters in strings

```cpp
string s = "Hello\nWorld";
cout << s;
```

Common escape characters:

* `\n` → new line
* `\t` → tab
* `\"` → double quote
* `\\` → backslash

Example:

```cpp
cout << "He said, \"Hello\"";
```

---

# 41. Raw string literal

Useful when many backslashes appear.

```cpp
string path = R"(C:\Users\Name\Documents)";
cout << path;
```

---

# 42. Important string methods list

Here is a clean method summary:

## Element access

* `s[i]`
* `at(i)`
* `front()`
* `back()`

## Capacity

* `size()`
* `length()`
* `empty()`
* `capacity()`
* `reserve()`
* `resize()`
* `max_size()`
* `shrink_to_fit()`

## Modifiers

* `append()`
* `push_back()`
* `pop_back()`
* `insert()`
* `erase()`
* `replace()`
* `clear()`
* `swap()`

## Operations

* `find()`
* `rfind()`
* `substr()`
* `compare()`
* `copy()`
* `c_str()`

## Iterators

* `begin()`
* `end()`
* `rbegin()`
* `rend()`

---

# 43. Full demo program

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s = "Hello";

    cout << "Original: " << s << endl;
    cout << "Size: " << s.size() << endl;
    cout << "First char: " << s.front() << endl;
    cout << "Last char: " << s.back() << endl;

    s.push_back('!');
    cout << "After push_back: " << s << endl;

    s.pop_back();
    cout << "After pop_back: " << s << endl;

    s.append(" World");
    cout << "After append: " << s << endl;

    cout << "Substring: " << s.substr(0, 5) << endl;
    cout << "Find 'World': " << s.find("World") << endl;

    s.replace(6, 5, "C++");
    cout << "After replace: " << s << endl;

    reverse(s.begin(), s.end());
    cout << "Reversed: " << s << endl;

    sort(s.begin(), s.end());
    cout << "Sorted: " << s << endl;

    return 0;
}
```

---

# 44. Time complexity of common string operations

Approximate:

* `size()` → **O(1)**
* `empty()` → **O(1)**
* `push_back()` → **O(1)** amortized
* `pop_back()` → **O(1)**
* `substr()` → **O(k)**
* `find()` → **O(n)**
* `insert()` → **O(n)**
* `erase()` → **O(n)**
* `replace()` → **O(n)**
* `reverse()` → **O(n)**
* `sort()` → **O(n log n)**

---

# 45. Common mistakes

## 1. Using `cin` for full sentence

Wrong:

```cpp
string s;
cin >> s;
```

Input:

```cpp
I love cpp
```

Only `I` is stored.

Use:

```cpp
getline(cin, s);
```

---

## 2. Out of range access

Wrong:

```cpp
string s = "abc";
cout << s[5];
```

May cause undefined behavior.

Safer:

```cpp
cout << s.at(2);
```

---

## 3. Comparing string with integer

Wrong:

```cpp
string s = "123";
if (s == 123) {}
```

Need conversion:

```cpp
if (stoi(s) == 123) {}
```

---

# 46. Interview and exam important topics

You should know these very well:

* declaration of string
* input using `cin` and `getline`
* indexing
* `size()` and `length()`
* `find()`
* `substr()`
* `insert()`
* `erase()`
* `replace()`
* `append()`
* `compare()`
* string reverse
* string palindrome
* uppercase/lowercase conversion
* `stoi()` and `to_string()`

---

# 47. Practice examples

## Example 1: count letters

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s;
    getline(cin, s);

    cout << "Length = " << s.length() << endl;
    return 0;
}
```

## Example 2: reverse sentence

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s;
    getline(cin, s);

    reverse(s.begin(), s.end());
    cout << s << endl;

    return 0;
}
```

## Example 3: find word

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "I love programming";

    if (s.find("love") != string::npos)
        cout << "Found";
    else
        cout << "Not found";

    return 0;
}
```

---

# 48. Very short revision sheet

```cpp
string s = "Hello";

s.size();          // 5
s.length();        // 5
s.empty();         // false
s[0];              // H
s.at(1);           // e
s.front();         // H
s.back();          // o
s.push_back('!');
s.pop_back();
s.append(" World");
s.insert(5, " ABC");
s.erase(0, 2);
s.replace(0, 3, "Hi");
s.find("lo");
s.rfind('l');
s.substr(1, 3);
s.clear();
s.swap(other);
```

---

# 49. Difference between string and character array

## String

```cpp
string s = "hello";
```

## Character array

```cpp
char s[] = "hello";
```

### String advantages

* dynamic
* easier methods
* safer
* easier to compare and join

---

# 50. Final exam-style summary

C++ `string` is a class from the standard library used to handle text easily.
It supports:

* storing words and sentences
* accessing characters
* comparing strings
* finding substrings
* modifying content
* converting between string and numbers

Most used functions:

* `size()`
* `length()`
* `empty()`
* `append()`
* `find()`
* `substr()`
* `insert()`
* `erase()`
* `replace()`
* `clear()`
* `compare()`
* `stoi()`
* `to_string()`

---

I can also make this into a **clean note format**, **mind map**, or **50 practice problems with solutions** for C++ strings.
