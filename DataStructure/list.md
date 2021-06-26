# Lists

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

**In this problem, the input list is sorted, and we can determine if a node is a duplicate by comparing its value to the node afte it in the list. Step by step, we could identify the current sublist of duplicates.**

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

