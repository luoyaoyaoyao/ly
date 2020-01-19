# tree

1. [Search Insert Position](https://leetcode.com/problems/search-insert-position/
)

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

Example1:

```java
Input: [1,3,5,6], 5
Output: 2
```

Example1:

```java
Input: [1,3,5,6], 2
Output: 1
```

Solution:

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
       int left = 0;
        int right = nums.length;
        while (left < right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) {
                right = mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] > target) {
                right = mid;
            }
        }
        return left;
}
}
```

2. [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given a binary tree, return the inorder traversal of its nodes' values.

Example:

```java
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

```java
class Solution {
    List<Integer> result = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root == null) return new ArrayList<>();;
        inorderTraversal(root.left);
        result.add(root.val);
        inorderTraversal(root.right);
        return result;
    }
}
```

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        stack.push(root);
        TreeNode curr = root;
        while (curr != null && !stack.isEmpty()) {
            while (curr.left != null) {
                curr = curr.left;
                stack.push(curr);
            }
            TreeNode node = stack.pop();
            result.add(node.val);
            
            if (node.right != null) {
                curr = node.right;
                stack.push(curr);
            }
        }
        return result;
        }
}
```

```java
public class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        Stack < TreeNode > stack = new Stack < > ();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}
```

3. [Same Tree](https://leetcode.com/problems/same-tree/)

Given two binary trees, write a function to check if they are the same or not.

```java
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```

Solution:

```java
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
```

4. [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

```java
   1
   / \
  2   2
 / \ / \
3  4 4  3

output: true
```

Solution:

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null || (root.left == null && root.right == null)) {return true;}
	return checkIfSymmetricTree (root.left, root.right);
}

public boolean checkIfSymmetricTree(TreeNode p, TreeNode q) {
    if(p == null && q == null) {return true;}
    if(p == null || q == null) {return false;}
    return p.val == q.val && checkIfSymmetricTree(p.left, q.right) && checkIfSymmetricTree(p.right, q.left); 
}
}
```

5. [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

```java
class Solution {
public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        if (Math.abs(getMaxDepth(root.left) - getMaxDepth(root.right)) > 1) return false;
        return isBalanced(root.left) && isBalanced(root.right);
    }

    public int getMaxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(getMaxDepth(root.left), getMaxDepth(root.right)) + 1;
    }
}
```

6. [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

