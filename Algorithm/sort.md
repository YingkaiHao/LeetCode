# Sort

1. [Kth largest element in an array](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/sort.md#1-kth-largest-element-in-an-array)

## 1. Kth largest element in an array

Given a integer array nums and an integer k, return the nth largest element in the array. Note that it is the largest element in the sorted order, not the nth distinct element.(problem 215)

Example:

Input: nums = [3, 2, 1, 5, 6, 4], k = 2

Output: 5

### (1) Time complexity: O(NlogN). Space complexity: O(1)

```java
public Solution {
  public int findKthLargest(int[] nums, int k) {
    Arrays.sort(nums);
    int result = nums[nums.length - k];
    return result;
  }
}
```

### (2) Time complexity: O(NlogK). Space complexity:O(k)

When the number of elements in the heap is greater than k, remove the top element of the heap, which is the largest element in the current heap, and all remaining elements are the smallest k elements of the currently added element.

```java
class Solution {
  public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> p = new PriorityQueue<>();
    for (int val: nums) {
      p.add(val);
      if (p.size() > k) {
        p.poll();
      }
    }
    return p.peek();
  }
}
```

### (3) Time complexity: O(n). Space complexity: O(1)

```java
class Solution {
  public int findKthLargest(int[] nums, int k) {
    int max;
    int temp;
    for (int i = 0; i < nums.length - 1; i++) {
      max = i;
      for (int j = i + 1; j < nums.length; j++) {
        if (nums[max] < nums[j]) {
          max = j;
        }
      }
      if (max != i) {
        temp = nums[i];
        nums[i] = nums[max];
        nums[max] = temp;
      }
    }
    return nums[k - 1];
  }
}
```

