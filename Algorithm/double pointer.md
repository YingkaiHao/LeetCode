# Double Pointer

1. [Two sum II-Input array is sorted](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#1-two-sum-ii-input-array-is-sorted)
2. [Sum of square numbers](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#2-sum-of-square-numbers)
3. [Reverse vowels of a string](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#3-reverse-vowels-of-a-string)
4. [Valid palindrome II](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#4-valid-palindrome-ii)
5. [Merge sorted list](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#5-merge-sorted-list)
6. [Linked list cycle](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#6-linked-list-cycle)

## 1. Two sum II-Input array is sorted

Given an array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.

Return the indices of the two numbers (1-indexed) as an integer array answer of size 2, where 1 <= answer[0] < answer[1] <= numbers.length.

The tests are generates such that there is exactly one solution. You may not use the same element twice.(problem 167)

Example 1:

Iuput: numbers = [2, 7, 11, 15], target = 9

Output: [1, 2]

Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.

Example 2:

Input: numbers = [2, 3, 4], target = 6

Output: [1, 3]

**We use double pointer to solve this problem. One pointer point to the head of the array and traverse from head to tail. Another pointer point to the tail of the array and traverse from the tail to head. We do adjustment below when we face specific situations.**

**1. when sum == target, we get the right result.**

**2. when sum > target, we move the large element to make sum a little smaller.**

**3. when sum < target, we move the small element to make sum a little larger.**

```java
class Solution{
  public int[] twoSum(int[] numbers, int target){
    if(numbers == null) return null;
    int i = 0;
    int j = numbers.length - 1;
    while(i < j){
      int sum = numbers[i] + numbers[j];
      if(sum == target){
        int[] newList = new int[]{i+1, j+1}
        return newList;
      }else if(sum < target){
        i++;
      }else{
        j--;
      }
    }
    return null;
  }
}
```

## 2. Sum of square numbers

Given a non-negative integer c, decide whether there're two integers a and b such that a^2+b^2 = c.(problem 633)

Example 1:

Input: c = 5;

Output: true;

Explanation: 1 * 1 + 2 * 2 = 5

Example 2:

Input: c = 3;

Output: false

**This problem is changed a little from prolem 167. We also use double pointter to solve this problem. The left pointer point to 0 and the right pointer point to sqrt(c).**

```java
class Solution{
  public boolean judgeSquareSum(int c){
    if(c < 0) return null;
    int i = 0;
    int j = (int)Math.sqrt(c);
    while(i < j){
      int sum = i * i + j * j;
      if(sum == c){
        return true;
      }else if(sum < c){
        i++;
      }else{
        j--
      }
    }
    return false;
  }
}
```

## 3. Reverse vowels of a string

Given a string s, reverse only all the vowels in the string and return it. The vowels are 'a', 'e', 'i', 'o', 'u', and they can appear in both cases.(problem 345)

Example 1:

Input: s = "hello"

Output: "holle"

**We still use double pointer to solve this problem. One pointer points to the head of s and remove from head to tail. Another pointer points to the tail of s and remove from tail to head. During this process, if both head pointer and tail pointer contains vowels, we exchange two vowels.**

```java
class solution{
  public String reverseVowels(String s){
    if(s == null) return null;
    int i = 0;
    int j = s.length()-1;
    char[] output = new char[s.length()];
    while(i <= j){
      char si = s.charAt[i];
      char sj = s.charAt[j];
      if(!vowels.contains(si)){
        output[i++] = si;
      }else if(!vowels.contains(sj)){
        output[j--] = sj;
      }else{
        output[i++] = sj;
        output[j--] = si;
      }
    }
    return new String(output);
  }
  private final static HashSet<Character> vowels = new HashSet<>(
    Array. asList('u', 'A', 'E', 'I', 'O', 'U', 'a', 'e', 'i', 'o')
  );
}
```

## 4. Valid palindrome II

Given a string s, return true if the s can be palindrome after deleting at most one character from it.(problem 680)

Example 1:

Input: s = "aba"

Output: true

Example 2:

Input: s = "abca"

Output: true

Explanation: You could delete the character 'c'

**Actually, this problem can be divide into two conditions. If the 's' is already a palindrome, the 's' must be palindrome after deleting at most one character from it. However, if the 's' is not a palindrome, we have to judge whether the 's' is apalindrome after deleting at most one character from it.** 

```java
class Solution{
  private boolean isPalindrome(String s, int i, int j){
    while(i < j){
      if(s.charAt(i++) != s.charAt(j--)){
        return false;
      }
    }
    return true;
  }
  public boolead validPalindrome(String s){
    for (int i = 0, j = s.length()-1; i < j; i++, j--){
      if(s.charAt(i) != s.charAt(j)){
        boolean result = isPalindrome(s, i + 1, j) || isPalindrome(s, i, j - 1);
        return result;
      }
    }
    return true;
  }
}
```

## 5. Merge sorted list

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively. Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be store dinside the array nums1. To accommodate this, nums1 has a length of m+n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example 1:

Input: nums1 = [1, 2, 3, 0, 0, 0], m = 3, nums2 = [2, 5, 6], n = 3

Output: [1, 2, 2, 3, 5, 6]

Explanation: The arrays we are merging are [1, 2, 3] and [2, 5, 6]. The result of the merge is [1, 2, 2, 3, 5, 6] with the underlined elements coming from nums1.

Example 2:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1

Output: [1]

Explanation: The arrays we are merging are [ ] and [1]. The result of the merge is [1]. Note that because m=0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

**The difficulty of this problem is that we can not merge this list from head to tail. If we do so, the original elements in the nums1 will probably be changed. However, if we merge this list from tail to head, everything work out.**

```java
class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1, j = n - 1;
    int index = m + n - 1;
    while (i >= 0 && j >=0) {
      if (nums1[i] > nums2[j]) {
        nums1[index--] = nums1[i--];
      } else {
        nums1[index--] = nums2[j--];
      }
    }
    while (j >= 0) {
      nums1[index--] = nums2[j--];
    }
  }
}
```

## 6. Linked list cycle

Given head, the head of a linked list, determine if the linked list has a cycle in it. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter. Return true if there is a cycle int ehlinked list. Otherwise, return false. (problem 141)

Example 1:

Input: head = [3, 2, 0, -4], pos = 1

Output: true

Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

**Use two pointers to solve this problem. The first pointer points to head and second pointer points to head.next. The first pointer moves one node each time and the second pointer moves two nodes each time. If two pointers encounter, that means there is a cycle in the given linked list.**

```java
class Solution {
  public boolean hasCycle(ListNode head) {
    if (head == null) return false;
    ListNode l1 = head, l2 = head.next;
    while (l1 != null && l2 != null && l2.next != null) {
      if (l1 == l2) {
        return true;
      } else {
        l1 = l1.next;
        l2 = l2.next.next;
      }
    }
    return false;
  }
}
```

## 7. Linked list cycle II

Given a linked list, return the node where the cycle begins. If there is no cycle, return null. There is a cycle in a linked list if there is some node ine the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter. NOTICE that you should not modify the linked list. (Problem 142)

Examples are same as problem 141.

**First, we use the function in problem 141, which is using two pointers to find the encounter pointer. Then, We set the distance from head to pos as m, the cycle's distance is n, the distance from pos to the meet point as y and the distance from meet point to the pos as x. Because the fast pointer's moving distance is twice as slow pointer. We can get the equation m + kn + y = 2(m + n). Finally, we simplifiy this equation and we have m = x + (k - 1)n. This equation means that if one pointer move from meet point and another point move from head, they will encounter at the node where the cycle begins.**

```java
class Solution {
  if (head == null) return null;
  
  ListNode l1 = head, l2 = head;
  while (l1 != null && l2 != null && l2.next != null) {
    l1 = l1.next;
    l2 = l2.next.next;
    if (l1 != l2) {
      break;
    }
  }
  
  if (l2 == null || l2.next == null) return null;
  
  l2 = head;
  while (l1 != l2) {
    l1 = l1.next;
    l2 = l2.next;
  }
  
  return l1;
}
```

