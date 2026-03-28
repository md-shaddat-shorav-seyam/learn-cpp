```cpp
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;

int main() {
    string str = "Hello, World!";
    
    // Method 1: Using std::reverse
    string reversed1 = str;
    reverse(reversed1.begin(), reversed1.end());
    cout << "Method 1: " << reversed1 << endl;

    // Method 2: Using rbegin/rend iterator
    string reversed2(str.rbegin(), str.rend());
    cout << "Method 2: " << reversed2 << endl;

    // Method 3: Manual loop
    string reversed3 = "";
    for (int i = str.length() - 1; i >= 0; i--)
        reversed3 += str[i];
    cout << "Method 3: " << reversed3 << endl;

    return 0;
}
```

**Output:**
```
Method 1: !dlroW ,olleH
Method 2: !dlroW ,olleH
Method 3: !dlroW ,olleH
```

Three common approaches:

| Method | How it works |
|---|---|
| `std::reverse` | In-place reversal using iterators from `<algorithm>` |
| `rbegin/rend` | Constructs a new string using reverse iterators |
| Manual loop | Iterates from last char to first, building a new string |

**Recommendation:** Use `std::reverse` (Method 1) for in-place or the `rbegin/rend` constructor (Method 2) for a new string — both are clean, idiomatic C++.