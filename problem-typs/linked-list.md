# Linked List in C++ — Full Concept + CP Tricks

---

## 1. Types of Linked Lists

| Type | Description |
|------|-------------|
| Singly Linked List | Each node points to next |
| Doubly Linked List | Each node points to next and prev |
| Circular Linked List | Last node points back to head |
| Circular Doubly Linked List | Combines both above |

---

## 2. Node Structure

```cpp
// Singly
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Doubly
struct DNode {
    int data;
    DNode* prev;
    DNode* next;
    DNode(int val) : data(val), prev(nullptr), next(nullptr) {}
};
```

---

## 3. Basic Singly Linked List Operations

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Insert at head — O(1)
Node* insertHead(Node* head, int val) {
    Node* newNode = new Node(val);
    newNode->next = head;
    return newNode;
}

// Insert at tail — O(n)
Node* insertTail(Node* head, int val) {
    Node* newNode = new Node(val);
    if (!head) return newNode;
    Node* cur = head;
    while (cur->next) cur = cur->next;
    cur->next = newNode;
    return head;
}

// Insert at position k (0-indexed) — O(k)
Node* insertAt(Node* head, int val, int k) {
    Node* newNode = new Node(val);
    if (k == 0) { newNode->next = head; return newNode; }
    Node* cur = head;
    for (int i = 0; i < k - 1 && cur; i++) cur = cur->next;
    if (!cur) return head; // k out of bounds
    newNode->next = cur->next;
    cur->next = newNode;
    return head;
}

// Delete by value — O(n)
Node* deleteVal(Node* head, int val) {
    if (!head) return nullptr;
    if (head->data == val) {
        Node* tmp = head->next;
        delete head;
        return tmp;
    }
    Node* cur = head;
    while (cur->next && cur->next->data != val)
        cur = cur->next;
    if (cur->next) {
        Node* tmp = cur->next;
        cur->next = tmp->next;
        delete tmp;
    }
    return head;
}

// Search — O(n)
bool search(Node* head, int val) {
    while (head) {
        if (head->data == val) return true;
        head = head->next;
    }
    return false;
}

// Print list
void print(Node* head) {
    while (head) {
        cout << head->data;
        if (head->next) cout << " -> ";
        head = head->next;
    }
    cout << "\n";
}

// Length — O(n)
int length(Node* head) {
    int len = 0;
    while (head) { len++; head = head->next; }
    return len;
}
```

---

## 4. Reversal (Most Important CP Trick)

### Iterative — O(n), O(1) space

```cpp
Node* reverse(Node* head) {
    Node* prev = nullptr;
    Node* cur = head;
    while (cur) {
        Node* nxt = cur->next;
        cur->next = prev;
        prev = cur;
        cur = nxt;
    }
    return prev; // new head
}
```

### Recursive — O(n), O(n) stack space

```cpp
Node* reverseRec(Node* head) {
    if (!head || !head->next) return head;
    Node* newHead = reverseRec(head->next);
    head->next->next = head;
    head->next = nullptr;
    return newHead;
}
```

### Reverse in groups of K

```cpp
Node* reverseK(Node* head, int k) {
    if (!head || k == 1) return head;
    Node* cur = head;
    Node* prev = nullptr;
    int count = 0;
    // reverse k nodes
    while (cur && count < k) {
        Node* nxt = cur->next;
        cur->next = prev;
        prev = cur;
        cur = nxt;
        count++;
    }
    // head is now the tail of this reversed group
    head->next = reverseK(cur, k);
    return prev;
}
```

---

## 5. Floyd's Cycle Detection (Tortoise & Hare)

```cpp
// Detect cycle — O(n), O(1)
bool hasCycle(Node* head) {
    Node* slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}

// Find start of cycle — O(n), O(1)
Node* cycleStart(Node* head) {
    Node* slow = head, *fast = head;
    bool found = false;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) { found = true; break; }
    }
    if (!found) return nullptr;
    slow = head; // reset slow to head
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow; // start of cycle
}

// Length of cycle
int cycleLength(Node* head) {
    Node* slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) {
            int len = 1;
            fast = fast->next;
            while (slow != fast) { fast = fast->next; len++; }
            return len;
        }
    }
    return 0;
}
```

---

## 6. Two-Pointer Tricks

### Find Middle of Linked List

```cpp
// Returns middle node (left-middle for even length)
Node* findMiddle(Node* head) {
    Node* slow = head, *fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```

### Find Nth Node from End

```cpp
// O(n), single pass
Node* nthFromEnd(Node* head, int n) {
    Node* fast = head, *slow = head;
    for (int i = 0; i < n; i++) {
        if (!fast) return nullptr; // n > length
        fast = fast->next;
    }
    while (fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```

### Remove Nth Node from End

```cpp
Node* removeNthFromEnd(Node* head, int n) {
    Node dummy(0);
    dummy.next = head;
    Node* fast = &dummy, *slow = &dummy;
    for (int i = 0; i <= n; i++) fast = fast->next;
    while (fast) {
        slow = slow->next;
        fast = fast->next;
    }
    Node* toDelete = slow->next;
    slow->next = slow->next->next;
    delete toDelete;
    return dummy.next;
}
```

---

## 7. Merge Operations

### Merge Two Sorted Lists — O(n+m)

```cpp
Node* mergeSorted(Node* l1, Node* l2) {
    Node dummy(0);
    Node* cur = &dummy;
    while (l1 && l2) {
        if (l1->data <= l2->data) { cur->next = l1; l1 = l1->next; }
        else                      { cur->next = l2; l2 = l2->next; }
        cur = cur->next;
    }
    cur->next = l1 ? l1 : l2;
    return dummy.next;
}
```

### Merge Sort on Linked List — O(n log n)

```cpp
Node* mergeSort(Node* head) {
    if (!head || !head->next) return head;
    Node* mid = findMiddle(head);
    Node* second = mid->next;
    mid->next = nullptr; // split
    Node* left  = mergeSort(head);
    Node* right = merseSort(second);
    return mergeSorted(left, right);
}
```

---

## 8. Palindrome Check

```cpp
bool isPalindrome(Node* head) {
    if (!head || !head->next) return true;
    // Find middle
    Node* slow = head, *fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // Reverse second half
    Node* secondHalf = reverse(slow->next);
    Node* copy = secondHalf;
    bool result = true;
    // Compare
    Node* first = head;
    while (copy) {
        if (first->data != copy->data) { result = false; break; }
        first = first->next;
        copy  = copy->next;
    }
    // Restore list (optional but good practice)
    slow->next = reverse(secondHalf);
    return result;
}
```

---

## 9. Intersection of Two Lists

```cpp
// O(n+m), O(1) space
Node* getIntersection(Node* headA, Node* headB) {
    if (!headA || !headB) return nullptr;
    Node* a = headA, *b = headB;
    while (a != b) {
        a = a ? a->next : headB;
        b = b ? b->next : headA;
    }
    return a;
}
```

---

## 10. Flatten a Multilevel List

```cpp
// Each node may have a child pointer to another list
struct MNode {
    int val;
    MNode* next;
    MNode* child;
};

MNode* flatten(MNode* head) {
    if (!head) return head;
    MNode* cur = head;
    while (cur) {
        if (cur->child) {
            MNode* child = cur->child;
            MNode* next  = cur->next;
            cur->next    = child;
            child->prev  = cur;
            cur->child   = nullptr;
            // find tail of child list
            MNode* tail = child;
            while (tail->next) tail = tail->next;
            tail->next = next;
        }
        cur = cur->next;
    }
    return head;
}
```

---

## 11. Rotate List by K

```cpp
Node* rotateRight(Node* head, int k) {
    if (!head || !head->next || k == 0) return head;
    int n = 1;
    Node* tail = head;
    while (tail->next) { tail = tail->next; n++; }
    tail->next = head; // make circular
    k = k % n;
    int stepsToNewHead = n - k;
    Node* newTail = head;
    for (int i = 1; i < stepsToNewHead; i++) newTail = newTail->next;
    Node* newHead = newTail->next;
    newTail->next = nullptr;
    return newHead;
}
```

---

## 12. Clone List with Random Pointer

```cpp
struct RNode {
    int val;
    RNode* next;
    RNode* random;
};

RNode* copyRandomList(RNode* head) {
    if (!head) return nullptr;
    unordered_map<RNode*, RNode*> mp;
    RNode* cur = head;
    // First pass: create all nodes
    while (cur) {
        mp[cur] = new RNode{cur->val, nullptr, nullptr};
        cur = cur->next;
    }
    // Second pass: assign pointers
    cur = head;
    while (cur) {
        mp[cur]->next   = mp[cur->next];
        mp[cur]->random = mp[cur->random];
        cur = cur->next;
    }
    return mp[head];
}

// O(1) space trick — interleave original and clone
RNode* copyRandomListO1(RNode* head) {
    if (!head) return nullptr;
    RNode* cur = head;
    // Step 1: interleave clones
    while (cur) {
        RNode* clone = new RNode{cur->val, cur->next, nullptr};
        cur->next = clone;
        cur = clone->next;
    }
    // Step 2: set random pointers
    cur = head;
    while (cur) {
        if (cur->random)
            cur->next->random = cur->random->next;
        cur = cur->next->next;
    }
    // Step 3: separate lists
    cur = head;
    RNode* cloneHead = head->next;
    while (cur) {
        RNode* clone = cur->next;
        cur->next = clone->next;
        if (clone->next) clone->next = clone->next->next;
        cur = cur->next;
    }
    return cloneHead;
}
```

---

## 13. Add Two Numbers as Lists

```cpp
// Numbers stored in reverse (LSD first)
Node* addTwoNumbers(Node* l1, Node* l2) {
    Node dummy(0);
    Node* cur = &dummy;
    int carry = 0;
    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) { sum += l1->data; l1 = l1->next; }
        if (l2) { sum += l2->data; l2 = l2->next; }
        carry = sum / 10;
        cur->next = new Node(sum % 10);
        cur = cur->next;
    }
    return dummy.next;
}
```

---

## 14. Sort List — Partition (Dutch National Flag on LL)

```cpp
// Partition around pivot value
Node* partition(Node* head, int x) {
    Node lessHead(0), greaterHead(0);
    Node* less = &lessHead, *greater = &greaterHead;
    while (head) {
        if (head->data < x) { less->next = head; less = less->next; }
        else                 { greater->next = head; greater = greater->next; }
        head = head->next;
    }
    greater->next = nullptr;
    less->next = greaterHead.next;
    return lessHead.next;
}
```

---

## 15. Odd-Even Grouping

```cpp
// Group all odd-indexed nodes, then even-indexed — O(n), O(1)
Node* oddEvenList(Node* head) {
    if (!head) return head;
    Node* odd = head, *even = head->next, *evenHead = even;
    while (even && even->next) {
        odd->next  = even->next;
        odd        = odd->next;
        even->next = odd->next;
        even       = even->next;
    }
    odd->next = evenHead;
    return head;
}
```

---

## 16. XOR Linked List (Memory-Efficient Doubly LL)

```cpp
// Uses XOR of addresses instead of two pointers
#include <cstdint>

struct XorNode {
    int data;
    XorNode* both; // XOR of prev and next
    XorNode(int val) : data(val), both(nullptr) {}
};

XorNode* XOR(XorNode* a, XorNode* b) {
    return reinterpret_cast<XorNode*>(
        reinterpret_cast<uintptr_t>(a) ^ reinterpret_cast<uintptr_t>(b)
    );
}

// Traverse XOR list
void printXor(XorNode* head) {
    XorNode* prev = nullptr, *cur = head;
    while (cur) {
        cout << cur->data << " ";
        XorNode* next = XOR(prev, cur->both);
        prev = cur;
        cur  = next;
    }
    cout << "\n";
}
```

---

## 17. STL Alternatives for CP

```cpp
#include <list>
#include <forward_list>

// std::list  = doubly linked list
list<int> dll = {1, 2, 3};
dll.push_front(0);
dll.push_back(4);
dll.insert(next(dll.begin(), 2), 99); // insert at position 2
dll.reverse();
dll.sort();
dll.unique();   // remove consecutive duplicates
dll.merge(another_list);

// std::forward_list = singly linked list
forward_list<int> sll = {1, 2, 3};
sll.push_front(0);
sll.insert_after(sll.begin(), 99);
sll.reverse();
sll.sort();

// Splice (O(1) move of elements — killer CP trick)
list<int> a = {1, 2, 3}, b = {4, 5, 6};
auto it = next(a.begin()); // points to 2
a.splice(it, b);           // inserts all of b before 'it': 1, 4, 5, 6, 2, 3
```

---

## 18. Common CP Problem Patterns

| Problem Pattern | Key Technique |
|-----------------|---------------|
| Detect / find cycle | Floyd's algorithm |
| Middle of list | Slow-fast pointers |
| Merge k sorted lists | Min-heap + dummy node |
| LRU Cache | `list` + `unordered_map` |
| Reorder list | Find mid → reverse 2nd half → merge |
| Palindrome | Find mid → reverse → compare |
| Intersection | Two-pointer equalization |
| K-group reversal | Recursion + iterative reverse |
| Sort linked list | Merge sort (never bubble sort) |

---

## 19. LRU Cache (Classic CP/Interview Problem)

```cpp
class LRUCache {
    int cap;
    list<pair<int,int>> dll; // {key, value}
    unordered_map<int, list<pair<int,int>>::iterator> mp;
public:
    LRUCache(int capacity) : cap(capacity) {}

    int get(int key) {
        if (mp.find(key) == mp.end()) return -1;
        dll.splice(dll.begin(), dll, mp[key]); // move to front O(1)
        return mp[key]->second;
    }

    void put(int key, int value) {
        if (mp.count(key)) {
            dll.splice(dll.begin(), dll, mp[key]);
            mp[key]->second = value;
        } else {
            if ((int)dll.size() == cap) {
                mp.erase(dll.back().first);
                dll.pop_back();
            }
            dll.push_front({key, value});
            mp[key] = dll.begin();
        }
    }
};
```

---

## 20. Reorder List (Leetcode 143 Style)

```cpp
// 1->2->3->4->5  becomes  1->5->2->4->3
void reorderList(Node* head) {
    if (!head || !head->next) return;
    // Step 1: find middle
    Node* slow = head, *fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // Step 2: reverse second half
    Node* second = reverse(slow->next);
    slow->next = nullptr;
    // Step 3: merge alternately
    Node* first = head;
    while (second) {
        Node* tmp1 = first->next;
        Node* tmp2 = second->next;
        first->next  = second;
        second->next = tmp1;
        first  = tmp1;
        second = tmp2;
    }
}
```

---

## 21. Quick Reference — Time Complexities

| Operation | Singly LL | Doubly LL | Array |
|-----------|-----------|-----------|-------|
| Access by index | O(n) | O(n) | O(1) |
| Search | O(n) | O(n) | O(n) |
| Insert at head | O(1) | O(1) | O(n) |
| Insert at tail | O(n) / O(1)* | O(1)* | O(1) amortized |
| Insert at middle | O(n) | O(n) | O(n) |
| Delete at head | O(1) | O(1) | O(n) |
| Delete at tail | O(n) | O(1)* | O(1) |
| Delete at middle | O(n) | O(n) | O(n) |

*With tail pointer maintained

---

## 22. Common Pitfalls in CP

```cpp
// 1. Always check for null before accessing ->next
if (head && head->next) { ... }

// 2. Use dummy node to simplify edge cases
Node dummy(0);
dummy.next = head;
// work with dummy.next instead of head
return dummy.next;

// 3. Don't forget to update tail pointer when maintaining one
// 4. Free memory if asked (competitive: usually skip)
// 5. Odd/even length edge cases in palindrome / middle problems
// 6. When reversing, save next BEFORE breaking the link
Node* nxt = cur->next; // save
cur->next = prev;       // break/redirect
```

---

## 23. Template for Fast LL Setup in CP

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

Node* build(vector<int>& v) {
    if (v.empty()) return nullptr;
    Node* head = new Node(v[0]);
    Node* cur = head;
    for (int i = 1; i < (int)v.size(); i++) {
        cur->next = new Node(v[i]);
        cur = cur->next;
    }
    return head;
}

vector<int> toVector(Node* head) {
    vector<int> res;
    while (head) { res.push_back(head->data); head = head->next; }
    return res;
}

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    Node* head = build(v);
    // ... solve problem ...
    for (int x : toVector(head)) cout << x << " ";
}
```
