# C++ STL – Vector (`std::vector`) Detailed Notes

A **vector** is a **sequence container** that encapsulates dynamic arrays. It allows **automatic resizing**, provides **random access**, and integrates well with STL algorithms.

---

## 1. Introduction

* Vectors are part of `<vector>` header.
* Dynamic size: Unlike C-style arrays, vectors can **grow or shrink** during runtime.
* Contiguous storage: Elements are stored in a continuous block of memory.
* Random access: Access elements by index in **O(1)** time.

```cpp
#include <vector>
using namespace std;

vector<int> v; // empty vector of integers
```

---

## 2. Declaration and Initialization

**1. Default initialization**

```cpp
vector<int> v1; // empty vector
```

**2. Initialize with size**

```cpp
vector<int> v2(5);      // 5 elements initialized to 0
vector<int> v3(5, 10);  // 5 elements, all 10
```

**3. Initialize using initializer list**

```cpp
vector<int> v4 = {1, 2, 3, 4, 5};
```

**4. Copy constructor**

```cpp
vector<int> v5(v4); // copy all elements from v4
```

**5. Range constructor**

```cpp
vector<int> v6(v4.begin(), v4.begin() + 3); // first 3 elements
```

---

## 3. Accessing Elements

| Method    | Description                       |
| --------- | --------------------------------- |
| `[]`      | Direct access, no bounds check    |
| `at()`    | Access with bounds checking       |
| `front()` | Access first element              |
| `back()`  | Access last element               |
| `data()`  | Returns pointer to internal array |

```cpp
int x = v[0];
int y = v.at(0);
int first = v.front();
int last = v.back();
int* ptr = v.data();
```

---

## 4. Modifying Vectors

### 4.1 Adding Elements

```cpp
v.push_back(10);      // append at the end
v.emplace_back(20);   // construct element at the end (faster)
```

### 4.2 Removing Elements

```cpp
v.pop_back();                  // remove last element
v.erase(v.begin() + 1);        // remove element at index 1
v.erase(v.begin(), v.begin()+2); // remove first two elements
v.clear();                     // remove all elements
```

### 4.3 Inserting Elements

```cpp
v.insert(v.begin() + 1, 50);       // insert 50 at index 1
v.insert(v.end(), {100,200,300});  // insert multiple at end
```

### 4.4 Resizing and Capacity

```cpp
v.resize(10);   // resize vector to 10 elements
v.reserve(20);  // allocate memory for 20 elements without changing size
v.shrink_to_fit(); // reduce capacity to fit size
```

---

## 5. Iterators

Vectors support **random access iterators**.

```cpp
for(vector<int>::iterator it = v.begin(); it != v.end(); ++it)
    cout << *it << " ";

for(auto it = v.rbegin(); it != v.rend(); ++it)
    cout << *it << " "; // reverse iteration
```

* `begin()`, `end()` → forward iteration
* `rbegin()`, `rend()` → reverse iteration
* `cbegin()`, `cend()` → constant iterators (read-only)

---

## 6. Common Algorithms

Vectors work seamlessly with STL algorithms.

```cpp
#include <algorithm>
sort(v.begin(), v.end());                    // sort ascending
reverse(v.begin(), v.end());                 // reverse
v.erase(unique(v.begin(), v.end()), v.end());// remove duplicates
auto it = find(v.begin(), v.end(), 5);      // find element
```

* `lower_bound`, `upper_bound` work only on **sorted vectors**.

---

## 7. Performance Characteristics

| Operation           | Complexity     |
| ------------------- | -------------- |
| Access by index     | O(1)           |
| Insertion at end    | Amortized O(1) |
| Insertion in middle | O(n)           |
| Deletion at end     | O(1)           |
| Deletion in middle  | O(n)           |
| Search              | O(n)           |
| Sort                | O(n log n)     |

**Tips:**

* Use `reserve()` if the number of elements is known to avoid frequent reallocations.
* Prefer `emplace_back()` over `push_back()` for objects to reduce copies.
* For large vectors, `shrink_to_fit()` can release unused memory.

---

## 8. Vectors of Vectors

Useful for 2D grids, matrices, and adjacency lists.

```cpp
vector<vector<int>> matrix(3, vector<int>(4, 0)); // 3x4 matrix
matrix[0][1] = 5;
```

* Access: `matrix[row][col]`
* Can be resized dynamically.

---

## 9. Advanced Features

### 9.1 Swapping Vectors

```cpp
vector<int> v1 = {1,2,3};
vector<int> v2 = {4,5,6};
v1.swap(v2); // v1 = {4,5,6}, v2 = {1,2,3}
```

### 9.2 Copy and Move Semantics

```cpp
vector<int> v3 = v1;         // copy constructor
vector<int> v4 = move(v1);   // move constructor (v1 becomes empty)
```

### 9.3 Integration with STL

```cpp
vector<int> v = {4,2,5,1,3};
sort(v.begin(), v.end());
auto it = lower_bound(v.begin(), v.end(), 3); // first >=3
auto pos = distance(v.begin(), it);          // index of element
```

* Vectors are **contiguous**, so pointer arithmetic is allowed with `data()`.

---

## 10. Common Use Cases

* Dynamic arrays with frequent resizing
* Matrices and grids
* Storing lists of values for sorting, searching, or binary search
* Adjacency lists in graph algorithms
* Using with STL algorithms (`sort`, `lower_bound`, `upper_bound`)

---

## Summary Table

| Feature                    | Vector (`std::vector`)                                      |
| -------------------------- | ----------------------------------------------------------- |
| Header                     | `<vector>`                                                  |
| Type                       | Sequence container                                          |
| Storage                    | Contiguous memory                                           |
| Size                       | Dynamic                                                     |
| Access                     | Random access (`[]`, `at()`)                                |
| Iterators                  | Random access iterators                                     |
| Modifiers                  | `push_back`, `pop_back`, `insert`, `erase`, `swap`, `clear` |
| Common Algorithms          | `sort`, `reverse`, `unique`, `find`                         |
| Advanced Features          | `emplace_back`, `reserve`, `shrink_to_fit`, move semantics  |
| Complexity (access)        | O(1)                                                        |
| Complexity (insert end)    | Amortized O(1)                                              |
| Complexity (insert middle) | O(n)                                                        |

