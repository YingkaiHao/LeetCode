# Tree

1.[Recursion](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-recursion)

(1).[Maximum depth of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-maximum-depth-of-binary-tree)

(2).[Balanced binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#2-balanced-binary-tree)

(3).[Diameter of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#3-diameter-of-binary-tree)

(4).[Invert binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#4-invert-binary-tree)

(5).[Merge two binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#5-merge-two-binary-trees)

(6).[Path sum](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#6-path-sum)

(7).[Path sum III](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#7-path-sum-iii)

(8).[Subtree of another tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#8-subtree-of-another-tree)

(9).[Symmetric tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#9-symmetric-tree)

(10).[Minimum depth of binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#10-minimum-depth-of-binary-tree)

(11).[Sum of left leaves](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#11-sum-of-left-leaves)

(12).[Longest univalue path](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#12-longest-univalue-path)

(13).[House robber III](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#13-house-robber-iii)

(14).[Second minimum node in a binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#14-second-minimum-node-in-a-binary-tree)

2.[Traverse](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#2-traverse)

(1).[Average of levels in binary tree](https://github.com/YingkaiHao/LeetCode/blob/main/DataStructure/tree.md#1-average-of-levels-in-binary-tree)

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

### (8). Subtree of another tree

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise. A subtree of a binary tree is a tree that consists of a node in tree and all of this node's descendents. The tree could also be considered as a subtree of itself. (Problem 572)

Example1:

```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

Example2:

```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
```

```java
class Solution {
  public boolean isSubtree(TreeNode root, TreeNode subRoot) {
    if (root == null) return false;
    boolean result = isNewSubtree(root, subRoot) || isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    return result;
  }
  private boolean isNewSubtree(TreeNode root, TreeNode subRoot) {
    if (root == null && subRoot == null) return true;
    if (root == null || subRoot == null) return false;
    if (root.val != subRoot.val) return false;
    boolean result = isNewSubtree(root.left, subRoot.left) && isNewSubtree(root.right, subRoot.right);
    return result;
  }
}
```

### (9). Symmetric tree

Given the root of a binary tree, check whether it is a mirror of itself(i.e., symmetric around its center) (problem 101)

Example:

```
Input: root = [1,2,2,3,4,4,3]
Output: true
```

```java
class Solution {
  public boolean isSymmetric(TreeNode root) {
    if (root == null) return false;
    boolean result = isLeafSymmetric(root.left, root.right);
    return result;
  }
  
  private boolean isLeafSymmetric(TreeNode l1, TreeNode l2) {
    if (l1 == null && l2 == null) return true;
    if (l1 == null || l2 == null) return false;
    if (l1.val != l2.val) return false;
    boolean result = isLeafSymmetric(l1.left, l2.right) && idLeafSymmetric(l1.right, l2.left);
    return result;
  }
}
```

### (10). Minimum depth of binary tree

Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node. (Problem 111)

Example:

```
Input: root = [3,9,20,null,null,15,7]
Output: 2
```

```java
class Solution {
  public int minDepth(TreeNode root) {
    if (root == null) return 0;
    int left = minDepth(root.left);
    int right = minDepth(root.right);
    if (left == 0 || right ==0) {
      return left + right + 1;
    }
    return Math.min(left, right) + 1;
  }
}
```

### (11). Sum of left leaves

Given the root of a binary tree, return the sum of all left leaves. (Problem 404)

Example:

```
Input: root = [3,9,20,null,null,15,7]
Output: 24
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.
```

```java
class Solution {
  public int sumOfLeftLeaves(TreeNode root) {
    if (root == null) return 0;
    if (leftOrNot(root.left)) {
      return root.left.val + sumOfLeftLeaves(root.right);
    }
    return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
  }
  
  private boolean leftOrNot(TreeNode root) {
    if (root == null) return false;
    boolean result = root.left == null && root.right == null;
    return result;
  }
}
```

### (12). Longest univalue path

Given the root of a binary tree, return the length of the longest path, where each node in the path has the same value. This path may or may not pass through the root. The length of the path between two nodes is represented by the number of edges between them. (Problem 687)

Example 1:

```
Input: root = [5,4,5,1,1,5]
Output: 2
```

Example 2:

```
Input: root = [1,4,5,4,4,5]
Output: 2
```

```java
class Solution {
  private int path = 0;
  
  public int longestUnivaluePath(TreeNode root) {
    findPath(root);
    return path;
  }
  
  private int findPath(TreeNode root) {
    int leftPath = 0;
    int rightPath = 0;
    if (root == null) return 0;
    int left = findPath(root.left);
    int right = findPath(root.right);
    if(root.left != null && root.left.val == root.val) {
      leftPath = left + 1;
    } else {
      leftPath = 0;
    }
    if(root.right != null && root.right.val == root.val) {
      rightPath = right + 1;
    } else {
      rightPath = 0;
    }
    path = Math.max(path, leftPath + rightPath);
    return Math.max(leftPath, rightPath);
  }
}
```

### (13). House robber III

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root. Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this places form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night. Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police. (Problem 337)

Example 1:

```
Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

Eample 2:

```
Input: root = [3,4,5,1,3,null,1]
Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

```java
class Solution {
  Map<TreeNode, Integer> map = new HashMap<>();
  
  public int rob(TreeNode root) {
    if (root == null) return 0;
    if (map.containsKey(root)) return map.get(root);
    
    int value1 = root.val;
    if (root.left != null) {
      value1 += rob(root.left.left) + rob(root.left.right);
    }
    if (root.right != null) {
      value2 += rob(root.right.left) + rob(root.right.right);
    }
    
    int value2 = rob(root.left) + rob(root.right);
    int result = Math.max(value1, value2);
    map.put(root, result);
    
    return result;
  }
}
```

### (14). Second minimum node in a binary tree

Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property root.val = min(root.left.val, root.right.val) always holds.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree. If no such second minimum value exists, output -1 instead.

Example 1:

```
Input: root = [2,2,5,null,null,5,7]
Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```

Example 2:

```
Input: root = [2,2,2]
Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
```

```java
class Solution {
  public int findSedondMinimumValue(TreeNode root) {
    if (root == null) return -1;
    if (root.left == null && root.right == null) return -1;
    int leftValue = root.left.val;
    int rightValue = root.right.val;
    
    if (leftValue == root.val) {
      leftValue = findSecondMinimumValue(root.left);
    }
    
    if (rightValue == root.val) {
      rightValue = findSecondMinimumValue(root.right);
    }
    
    if (leftValue != -1 && rightValue != -1) return Math.min(leftValue, rightValue);
    if (leftValue != -1) return leftValue;
    return rightValue;
  }
}
```

## 2. Traverse

### (1). Average of levels in binary tree

Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. (Problem 637)

Example 1:

```
Input: root = [3,9,20,null,15,7]
Output: [3.00000,14.50000,11.00000]
Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].
```

Example 2:

```
Input: root = [3,9,20,15,7]
Output: [3.00000,14.50000,11.00000]
```

```java
class Solution {
  public List<Double> average(TreeNode root) {
    ListNode<Double> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!root.isEmpty()) {
      int size = queue.size();
      double sum = 0;
      for (int i = 0; i < size; i++) {
        TreeNode node = queue.poll();
        sum += node.val;
        if (node.left != null) queue.add(node.left);
        if (node.right != null) queue.add(node.right);
      }
      result.add(sum/size);
    }
    return result;
  }
}
```

