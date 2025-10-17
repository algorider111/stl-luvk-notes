**Topic:** Find Minimum in Rotated Sorted Array
**Difficulty:** Easy
**Algorithm Type:** Binary Search
**Related Concept:** Rotated Sorted Array

---

### 1. Problem Statement

You are given a sorted array that has been rotated an unknown number of times.
Your task is to find and return the minimum element in the array.

**Example 1:**
Input: `[4, 5, 6, 7, 0, 1, 2]`
Output: `0`
Explanation: The array was originally `[0, 1, 2, 4, 5, 6, 7]`, rotated at pivot index 4.

**Example 2:**
Input: `[3, 4, 5, 1, 2]`
Output: `1`

---

### 2. Brute Force Approach – O(N)

**Idea:**
Traverse the entire array and track the smallest element.

**Algorithm Steps:**

1. Initialize `ans = nums[0]`.
2. Loop through every element in the array.
3. Update `ans = min(ans, nums[i])`.
4. Return `ans`.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

**C++ Code:**

```cpp
int findMin(vector<int>& nums) {
    int ans = nums[0];
    for (int x : nums)
        ans = min(ans, x);
    return ans;
}
```

**Note:**
This approach is simple but not efficient for large inputs.

---

### 3. Optimized Approach – O(log N) using Binary Search

**Idea:**
Since the array is partially sorted, we can use binary search to eliminate one half in each step.
In a rotated sorted array, one part is always sorted, and the minimum element lies in the unsorted half.

---

#### Key Observations

1. One half (either left or right) is always sorted.
2. The minimum element will lie in the unsorted half.
3. The smallest element of a sorted half is always at its starting index.

---

### 4. Binary Search Algorithm

**Steps:**

1. Initialize:

   ```
   low = 0, high = n - 1, ans = INT_MAX
   ```
2. While `low <= high`:

   * Compute `mid = (low + high) / 2`
   * If the subarray `[low..high]` is already sorted:

     * `ans = min(ans, nums[low])`
     * Break out of the loop (optimization)
   * If the left half `[low..mid]` is sorted:

     * Update `ans = min(ans, nums[low])`
     * Move to the right half → `low = mid + 1`
   * Otherwise (right half is sorted):

     * Update `ans = min(ans, nums[mid])`
     * Move to the left half → `high = mid - 1`
3. Return `ans`.

---

### 5. C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

int findMin(vector<int>& nums) {
    int low = 0, high = nums.size() - 1;
    int ans = INT_MAX;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        // If the search space is already sorted
        if (nums[low] <= nums[high]) {
            ans = min(ans, nums[low]);
            break;
        }

        // Left half is sorted
        if (nums[low] <= nums[mid]) {
            ans = min(ans, nums[low]);
            low = mid + 1;
        }
        // Right half is sorted
        else {
            ans = min(ans, nums[mid]);
            high = mid - 1;
        }
    }

    return ans;
}

int main() {
    vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    cout << findMin(nums);
}
```

---

### 6. Dry Run Example

For `nums = [4, 5, 6, 7, 0, 1, 2]`:

| low | mid | high | nums[mid] | Action                        | ans |
| --- | --- | ---- | --------- | ----------------------------- | --- |
| 0   | 3   | 6    | 7         | Left half sorted → move right | 4   |
| 4   | 5   | 6    | 1         | Right half sorted → move left | 0   |
| End |     |      |           | Minimum found                 | 0   |

---

### 7. Optimization

If at any point the subarray `[low..high]` is completely sorted (`nums[low] <= nums[high]`),
then the smallest element in that subarray is `nums[low]`.
In such cases, update `ans` and break the loop to stop early.

---

### 8. Complexity Analysis

| Parameter        | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(log N)      |
| Space Complexity | O(1)          |
| Type             | Binary Search |

---

### 9. Important Notes

* In a rotated sorted array:

  * One half is always sorted.
  * The pivot (rotation point) is where the minimum lies.
* The algorithm eliminates the sorted half since its smallest element is already known.
* When the array becomes fully sorted (no rotation left), the loop terminates early.

---

### 10. Summary

| Approach                | Description            | Time     | Space |
| ----------------------- | ---------------------- | -------- | ----- |
| Linear Search           | Check all elements     | O(N)     | O(1)  |
| Binary Search           | Use rotation property  | O(log N) | O(1)  |
| Optimized Binary Search | Early stop when sorted | O(log N) | O(1)  |

---

**Conclusion:**
The binary search approach efficiently finds the minimum element in a rotated sorted array by exploiting the sorted-half property and eliminating one half in each step, achieving O(log N) complexity.
