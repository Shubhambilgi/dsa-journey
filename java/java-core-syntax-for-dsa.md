# Java Core Syntax for DSA

A short cheat sheet of the Java you need before starting Data Structures and Algorithms.

## 1. Setup, Compile and Run

Install the JDK (version 17 or newer), then check:

```bash
java -version
javac -version
```

```bash
javac Main.java     # compile
java Main           # run
```

The file name must match the public class name: `public class Main` goes in `Main.java`.

## 2. Program Template

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // your code here

        sc.close();
    }
}
```

`import java.util.*;` brings in `ArrayList`, `HashMap`, `Scanner`, `Arrays`, `Collections` and the rest.

Helper methods go inside the class and are usually `static`:

```java
static int add(int a, int b) {
    return a + b;
}
```

## 3. Data Types

| Type | Use | Note |
|------|-----|------|
| `int` | whole numbers | about -2.1 x 10^9 to 2.1 x 10^9 |
| `long` | big whole numbers | about 9 x 10^18 (use when `int` may overflow) |
| `double` | decimals | |
| `char` | one character | `'a'` |
| `boolean` | true / false | |
| `String` | text | immutable object |

```java
int a = 10;
long big = 1_000_000_000_000L;   // L suffix for long literals
double d = 3.14;
char c = 'x';
boolean ok = true;
String s = "hello";
final int MOD = 1_000_000_007;   // constant
```

Overflow is a common DSA bug. If sums or products can pass about 2 billion, use `long`.

Useful constants:

```java
Integer.MAX_VALUE;   Integer.MIN_VALUE;
Long.MAX_VALUE;      Long.MIN_VALUE;
```

## 4. Input and Output

```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
String word = sc.next();           // one word
sc.nextLine();                     // consume leftover newline after nextInt()
String line = sc.nextLine();       // full line

System.out.println(n);             // print with newline
System.out.print(n + " ");         // print without newline
System.out.printf("%.2f%n", 3.14159);   // formatted output
```

`Scanner` is fine for learning. For big inputs in contests, use `BufferedReader` (faster).

## 5. Operators

```java
+  -  *  /  %          // arithmetic (5 / 2 is 2, integer division)
++  --  +=  -=  *=     // increment, compound assignment
==  !=  <  >  <=  >=   // comparison
&&  ||  !              // logical AND, OR, NOT
&  |  ^  <<  >>  >>>   // bitwise (>>> is unsigned right shift)
```

## 6. Conditions

```java
if (x > 0) {
} else if (x == 0) {
} else {
}

int m = (a > b) ? a : b;   // ternary

switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    default: System.out.println("Other");
}
```

## 7. Loops

```java
for (int i = 0; i < n; i++) { }       // classic
for (int x : arr) { }                 // enhanced for (read each element)
while (cond) { }
do { } while (cond);

break;       // exit loop
continue;    // skip to next iteration
```

## 8. Methods (Functions)

```java
static int add(int a, int b) {
    return a + b;
}

static void printArray(int[] arr) {
    for (int x : arr) System.out.print(x + " ");
}
```

**Pass by value rule in Java:**
- Primitives (`int`, `long`, `double`, `char`, `boolean`) are copied, so changes inside the method do not affect the original.
- Objects and arrays pass a copy of the reference, so changing their contents does affect the original.

```java
static void change(int[] arr) { arr[0] = 99; }   // original array changes
static void change(int x)     { x = 99; }        // original does NOT change
```

That means a `swap(int a, int b)` method does not work. Swap inside the same method or use an array and indexes.

**Recursion** (very important for DSA):

```java
static int fact(int n) {
    if (n <= 1) return 1;       // base case: always needed
    return n * fact(n - 1);     // recursive call
}
```

## 9. Arrays

```java
int[] arr = {1, 2, 3, 4, 5};
int[] a = new int[10];            // all zeros by default
int n = arr.length;               // .length, no parentheses

int[][] grid = new int[3][4];     // 2D array, 3 rows x 4 columns
int[][] g2 = {{1, 2}, {3, 4}};
grid.length;                      // rows
grid[0].length;                   // columns

Arrays.sort(arr);                 // sort ascending
Arrays.fill(a, -1);               // fill with a value
Arrays.toString(arr);             // "[1, 2, 3, 4, 5]"
Arrays.deepToString(grid);        // for 2D arrays
int[] copy = Arrays.copyOf(arr, arr.length);
int[] part = Arrays.copyOfRange(arr, 1, 4);   // indexes 1 to 3
Arrays.equals(arr, copy);         // compares contents
```

Indexing starts at 0. Going outside `0..n-1` throws `ArrayIndexOutOfBoundsException` (Java catches it, unlike C++).

Note: `System.out.println(arr)` prints a memory-like address. Use `Arrays.toString(arr)`.

## 10. ArrayList (dynamic array)

```java
ArrayList<Integer> list = new ArrayList<>();

list.add(10);              // add at end
list.add(1, 99);           // insert at index 1
list.get(0);               // read
list.set(0, 5);            // update
list.remove(list.size() - 1);   // remove by index
list.remove(Integer.valueOf(99)); // remove by value
list.size();
list.isEmpty();
list.contains(5);
list.clear();

for (int x : list) { }

ArrayList<ArrayList<Integer>> g = new ArrayList<>();   // list of lists (graphs)
```

Generics need wrapper types: use `Integer`, `Long`, `Character`, `Boolean`, not `int`, `long`, `char`.

## 11. String and StringBuilder

```java
String s = "hello";
s.length();                    // 5 (parentheses for String)
s.charAt(0);                   // 'h'
s.substring(1, 4);             // "ell" (start, end exclusive)
s.indexOf("lo");               // index or -1
s.contains("ell");
s.toUpperCase();  s.toLowerCase();
s.equals("abc");               // compare content (NEVER use == for strings)
s.compareTo("abd");            // dictionary order
s.toCharArray();               // char[]
s.split(" ");                  // String[]
String.valueOf(123);           // int to String
Integer.parseInt("123");       // String to int
```

Strings are immutable, so `s = s + "x"` creates a new string every time. For repeated changes inside loops use `StringBuilder`:

```java
StringBuilder sb = new StringBuilder();
sb.append("abc");
sb.append('d');
sb.reverse();
sb.insert(0, "x");
sb.deleteCharAt(sb.length() - 1);
sb.length();
sb.toString();
```

**Char tricks (very common in DSA):**

```java
char c = 'b';
int idx = c - 'a';                 // 1 (position in the alphabet)
char next = (char) (c + 1);        // 'c'
Character.isDigit(c);
Character.isLetter(c);
int[] freq = new int[26];
freq[c - 'a']++;                   // frequency counting
```

## 12. Math and Utilities

```java
Math.max(a, b);   Math.min(a, b);
Math.abs(x);      Math.pow(2, 10);     // returns double
Math.sqrt(25);    Math.ceil(2.1);      Math.floor(2.9);
Math.floorMod(-7, 3);                  // proper positive modulo
```

## 13. Classes and Objects

```java
class Student {
    String name;
    int age;

    Student(String name, int age) {    // constructor
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " " + age);
    }
}

Student s = new Student("Shubham", 21);
s.display();
```

**Node classes (needed for linked lists and trees).** Java has no pointers, so object references do the same job. Use `.` instead of `->` and `null` instead of `nullptr`.

```java
class Node {
    int data;
    Node next;
    Node(int data) { this.data = data; this.next = null; }
}

Node head = new Node(1);
head.next = new Node(2);

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}
```

You do not need to free memory. Java's garbage collector handles it.

## 14. Collections You Will Use in DSA

```java
// HashMap: key -> value, O(1) average
HashMap<Integer, Integer> map = new HashMap<>();
map.put(5, 1);
map.get(5);
map.getOrDefault(7, 0);
map.containsKey(5);
map.remove(5);
map.put(5, map.getOrDefault(5, 0) + 1);   // frequency count
for (Map.Entry<Integer, Integer> e : map.entrySet()) {
    int k = e.getKey(), v = e.getValue();
}

// HashSet: unique values
HashSet<Integer> set = new HashSet<>();
set.add(3);  set.contains(3);  set.remove(3);

// TreeMap / TreeSet: sorted, O(log n)
TreeMap<Integer, Integer> tm = new TreeMap<>();
TreeSet<Integer> ts = new TreeSet<>();
ts.first();  ts.last();  ts.floor(5);  ts.ceiling(5);

// Stack (use Deque, not the old Stack class)
Deque<Integer> st = new ArrayDeque<>();
st.push(1);  st.peek();  st.pop();  st.isEmpty();

// Queue
Queue<Integer> q = new LinkedList<>();
q.add(1);  q.peek();  q.poll();  q.isEmpty();

// Deque (both ends)
Deque<Integer> dq = new ArrayDeque<>();
dq.addFirst(1);  dq.addLast(2);  dq.pollFirst();  dq.pollLast();

// Heap
PriorityQueue<Integer> minHeap = new PriorityQueue<>();                          // min on top
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // max on top
minHeap.add(5);  minHeap.peek();  minHeap.poll();
```

| Structure | Typical operation cost |
|-----------|-----------------------|
| `ArrayList` get by index | O(1) |
| `ArrayList` add at end | O(1) average |
| `HashMap`, `HashSet` | O(1) average |
| `TreeMap`, `TreeSet` | O(log n) |
| `PriorityQueue` add/poll | O(log n) |

Warning: `stack.peek()` and `queue.poll()` on an empty structure give `null` (or throw an exception for `pop()`), so check `isEmpty()` first.

## 15. Sorting and Comparators

```java
Arrays.sort(arr);                                   // int[] ascending
Collections.sort(list);                             // ArrayList ascending
Collections.sort(list, Collections.reverseOrder()); // descending

Integer[] boxed = {5, 2, 9};
Arrays.sort(boxed, Collections.reverseOrder());     // descending (needs Integer[], not int[])

// Sort a 2D array by a column (lambda)
int[][] pairs = {{2, 5}, {1, 9}, {3, 1}};
Arrays.sort(pairs, (a, b) -> Integer.compare(a[0], b[0]));   // by first column

// Sort strings by length
Arrays.sort(words, (a, b) -> a.length() - b.length());
```

Prefer `Integer.compare(a, b)` over `a - b`, because subtraction can overflow.

## 16. Binary Search

```java
Arrays.sort(arr);
int idx = Arrays.binarySearch(arr, 7);    // index if found, negative if not
```

Writing your own is more common in DSA:

```java
static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;   // avoids overflow
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

## 17. Wrapper Class Pitfall

```java
Integer a = 1000, b = 1000;
a == b;           // false (compares references)
a.equals(b);      // true  (compares values)
```

Always use `.equals()` to compare `Integer`, `Long` and `String` objects.

## 18. Little Theory You Should Know

**Time complexity (Big O):** how the running time grows as input size `n` grows.

| Notation | Name | Example |
|----------|------|---------|
| O(1) | constant | array access |
| O(log n) | logarithmic | binary search |
| O(n) | linear | single loop |
| O(n log n) | linearithmic | sorting |
| O(n^2) | quadratic | nested loops |
| O(2^n) | exponential | naive recursion on subsets |

**Rule of thumb:** a computer does about 10^8 simple operations per second. If `n` is 10^5, an O(n^2) solution is too slow.

**Space complexity:** how much extra memory your solution uses.

**Stack vs heap memory:** local variables and method calls live on the stack. Objects created with `new` live on the heap, and the garbage collector frees them.

**Deep recursion** can cause `StackOverflowError`. Very deep recursion (around 10^4 to 10^5 levels) may need an iterative solution.

## 19. Common Mistakes

1. Comparing strings or `Integer` objects with `==` instead of `.equals()`.
2. Using `int` when the answer needs `long`.
3. Integer division: `5 / 2` is `2`.
4. Off-by-one errors: valid indexes are `0` to `n-1`.
5. Forgetting the base case in recursion.
6. Calling `pop()`, `peek()` or `poll()` on an empty stack, queue or heap.
7. Using `arr.length()` for arrays or `s.length` for strings (it is `arr.length` and `s.length()`).
8. Printing an array directly instead of using `Arrays.toString()`.
9. Using `Arrays.sort(arr, Collections.reverseOrder())` on `int[]` (needs `Integer[]`).

## 20. Complete Example: Two Sum

Save as `TwoSum.java`:

```java
import java.util.*;

public class TwoSum {

    // O(n) time, O(n) space
    static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> seen = new HashMap<>();   // value -> index
        for (int i = 0; i < nums.length; i++) {
            int need = target - nums[i];
            if (seen.containsKey(need)) {
                return new int[]{seen.get(need), i};
            }
            seen.put(nums[i], i);
        }
        return new int[]{};
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int[] ans = twoSum(nums, 9);
        System.out.println("Indexes: " + ans[0] + " " + ans[1]);
    }
}
```

```bash
javac TwoSum.java
java TwoSum
```

Expected output:

```
Indexes: 0 1
```

## 21. Next Step

Once these are comfortable, move on to the DSA topics in order: arrays, strings, recursion, sorting, binary search, linked lists, stacks and queues, trees, graphs, dynamic programming.
