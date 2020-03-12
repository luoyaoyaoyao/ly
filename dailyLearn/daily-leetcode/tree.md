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

7. [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

```java
Given a binary tree
          1
         / \
        2   3
       / \     
      4   5    
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int count = 1;
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        dfs(root);
        return count - 1;
    }
    public int dfs(TreeNode root) {
        if (root == null) return 0;
        int L = dfs(root.left);
        int R = dfs(root.right);
        count = Math.max(count, L + R + 1);
        //System.out.println(root.val + " " + Math.max(L, R));
        return Math.max(L, R) + 1;
    }
}
```

8. [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

```java
Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode left = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(left);
        return root;
    }
}
```

9. [112. Path Sum](https://leetcode.com/problems/path-sum/)

```java
Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        if (root.left == null && root.right == null && root.val == sum) return true;
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```

10. [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/)

```java
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

```java
public int pathSum(TreeNode root, int sum) {
    if (root == null) return 0;
    int ret = pathSumStartWithRoot(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
    return ret;
}

private int pathSumStartWithRoot(TreeNode root, int sum) {
    if (root == null) return 0;
    int ret = 0;
    if (root.val == sum) ret++;
    ret += pathSumStartWithRoot(root.left, sum - root.val) + pathSumStartWithRoot(root.right, sum - root.val);
    return ret;
}
```

11. [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

```java
Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its minimum depth = 2.
```

```java
class Solution {
     public int minDepth(TreeNode root) {
        //int ans = 0;
        if (root == null) return 0;
        if (root.left == null && root.right == null) return 1;
        int L = minDepth(root.left);
        int R = minDepth(root.right);
        if (root.left == null || root.right == null) return L + R + 1;
        return Math.min(L, R) + 1;
    }
```

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    int left = minDepth(root.left);
    int right = minDepth(root.right);
    if (left == 0 || right == 0) return left + right + 1;
    return Math.min(left, right) + 1;
}
```

12. [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/)

```java
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

```java
public int sumOfLeftLeaves(TreeNode root) {
    if (root == null) return 0;
    if (isLeaf(root.left)) return root.left.val + sumOfLeftLeaves(root.right);
    return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
}

private boolean isLeaf(TreeNode node){
    if (node == null) return false;
    return node.left == null && node.right == null;
}
```
