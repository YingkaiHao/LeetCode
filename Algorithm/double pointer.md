# Double Pointer

1. [Two sum II-Input array is sorted](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#1-two-sum-ii-input-array-is-sorted)
2. [Sum of square numbers](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#2-sum-of-square-numbers)
3. [Reverse vowels of a string](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#3-reverse-vowels-of-a-string)
4. [Valid palindrome II](https://github.com/YingkaiHao/LeetCode/blob/main/Algorithm/double%20pointer.md#4-valid-palindrome-ii)

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



