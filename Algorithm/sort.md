# Sort

1. [Kth largest element in an array](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/sort.md#1-kth-largest-element-in-an-array)
2. [Top k freuqent element](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/sort.md#2-top-k-frequent-element)

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

## 2. Top k frequent element

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order. (Problem 347)

Example:

Input: nums = [1, 1, 1, 2, 2, 3]

Output: [1, 2]

**In this problem, we normally use a method called bucket sort. For example, we set up a number of buckets, each of which stores the numbers with same frequency. That means the nth buckets stores the numbers which appear n times. When we put all the numbers in the bucket, we go through the bucket from the back to the front, the first k numbers we get are the k numbers that occur the most frequently.**

```java
class Solution {
  public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> numsFrequency = new HashMap<>();
    for (int num : nums) {
      numsFrequency.put(num, numsFrequency.getOrDefault(num, 0) + 1);
    }
    List<Integer> buckets = new ArrayList[nums.length + 1];
    for (int key : numsFrequency.keySet()) {
      int frequency = numsFrequency.get[key];
      if (buckets[frequency] == null) {
        buckets[frequency] = new ArrayList<>();
      }
      buckets[frequency].add(key);
    }
    List<Integer> topK = new ArrayList();
    for (int i = buckets.length - 1; i >= 0 && topk.size() < k; i--) {
      if (buckets[i] == null) {
        continue;
      } else if (buckets[i] <= k - topK.size()) {
        topK.addAll(buckets[i]);
      } else {
        topK.addAll(buckets[i].subList(0, k - topK.size()))
      }
    }
    int[] result = new int[k];
    for (int j = 0; j < k, j++) {
      result[j] = topK.get(j);
    }
    return result;
  }
}
```

## 3. Sort character by frequency

Given a string, sort it in decreasing order based on the frequency of characters, and return the sorted string.(problem 451)

Example 1:

Input: s = "tree"

Output: "eert"

Explanation: 'e' appears twice while 'r' and 't' both appear once. So 'e' must appear before both 'r' and 't'. Therefore, "eetr" is also a valid answer.

Example 2:

Input: s = "cccaaa"

Output: "aaaccc"

Explanation: Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer. Note that "cacaca" is incorrect, as the same characters must be together.

**This problem is just the same as problem 347. We also use buckets sort to solve this problem.**

```java
class Solution {
  public String frequencySort(String s) {
    Map<Character, Integer> frequencyForLetter = new HashMap<>();
    for (char c : s.toCharArray()) {
      frequencyForLetter.put(c, frequencyForLetter(c, 0) + 1);
    }
    List<Character> buckets= new ArrayList[s.length() + 1];
    for (char key : frequencyForLetter.keySet()) {
      int frequency = frequencyForLetter.get(key);
      if (buckets[frequency] == null) {
        buckets[frequency] = new ArrayList<>();
      }
      buckets[freuqency].add(key);
    }
    StringBuilder result = new StringBuilder();
    for (int i = buckets.length - 1; i >= 0; i--) {
      if (buckets[i] == null) {
        continue;
      }
      for (char letter : buckets[i]) {
        for (int j = 0; j < i; j++) {
          result.append(letter);
        }
      }
    }
    return result.toString();
  }
}
```

