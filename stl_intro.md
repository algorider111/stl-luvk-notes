# C++ STL – Overview Notes

The **Standard Template Library (STL)** in C++ is a powerful library providing **generic, reusable, and efficient components** for data structures and algorithms.
It consists of **four main parts**:

---

## 1. Containers

Containers store collections of data. They can be classified as:

* **Sequence Containers** – store elements in linear order. Examples: `vector`, `deque`, `list`, `array`, `forward_list`.
* **Associative Containers** – store elements in a sorted manner. Examples: `set`, `multiset`, `map`, `multimap`.
* **Unordered Containers** – use hash tables for fast access. Examples: `unordered_set`, `unordered_map`.
* **Container Adapters** – provide restricted interfaces to other containers. Examples: `stack`, `queue`, `priority_queue`.

**Note:** Choose a container based on the type of operations required, such as random access, insertion/deletion efficiency, or sorted storage.

---

## 2. Iterators

Iterators are objects that point to elements in a container, allowing traversal and access.

* Types of iterators:

  * Input Iterator
  * Output Iterator
  * Forward Iterator
  * Bidirectional Iterator
  * Random Access Iterator

**Example:**

```cpp
vector<int> v = {1, 2, 3};
for(auto it = v.begin(); it != v.end(); ++it) 
    cout << *it << " ";
```

---

## 3. Algorithms

STL provides a wide range of **predefined algorithms** for operations such as searching, sorting, counting, and numeric calculations.

* Examples:

```cpp
sort(v.begin(), v.end());
reverse(v.begin(), v.end());
count(v.begin(), v.end(), x);
find(v.begin(), v.end(), x);
accumulate(v.begin(), v.end(), 0);
```

**Note:** Using STL algorithms reduces code length and improves efficiency.

---

## 4. Functors (Function Objects)

A **functor** is a class or struct that overloads the `()` operator, allowing it to be used like a function.

* Primarily used with algorithms for **custom operations or comparisons**.
* Example:

```cpp
struct Greater {
    bool operator()(int a, int b) { return a > b; }
};

sort(v.begin(), v.end(), Greater()); // Sort in descending order
```

* STL also provides built-in functors like `greater<int>` and `less<int>`.

---

## Summary

* **Container:** Stores data
* **Iterator:** Accesses and traverses data
* **Algorithm:** Operates on data
* **Functor:** Customizes algorithm behavior

Do you want me to do that?
