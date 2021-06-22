# Lists

## 1. Intersection of two linked lists

Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If two linked lists have no intersection at all, return null. (Problem number 160)

For example, the following two linked lists begin to intersect at node c1:

A:         	 a1 → a2

​								 ↘

​									 c1 → c2 → c3

​								 ↗

B:    b1 → b2 → b3

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

Given the head of a singly linked list, reverse the list and return the reversed list.

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

