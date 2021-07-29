# Tree

1.[Recursion](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-recursion)

(1).[Maximum depth of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-maximum-depth-of-binary-tree)

(2).[Balanced binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#2-balanced-binary-tree)

(3).[Diameter of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#3-diameter-of-binary-tree)

(4).[Invert binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#4-invert-binary-tree)

(5).[Merge two binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#5-merge-two-binary-trees)

(6).[Path sum](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#6-path-sum)

(7).[Path sum III](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#7-path-sum-iii)

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

### (4). Invert binary tree

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

### (5). Merge two binary trees

You are given two binary trees root1 and root2. Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the other are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.(problem 617)

Example: 

Input: root1 = [1, 3, 2, 5] 	root2 = [2, 1, 4, null, 4, null, 7]

Output: [3, 4, 5, 5, 4, null, 7]

```java
class Solution {
  public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) return null;
    if (root1 == null) return root2;
    if (root2 == null) return root1;
    root.left = mergeTrees(root1.left, root2.left);
    root.right = mergeTrees(root2.left, root2.right);
    return root;
  }
}
```

### (6). Path sum

Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targerSum. A leaf is a node with no children. (Problem 112)

Example:

Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1]	targerSum = 22

Output: true

```java
class Solution {
  public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null && root.val == targetSum) return true;
    boolean leftResult = hasPathSum(root.left, targetSum - root.val);
    boolean rightResult = hasPathSum(root.right, targetSum = root.val);
    return leftResult || rightResult;
  }
}
```

### (7). Path sum III

Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targerSum. The path does not need to start or end at the root or a leaf, but it must go downwards(i.e., traveling only from parent nodes to child nodes).

Example:

Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8

Output: 3

Explanation: The paths that sum to 8 are shown.

```java
class Solution {
  public int pathSum(TreeNode root, int targetSum) {
    if (root == null) return 0;
    int result = newPathSum(root, targetSum) + pathSum(root.left, targetSum) + pathSum(root.right, targetSum);
    return result;
  }
  public int newPathSum(TreeNode root, int sum) {
    if (root == null) return 0;
    int result = 0;
    if (root.val == sum) result++;
    result += newPathSum(root.left, sum - root.val) + newPathSum(root.right, sum - root.val);
    return result;
  }
}
```

