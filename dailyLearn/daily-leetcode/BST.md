# Binary Search Tree

支持的集合操作：Search, Inorder, Minimum, Maximum, Predecessor, Successor, Insert, Delete

## Search

伪代码：  

```java
Iterative_Search(TreeNode root, int key):  
TreeNode curr = root;  
while (curr != null && curr.val != ket) {  
    if (curr.val < key>) {
        curr = curr.right;
    } else {
        curr = curr.left;
    }
}
return curr;
```

```java
Recurse_Search(TreeNode root, int key):
TreeNode curr = root;
if (root == null || curr.val == key) return curr;
if (curr.val < key) return Recurse_Search(curr.right);
else return Recurse_Search(curr.left);
```

## Inorder

```java
Recurse_Inorder(TreeNode root):  
if (root == null) return null;
Recurse_Inorder(root.left);
list.add(root);
Recurse_Inorder(root.right);
return list;
```

```java
Iterative_Inorder(TreeNode root):
List<Integer> list = new ArrayList<>();
Stack<Integer> stack = new Stack<>();
while (curr != null || !stack.isEmpty()) {
    while (curr != null) {
        stack.push(curr);
        curr = curr.left;
    }
    TreeNode curr = stack.pop();
    list.add(curr.val);
    curr = curr.right;
}
return lsit;
```

Pracetice:
[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/solution/)

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            result.add(curr.val);
            curr = curr.right;
        }
        return result;
    }
}
```


## Maximum

```java
while (curr.left != null) {
    curr = curr.left
}
return curr;
```

## Minimum 

```java
while (curr.right != null) {
    curr = curr.right;
}
return curr;
```

## Predecessor

```java
Predecessor(TreeNode root, TreeNode treeNode):
if  (treeNode.left != null) return Tree_minimum(treeNode.left);
else:
TreeNode curr = root;
TreeNode pre = null;
while (curr != null && curr != treeNode) {
    pre = curr;
    curr = curr.val < treeNode.val ? curr.right : curr.left;
}
return pre;
```

## Insert

```java
Insert(TreeNode root, TreeNode treeNode):
TreeNode curr = root;
TreeNode pre;
while (curr != null) {
    pre = curr;
    curr = curr.val < treeNode.val ? curr.right : curr.left;
}
if (pre.val < treeNode.val>) pre.right = treeNode;
else pre.left = treeNode;
```

## Delete

1. Search_Node

2. transplant

3. treeDelete

Practice:  
[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

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
    TreeNode delNode = new TreeNode(0);
    TreeNode pre = null;
    public TreeNode deleteNode(TreeNode root, int key) {
        TreeNode curr = root;
        delNode = search(root, key);
        if (pre == null) return treeDelete(delNode);
        else if (pre.left == delNode) pre.left = treeDelete(delNode);
        else if (pre.right == delNode) pre.right = treeDelete(delNode);
        return root;
    }

    public TreeNode treeDelete(TreeNode deleteNode) {
        TreeNode minimum = null;
        if (deleteNode == null) return null;
        if (deleteNode.left == null) {
            return deleteNode.right;
        } if (deleteNode.right == null) {
            return deleteNode.left;
        } else {
            TreeNode pre = treeMinimum(deleteNode.right).get(0);
            minimum = treeMinimum(deleteNode.right).get(1);
            System.out.println(minimum.val);
            if (minimum != deleteNode.right) {
                pre.left = minimum.right;
                minimum.right = deleteNode.right;
            }
            minimum.left = deleteNode.left;
        }
        return minimum;
    }

    public List<TreeNode> treeMinimum(TreeNode treeNode) {
        TreeNode pre = null;
        List<TreeNode> list = new ArrayList<>();
        while (treeNode.left != null) {
            pre = treeNode;
            treeNode = treeNode.left;
        }
        list.add(pre);
        list.add(treeNode);
        return list;
    }

    public TreeNode search(TreeNode root, int key) {
        if (root == null) return root;
        while (root != null) {
            if (root.val == key) {
                return root;
            }
            if (root.val < key) {
                pre = root;
                root = root.right;
            } else if (root.val >= key) {
                pre = root;
                root = root.left;
            }
        }
        return root;
    }
}
```