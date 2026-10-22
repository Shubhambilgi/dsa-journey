# C++ Core Syntax for DSA

A short cheat sheet of the C++ you need before starting Data Structures and Algorithms. Keep it open while watching videos.

## 1. Compile and Run

```bash
g++ -std=c++17 main.cpp -o main
./main
```

## 2. Program Template (use this for every DSA problem)

```cpp
#include <bits/stdc++.h>   // includes almost everything (works on g++, not on MSVC/clang by default)
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);  // faster input/output
    cin.tie(nullptr);

    // your code here

    return 0;
}
```

If `bits/stdc++.h` doesn't work on your machine, include headers individually: `<iostream>`, `<vector>`, `<algorithm>`, `<string>`, `<map>`, `<set>`, etc.

## 3. Data Types

| Type | Use | Range / Note |
|------|-----|--------------|
| `int` | whole numbers | about -2.1 x 10^9 to 2.1 x 10^9 |
| `long long` | big whole numbers | about 9 x 10^18 (use when `int` may overflow) |
| `double` | decimals | |
| `char` | one character | `'a'` |
| `bool` | true / false | |
| `string` | text | |

```cpp
int a = 10;
long long big = 1e12;      // 1e12 is a double, converted to long long
double d = 3.14;
char c = 'x';
bool ok = true;
string s = "hello";
```

Overflow is a common DSA bug. If sums or products can pass about 2 billion, use `long long`.

## 4. Input and Output

```cpp
int n;
cin >> n;                    // read
cout << n << "\n";           // print (use "\n", not endl, for speed)

string line;
getline(cin, line);          // read a full line
```

## 5. Operators

```cpp
+  -  *  /  %          // arithmetic (5 / 2 is 2, integer division)
++  --  +=  -=  *=     // increment, compound assignment
==  !=  <  >  <=  >=   // comparison
&&  ||  !              // logical AND, OR, NOT
&  |  ^  <<  >>        // bitwise (used in bit manipulation problems)
```

## 6. Conditions

```cpp
if (x > 0) {
} else if (x == 0) {
} else {
}

int m = (a > b) ? a : b;   // ternary
```

## 7. Loops

```cpp
for (int i = 0; i < n; i++) { }          // classic
for (int x : arr) { }                    // range-based
for (auto &x : arr) { }                  // modify elements
while (cond) { }
do { } while (cond);

break;       // exit loop
continue;    // skip to next iteration
```

## 8. Functions

```cpp
int add(int a, int b) {
    return a + b;
}

void change(int &x) { x = 100; }               // reference: modifies original
void show(const vector<int> &v) { }            // const reference: no copy, read-only
void fill(vector<int> &v) { v.push_back(1); }  // modifies the original vector
```

Pass vectors and strings by reference. Passing by value copies them and makes your code slow.

**Recursion** (very important for DSA):

```cpp
int fact(int n) {
    if (n <= 1) return 1;     // base case: always needed
    return n * fact(n - 1);   // recursive call
}
```

## 9. Arrays

```cpp
int arr[5] = {1, 2, 3, 4, 5};
int arr2[100] = {0};               // all zeros
int grid[3][4];                    // 2D array
```

Indexing starts at 0. Accessing outside `0..n-1` is undefined behavior.

## 10. Vector (most used container)

```cpp
vector<int> v;                      // empty
vector<int> v2(5, 0);               // size 5, all 0
vector<int> v3 = {1, 2, 3};

v.push_back(10);      // add at end
v.pop_back();         // remove last
v.size();             // number of elements
v.empty();            // is empty?
v.front();  v.back(); // first / last
v.clear();
v.insert(v.begin() + 1, 99);   // insert at index 1
v.erase(v.begin() + 1);        // erase at index 1

vector<vector<int>> mat(n, vector<int>(m, 0));   // 2D vector, n x m
```

## 11. String

```cpp
string s = "hello";
s.size();                 // 5
s[0];                     // 'h'
s += " world";            // append
s.substr(1, 3);           // "ell" (start, length)
s.find("lo");             // index or string::npos
reverse(s.begin(), s.end());
s == "abc";               // comparison with ==
to_string(123);           // int to string
stoi("123");              // string to int
```

## 12. Pointers and References (basics)

```cpp
int x = 10;
int *p = &x;      // p stores the address of x
cout << *p;       // 10 (value at that address)
*p = 20;          // x becomes 20

int &r = x;       // r is another name for x
r = 30;           // x becomes 30

int *q = nullptr; // points to nothing
```

You need this for linked lists, trees and graphs:

```cpp
struct Node {
    int data;
    Node *next;
    Node(int d) : data(d), next(nullptr) {}
};

Node *head = new Node(1);
head->next = new Node(2);    // use -> to access members through a pointer
```

## 13. Struct and Class

```cpp
struct Point {
    int x, y;
};
Point p = {3, 4};
cout << p.x;

class Stack {
private:
    vector<int> data;
public:
    void push(int x) { data.push_back(x); }
    void pop()       { data.pop_back(); }
    int top()        { return data.back(); }
    bool empty()     { return data.empty(); }
};
```

## 14. STL Containers You Will Use in DSA

```cpp
stack<int> st;               // push, pop, top, empty
queue<int> q;                // push, pop, front, empty
deque<int> dq;               // push_front, push_back, pop_front, pop_back
priority_queue<int> maxHeap; // largest on top
priority_queue<int, vector<int>, greater<int>> minHeap; // smallest on top

set<int> s;                  // unique, sorted; insert, erase, find, count
map<string, int> m;          // sorted key -> value
unordered_map<int, int> um;  // hash map, fast lookup
unordered_set<int> us;       // hash set

m["a"] = 1;
if (m.find("a") != m.end()) { }   // key exists?
for (auto &[key, val] : m) { }    // loop through a map
```

| Container | Typical operation cost |
|-----------|-----------------------|
| `vector` access by index | O(1) |
| `vector` push_back | O(1) average |
| `set`, `map` | O(log n) |
| `unordered_set`, `unordered_map` | O(1) average |
| `priority_queue` push/pop | O(log n) |

## 15. STL Algorithms

```cpp
sort(v.begin(), v.end());                       // ascending
sort(v.begin(), v.end(), greater<int>());       // descending
reverse(v.begin(), v.end());
*max_element(v.begin(), v.end());
*min_element(v.begin(), v.end());
accumulate(v.begin(), v.end(), 0);              // sum (long long: use 0LL)
find(v.begin(), v.end(), 5);                    // iterator to 5, or v.end()
binary_search(v.begin(), v.end(), 5);           // needs sorted data
lower_bound(v.begin(), v.end(), 5);             // first element >= 5
swap(a, b);

// Sort with a custom rule (lambda)
sort(v.begin(), v.end(), [](int a, int b) {
    return a > b;
});

// Sort pairs
vector<pair<int,int>> p = {{2, 1}, {1, 5}};
sort(p.begin(), p.end());       // sorts by first, then second
p[0].first;  p[0].second;
```

## 16. Useful Constants

```cpp
INT_MAX;    // largest int
INT_MIN;    // smallest int
LLONG_MAX;  // largest long long
```

## 17. Little Theory You Should Know

**Time complexity (Big O):** how the running time grows as input size `n` grows.

| Notation | Name | Example |
|----------|------|---------|
| O(1) | constant | array access |
| O(log n) | logarithmic | binary search |
| O(n) | linear | single loop |
| O(n log n) | linearithmic | sorting |
| O(n^2) | quadratic | nested loops |
| O(2^n) | exponential | naive recursion on subsets |

**Rule of thumb:** a computer does about 10^8 simple operations per second. If `n` is 10^5, an O(n^2) solution is too slow, so aim for O(n log n) or better.

**Space complexity:** how much extra memory your solution uses.

**Stack vs heap memory:** normal local variables live on the stack and are freed automatically. Memory created with `new` lives on the heap and must be freed with `delete`.

**Pass by reference:** use `&` for vectors, strings and anything large, otherwise C++ copies them.

## 18. Common Mistakes

1. Off-by-one errors: valid indexes are `0` to `n-1`.
2. Using `int` when the answer needs `long long`.
3. Integer division: `5 / 2` is `2`.
4. Forgetting the base case in recursion (causes a crash).
5. Accessing an empty `vector`, `stack` or `queue` (`back()`, `top()`, `front()`) without checking `empty()`.
6. Using `=` instead of `==`.
7. Passing big vectors by value.

## 19. Next Step

Once these are comfortable, move on to the DSA topics in order: arrays, strings, recursion, sorting, binary search, linked lists, stacks and queues, trees, graphs, dynamic programming.
