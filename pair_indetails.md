# C++ STL – Pair (`std::pair`) Detailed Notes

A **pair** is a **simple container** in C++ STL that stores **two heterogeneous values together**. It is defined in the `<utility>` header and is widely used in combination with STL containers, especially vectors, maps, and algorithms.

---

## 1. Introduction

* **Header:** `<utility>`
* **Namespace:** `std`
* **Purpose:** To store **two related values** as a single object.
* Commonly used in:

  * Storing key-value pairs
  * Returning two values from a function
  * Sorting and comparison operations
  * Graph algorithms (edges with weights)

---

## 2. Declaration and Initialization

### 2.1 Basic Declaration

```cpp
#include <utility>
using namespace std;

pair<int, string> p1;  // pair of int and string
```

### 2.2 Initialization

```cpp
pair<int, string> p1 = {1, "Hello"};
pair<int, int> p2(10, 20);
pair<string, string> p3;
p3.first = "Key";
p3.second = "Value";
```

### 2.3 Using `make_pair()`

```cpp
auto p4 = make_pair(5, "World"); // type deduced automatically
```

**Notes:**

* Pairs can store **different data types**.
* Can be initialized at declaration or assigned later.

---

## 3. Accessing Members

Pairs have **two public data members**:

| Member   | Description                    |
| -------- | ------------------------------ |
| `first`  | The first element of the pair  |
| `second` | The second element of the pair |

```cpp
int x = p1.first;
string y = p1.second;
```

---

## 4. Modifying Pair Elements

```cpp
p1.first = 10;
p1.second = "Updated";
```

* You can assign **new values** directly.
* Pairs can also be **swapped**:

```cpp
pair<int,int> a = {1,2}, b = {3,4};
a.swap(b); // a = {3,4}, b = {1,2}
```

---

## 5. Pair Comparisons

Pairs support **lexicographical comparisons** based on `first` and then `second`.

| Operator | Meaning                     |
| -------- | --------------------------- |
| `==`     | Equal                       |
| `!=`     | Not equal                   |
| `<`      | Less than (lexicographical) |
| `>`      | Greater than                |
| `<=`     | Less or equal               |
| `>=`     | Greater or equal            |

```cpp
pair<int,int> a = {1,2}, b = {1,3};
if(a < b) cout << "a is smaller"; // True because 2 < 3
```

---

## 6. Nested Pairs

Pairs can contain other pairs as members:

```cpp
pair<int, pair<int,int>> np = {1, {2,3}};
cout << np.first << " " << np.second.first << " " << np.second.second;
// Output: 1 2 3
```

* Useful in **graph algorithms** for edges: `(weight, (u,v))`.
* Can be nested to **store multiple related values**.

---

## 7. Using Pairs with Vectors

Pairs are commonly used with vectors to store multiple values together:

```cpp
vector<pair<int,int>> vp;
vp.push_back({1,2});
vp.emplace_back(3,4);

for(auto pr : vp)
    cout << pr.first << " " << pr.second << "\n";
```

---

### 7.1 Sorting Vector of Pairs

1. **Default sorting** – by `first`, then `second`:

```cpp
vector<pair<int,int>> vp = {{3,4}, {1,2}, {5,0}};
sort(vp.begin(), vp.end()); // sorted: {1,2}, {3,4}, {5,0}
```

2. **Custom sorting by second element**:

```cpp
sort(vp.begin(), vp.end(), [](pair<int,int> a, pair<int,int> b){
    return a.second < b.second;
});
// sorts by second value of pair
```

* Can use **functors** or lambda functions.

---

### 7.2 Accessing Sorted Pairs

```cpp
for(auto pr : vp)
    cout << pr.first << " " << pr.second << "\n";
```

* Useful in competitive programming for **intervals, weights, or coordinates**.

---

## 8. Pairs with Maps

Pairs are used as **map elements**:

```cpp
map<int,string> mp;
mp[1] = "One";
mp[2] = "Two";

// Accessing map as pair
for(auto pr : mp)
    cout << pr.first << " " << pr.second << "\n";
```

* `map` internally stores elements as pairs `(key, value)`.

---

## 9. Advanced Uses

1. **Returning multiple values from a function**:

```cpp
pair<int,int> minMax(vector<int>& v) {
    return { *min_element(v.begin(), v.end()), *max_element(v.begin(), v.end()) };
}
```

2. **Graph edges**:

```cpp
vector<pair<int,pair<int,int>>> edges;
edges.push_back({10, {1,2}}); // weight 10, edge 1-2
sort(edges.begin(), edges.end()); // sort by weight
```

3. **Custom Comparisons** for sorting or priority queues:

```cpp
auto cmp = [](pair<int,int> a, pair<int,int> b) {
    return a.second > b.second; // sort descending by second
};
sort(vp.begin(), vp.end(), cmp);
```

---

## 10. Performance Notes

* Access: O(1)
* Swap: O(1)
* Comparisons: O(1) per comparison (lexicographical)
* Works efficiently with **vectors, maps, sets, and algorithms**.

---

## 11. Summary Table

| Feature        | Pair (`std::pair`)                                                 |
| -------------- | ------------------------------------------------------------------ |
| Header         | `<utility>`                                                        |
| Members        | `.first`, `.second`                                                |
| Initialization | `{}`, `()`, `make_pair()`                                          |
| Access         | `pair.first`, `pair.second`                                        |
| Modification   | Assign values directly or swap                                     |
| Comparison     | Lexicographical: `<`, `>`, `==`                                    |
| Nested Pairs   | Supported                                                          |
| Integration    | Vectors, Maps, Sets, Algorithms                                    |
| Common Uses    | Key-value storage, graph edges, returning multiple values, sorting |


