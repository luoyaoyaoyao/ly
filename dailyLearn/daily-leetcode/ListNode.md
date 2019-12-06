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