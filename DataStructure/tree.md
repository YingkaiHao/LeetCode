# Tree

1.[Recursion](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-recursion)

(1).[Maximum depth of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-maximum-depth-of-binary-tree)

(2).[Balanced binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#2-balanced-binary-tree)

## 1. Recursion

### (1). Maximum depth of binary tree

Given the root of a binary tree, return its maximum depth. A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.(problem 104)

Example:

Input: root = [3, 9, 20, null, null, 15, 7]

Output: 3

```java
class Solution {
  public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int max = Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    return max;
  }
}
```

### (2). Balanced binary tree

Given a binary tree, determine if it is height-balanced. For this problem, a height-balanced binary tree is defined as: a binary tree in which the left and right subtrees of every node differ in height by no more than 1.(problem 110)

Example:

Input: root = [3, 9, 20, null, null, 15, 7]

Output: true

```java
class Solution {
  private boolean result = true;
  
  public boolean isBalanced(TreeNode root) {
    maxDepth(root);
    return result;
  }
  
  public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int left = maxDepth(root.left);
    int right = maxDepth(root.right);
    if (Math.abs(left - right) > 1) {
      result = false;
    }
    return Math.max(left, right) + 1;
  }
}
```

