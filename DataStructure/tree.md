# Tree

1.[Recursion](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-recursion)

(1).[Maximum depth of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-maximum-depth-of-binary-tree)

(2).[Balanced binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#2-balanced-binary-tree)

(3).[Diameter of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#3-diameter-of-binary-tree)

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

### (3). Diameter of binary tree

Given the root of a binary tree, return the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root. the length of a path between two nodes is represented by the number of edges between them.(problem 543)

Example:

Input: root = [1, 2, 3, 4, 5]

Output: 3

Explanation: 3 is the length of the path [4, 2, 1, 3] or [5, 2, 1, 3]

```java
class Solution {
  private int max = 0;
  
  public int diameterOfBinary(TreeNode root) {
    depth(root);
    return max;
  }
  
  private int depth(TreeNode root) {
    if (root == null) return 0;
    int l = depth(root.left);
    int r = depth(root.right);
    max = Math.max(max, l + r);
    return Math.max(l, r) + 1;
  }
}
```

### (4). Invert Binary Tree

Given the root of a binary tree, invert the tree, and return its root.(problem 226)

Example:

Input: root = [4, 2, 7, 1, 3, 6, 9]

Output: [4, 7, 2, 9, 6, 3, 1]

```java
class Solution {
  public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode right = root.right;
    root.right = invertTree(root.left);
    root.left = invertTree(right);
    return root;
  }
}
```

