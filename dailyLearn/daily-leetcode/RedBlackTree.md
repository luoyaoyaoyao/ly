# 红黑树

BackGround: BST(O(h))  
>> RBTree: balanced-BST,保证最坏情况下时间复杂度：O(lgn)  

## 红黑树性质

红黑树确保没有一条路径会比其他路径长出2倍，因此近似于平衡的  

1. 每个节点或者是红色的，或者是黑色的

2. 根节点是黑色的

3. 如果一个节点是红色的，那么两个子节点是黑色的

4. 对每个节点，从该节点到其后代叶节点的简单路径上，均包含相同数目的黑色节点

## 旋转

任何一颗含n个节点的二叉搜索树可以通过O(n)次旋转，转变为其他任何一颗含n个节点的二叉搜索树。

左旋

```java
Left_Rotate(T, x)
x.right = y.left;
if (x.p == null)
T.root = y;
else if (x == x.p.left)
y = x.p.left;
else 
y = x.p.right;
y.left = x;
```

右旋

```java
Right_Rotate(T, x)
x.right = y;
if (y.p == null)
T.root = x;
else if (y == y.p.left)
x = y.p.left;
else 
x = y.p.right;
x.right = y;
```

## 插入

时间复杂度: O(lgn)

```java
RB_Insert(T, x)
TreeNode curr = T.root;
TreeNode pre;
while (curr != null || curr.val != x) 
pre = curr;
if (curr.val < x) curr = curr.right;
else curr = curr.left;

if (x < pre.val) pre.left = x;
else pre.right = x;
x.color = RED;
RB_Insert_Fixup(T, x);
```

```java
RB_Insert_Fixup(T, x)
while (x.p.color == Red)
if (x.p = x.p.p.left)
TreeNode y = x.p.p.right;
    if (y.color == RED)
    x.p.color = BLACK;
    y.color = BLACK;
    x.p.p = RED;
    x = x.p.p; //case 1: x的叔节点y是红色的
    else if (x = x.p.right)
    x = x.p;
    Left_Roteate(T, x);  //case 2: y是黑色的，且x是一个右孩子
    z.p.color = BLACK;
    z.p.p.color = RED;
    Right_Rotate(T, x);  
else (same as left)
T.root.colort = BLACK;
```

## 删除

时间复杂度: O(lgn)

```java
RB_Transplant(T, u, v)
if u.p == null
    T.root = v;
else if u == u.p.left
    u.p.left = v;
else if u == u.p.right
    u.p.right = v;
v.p = u.p;
```

```java
RB_Delete(T, z)
z_original_color = z.color;
//similar with BST_DeleteNode
//TreeNode x is the replacement of y
if z_original_color == Black
    RB_Delete_Fixup(T, x)
```


```java
RB_Delete_Fixup(T, x)
while x != T.root && x.color == Black
    if x == x.p.left
        w = x.p.right;
        if w.color == Red
            w.color = Black
            x.p.color = Red
            Left_Rotate(T, x.p)
            w = x.p.right //case 1
        if w.left.color == Black && w.right.color == Black
            w.colort = Red
            x = x.p //case 2
        else if w.right.color == Black
                w.left.color == Black
                w.color = Red
                Right_Rotate(T, w)
                w = x.p.right
                w.color = x.p.color
                x.p.color = Black
                w.right.color = Black
                Left_Rotate(T, x.p)
                x = T.root //case 3
x.color = Black
```