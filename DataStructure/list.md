# Lists

1. [ Intersection of two linked lists](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#1-intersection-of-two-linked-lists)
2. [Reverse linked list](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#2-reverse-linked-list)
3. [Merge two sorted lists](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#3-merge-two-sorted-lists)
4. [Remove duplicates from sorted lists](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#4-remove-duplicates-from-sorted-list)
5. [Remove Nth node from end of list](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#5-remove-nth-node-from-end-of-list)
6. [Swap nopes in pairs](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#6-swap-nodes-in-pairs)
7. [Add two numbers II](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#7-add-two-numbers-ii)
8. [Palindrome linked list](https://github.com/YinghaiHao/LeetCode/blob/main/DataStructure/list.md#8-palindrome-linked-list)

## 1. Intersection of two linked lists

Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If two linked lists have no intersection at all, return null. (Problem 160)

For example, the following two linked lists begin to intersect at node c1:

A:         	  a1 → a2 → c1 → c2 → c3

B:    b1 → b2 → b3 → c1 → c2 → c3

It is guaranteed that there are no cycles anywheres in the entire linked structure.

Note that the linked lists must retain their original structure after the function returns.

Could you write a solution that runs in O(n) time and use O(1) memory?

**The solution is quiet classic. We could assume that the length of A is a+c and the length of B is b+c. In this problem, c is the length of the common part of the tail of A and B. So, we could know that a+c+b = b+c+a.**

**When the pointer point to the tail of A list, we could set the pointer to the head of B list. Similarly, when the pointer point the tail of B list, we could set the pointer to the head of A list. By doing so, we could control the pointer point to the intersection of two linked lists.**

```java
//Defination for singly-linked list
public class ListNode{
  int val;
  ListNode next;
  ListNode(int X){
    val = x;
    next = null;
  }
}

public class Solution{
  public ListNode getIntersectionNode(ListNode headA, ListNode headB){
    if(headA == null || headB == null) return null;
    ListNode a_pointer = headA;
    ListNode b_pointer = headB;
    while(a_pointer != b_pointer){
      if(a_pointer == null){
        a_pointer = headB;
      }else{
        a_pointer = a_pointer.next;
      }
      if(b_pointer == null){
        b_pointer =headA;
      }else{
        b_pointer = b_pointer.next;
      }
    }
    return a_pointer
  }
}
```



## 2. Reverse linked list

Given the head of a singly linked list, reverse the list and return the reversed list. (problem 206)

Example:

Input: head = [1,2,3,4,5]

Output: [5,4,3,2,1]

A linked list can be reversed either iteratively or recursively. Could you implement both?

**An iteratively method:**

```java
class Solution{
  public listNode reverseList(ListNode head){
    ListNode prev = null;
    ListNode curr = head;
    ListNode next = null;
    while(curr != null){
      //save next
      next = curr.next;
      //reverse
      curr.next = prev;
      //advance prev and curr
      prev = curr;
      curr = next;
    }
    return prev;
  }
}
```

**A recursively method:**

```java
class Solution{
  public ListNode reverseList(ListNode head){
    if(head == null || head.next == null){
      return head;
    }
    ListNode nextNode = head.next;
    curr.next = null;
    ListNode rest = reverseList(nextNode);
    nextNode.next = curr;
    return rest;
  }
}
```

## 3. Merge two sorted lists

Merge two sorted linked and return as a sorted list. The list should be made by splicing together the nodes of the first two lists.(problem 21)

Example:

Input: l1 = [1, 2, 4], l2 = [1, 3, 4]

Output: [1, 1, 2, 3, 4, 4]

Constraints:

1. The number of nodes in both lists is in the range[0, 50].
2. -100 <= Node.val <= 100
3. Both l1 and l2 are sorted in non-decreasing order.

**When we doing linked list problems, we can have a temp_node just to hold the heads place. So, as we do all this problems at the very end, we just return temp_node.next to get the actual head we need.** 

**In this problem, we first set a list with temp_node. Next, to traverse twe linked lists, we set a pointer current_node to temp_node. Then, traverse twe linked lists using current_node and return as a sorted list.**

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode temp_node = new ListNode(0);
        ListNode current_node = temp_node;
        
        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                current_node.next = l1;
                l1 = l1.next;
            }else{
                current_node.next = l2;
                l2 = l2.next;
            }
            
            current_node = current_node.next;
        }
        
        if(l1 == null && l2 != null){
            current_node.next = l2;
            l2 = l2.next;
        }else if(l2 == null && l1 != null){
            current_node.next = l1;
            l1 = l1.next;
        }
        
        return temp_node.next;
    }
}
```

## 4. Remove duplicates from sorted list

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well. (problem 82)

Example:

Input: head = [1, 2, 3, 3, 4, 4, 5]

Output: [1, 2, 5]

Constraints:

1. The number of nodes in the list is in the range[0, 300].
2. -100 <= Node.val <= 100
3. The list is guaranteed to be sorted in ascending order.

A method is reference from [leetcode solution](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/solution/).

**I use the approach called "sentinel head + predecessor". Sentinel nodes are widely used for trees and linked lists. They are purely functional and usually don't hold any data. Their primary purpose is to standardize the situation to avoid edge case handling.**

**For example, we could use pseudo-head with zero value to ensure that the situation "delete the list head" could never happen, and all nodes to delete are "inside" the list. (This is a really useful method)**

**In this problem, the input list is sorted, and we can determine if a node is a duplicate by comparing its value to the node afte it in the list. Step by step, we could identify the current sublist of duplicates.**

**Now, since we find the duplicates, it's time to delete it using pointer manipulations. Note that the first node in the duplicates sublist should be removed as well. That means that we have to track the predecessor of duplicates sublist, i,e., the last node before the sublist of duplicates**.

**Then, we use predecessor to skip the entire duplicate sublist and make predecessor to point to the node after the sublist.**

**Finally, I really want to mention that the "while" loop is really useful when we handle data structure problem.**

```java
class Solution{
  public ListNode deleteDuplicates(ListNode head){
    ListNode sentinel = new ListNode(0, head);
    ListNode pred = sentinel;
    
    while(head != null){
      if(head.next != null && head.val == head.next.val){
        //This while is use for skip the duplicates that duplicate more than two times.
        while(head.next != null && head.val == head.next.val){
          head = head.next;
        }
        pred.next = head.next;
      }else{
        pred = pred.next;
      }
    }
    
    return sentinel.next;
  }
}
```

## 5. Remove Nth node from end of list

Given the head of a linked list, remove the nth node from the end of the list and return its head. (Problem 19)

Example:

Input: head = [1, 2, 3, 4, 5], n = 2

Output: [1, 2, 3, 5]

Constraints:

1. The number of nodes in the list is sz
2. 1 <= sz <= 30
3. 0 <= sz <= 100
4. 1 <= n <= sz

There are two methods I reference from [leetcode solution](https://leetcode.com/problems/remove-nth-node-from-end-of-list/solution/).

### Approach 1: Two pass algorithm

When we first read the problem, it is easy to find out that we are going to remove the node whose length is L-n+1(L is the list length). If we figure out this length, we could relink next pointer of the (L-n)th node to the (L-n+2)th node and the problem solved. So, the only thing we do not know is L which is the list length. We figure out the list length. Then, the problem solved.

Before we start calculating the length, first we will add an auxiliary "dummy" node, which points to the list head. The "dummy" node is used to simlify some corner cases such as list with only one node, or removing the head of the list.

```java
class Solution{
  public ListNode removeNthFromEnd(ListNode head, int n){
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    int length = 0;
    ListNode first = head;
    while(first != null){
      length++;
      first = first.next;
    }
    length -= n;
    first = dummy;
    while(length > 0){
      length--;
      first = first.next;
    }
    first.next = first.next.next;
    return dummy.next;
  }
}
```

### Approach 2: One pass algorithm

I didn't figure out this method until I see it. Instead of using one pointer, we could use two pointers. The first pointer advances the list by n+1 steps from teh beginning, while the second pointers starts from the beginning of the list. Now, both pointers are exactly separated by n nodes apart. We maintain this constant gap by advancing both pointers together until the first pointer arrives past the last node. And second pointer will be pointing at the nth node counting from the last. We relink the next pointer of the node referenced by the second pointer to point to the node's next next node.

```java
class Solution{
  public ListNode removeNthFromEnd(ListNode head, int n){
    ListNode dummy = new listNode(0);
    dummy.next = head;
    ListNode first = dummy;
    LisrNode second = dummy;
    
    for(int i = 1; i <= n+1, i++){
      first = first.next;
    }
    
    while(first != null){
      first = first.next;
      second = second.next;
    }
    
    second.next = second.next.next;
    return dummy.next;
  }
}
```

## 6. Swap nodes in pairs

Given a linked list, swap every two adjacent nodes and return its head. **You must solve the problem without modifying the values in the list's nodes(i.e., only nodes themselves may be changed.)**(problem 24)

Example:

Input: head = [1, 2, 3, 4]

Output: [2, 1, 4, 3]

Constraints:

1. The number of nodes in the list is in the range[0, 100].
2. 0 <= Node.val <= 100

```java
class Solution{
  public ListNode swapPairs(ListNode head){
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode pre = dummy;
    
    while(pre.next != null && pre.next.next != null){
      ListNode l1 = pre.next;
      ListNode l2 = pre.next.next;
      ListNode l3 = l2.next;
      
      l1.next = l3;
      l2.next = l1;
      pre.next = l2;
      
      pre = l1;
    }
    return dummy.next;
  }
}
```

## 7. Add two Numbers II

You are given two non_empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number itself.

Example:

Input: l1 = [7, 2, 4, 3], l2 = [5, 6, 4]

Output: [7, 8, 0, 7]

Constrains: 

1. The number of nodes in each linked list is in range[0, 100].
2. 0 <= node.val <= 9
3. It is guaranteed that the list represents a number that does not have leading zeros.

**The main difficulty in this problem is that the order of the digits in the list is the opposite of the order in which we do addition. To deal with all digits reversely, we could use stack. First, we push all numbers into stacks. Then, we get them out and do addition. Here, we use a specialty of stack, which is the orders we push numbers in and out are opposite. In this case, we could reverse lists and do addition.**

```java
class Solution{
  public ListNode addTwoNumebers(ListNode l1, ListNode l2){
    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack1 = new Stack<>();
    while(l1 != null){
      stack1.push(l1.val);
      l1 = l1.next;
    }
    while(l2 != null){
      stack2.push(l2.val);
      l2 = l2.next;
    }
    
    ListNode head = new ListNode(0);
    int carry = 0;
    while(!stack1.isEmpty() || !stack2.isEmpty() || carry != 0){
      int a = stack1.isEmpty() ? 0 : stack1.pop();
      int b = stack2.isEmpty() ? 0 : stack2.pop();
      
      int sum = a + b + carry;
      carry = sum/10;
      ListNode new_node = new ListNode(sum%10);
      
      new_node.next = head.next;
      head.next = new_node;
    }
    
    return head.next;
  }
}
```

## 8. Palindrome linked list

Given the head of a singly linked list, return true if it is a palindrome. (Problem 234)

Example:

Input: head = [1, 2, 2, 1]

Output: true

Constraints:

1. The number fo nodes in the list is in the range[1, 100000]
2. 0 <= node.val <= 9

Follow up: O(n) time and O(1) space.

**The method of this problem is quite easy. We could combine some of the methods above to solve this problem. Firstly, we have to cut the linked list from middle to two separate listsm, like l1 list and l2 list.  Then, we reverse l2 list and compare each node from the newly l2 list and each node from l1 list. If all nodes are same, the linked list is a palindrome.**

```java
class Solution{
  public boolean isPalindrome(ListNode head){
    if(head == null || head.next = null) return true;
    //mark a pointer before head
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    //calculate the length of the linked list
    ListNode node = head;
    int length = 0;
    while(node != null){
      length++;
      node = node.next;
    }
    //Using "length" to cut the linked list from middle into two separate lists
    ListNode new_node = dummy;
    if(length % 2 == 0){
      int new_length = length/2;
      while(new_length > 0){
        new_length--;
        new_node = new_node.next;
        head = head.next;
      }
      new_node = new_node.next;
    }else{
      int new_length = length/2;
      while(new_length > 0){
         new_length--;
         new_node = new_node.next;
         head = head.next;
       }
      new_node = new_node.next.next;
    }
    
    //reverse the list from behind and compare each node.val
    ListNode newHead = reverseList(new_node);
    //use dummy
    head = dummy.next;
    return isEqual(newHead, head);
  }
  
  //The method which used to reverse list
  private ListNode reverseList(ListNode l){
    ListNode newHead = new ListNode(0);
    while(l != null){
      ListNode next = l.next;
      l.next = newHead.next;
      newHead.next = l;
      l = next;
    }
    return newHead.next;
  }
  //The method which used to compare l1 and l2 lists
  private boolean isEqual(ListNode l1, ListNode l2){
    while(l1 != null && l2 != null){
      if(l1.val != l2.val) return false;
      l1 = l1.next;
      l2 = l2.next;
    }
    return true;
  }
}
```

