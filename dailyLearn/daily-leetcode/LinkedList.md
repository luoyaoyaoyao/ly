# LinkedList

1. 单链表Insert和Delete在O(1)时间内实现  
LinkedList-Insert(L, x)  
x.next = L.head;  
L.head = x;  
LinkedList-Delete(L, x)  
if LinkedList null, return null;  
if x == head, head = head.next;  
if x.next == null, forLook  
else x.val = x.next.val; x.next = x.next.next;  

2. List-Search: 每一次循环需要两个测试（1. x != null && x.val != target）,怎么忽略对x != null的检查.   
哨兵val = k;

3. 动态操作Union,以S1和S2作为输入，返回S1US2所有元素，O(1)时间实现.  
**

4. 链表反转，非递归  
LinkedList-Reverse(L)  
ListNode pre = null, curr = head  
for head -> tail  
next = curr.next;  
curr.next = pre;  
pre = curr;  
curr = next;  

[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

```java
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        		ListNode result = new ListNode(-1);
		ListNode p1 = l1;
		ListNode p2 = l2;
		ListNode curr = result;
		while (p1 != null && p2 != null) {
			if (p1.val <= p2.val) {
				curr.next = new ListNode(p1.val);
				curr = curr.next;
				p1 = p1.next;
			} else {
				curr.next = new ListNode(p2.val);
				curr = curr.next;
				p2 = p2.next;
			}
			
		}
		if (p1 != null) curr.next = p1;
		if (p2 != null) curr.next = p2;
		return result.next;
        
    }
}
```