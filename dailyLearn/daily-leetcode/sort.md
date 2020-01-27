[heap sort]

```java
package com.ly.listStack;

import java.util.Arrays;

public class MaxHeap {

    //堆排序：1.建堆 2.调整堆
    //堆排序两个方法：sortHeap本身和adjustHeap

    public void sortHeap(int[] tmp) {
        //建堆和调整堆
        //sortHeap
        for (int pos = tmp.length / 2 - 1; pos >= 0; pos--) {
            adjustHeap(tmp, pos, tmp.length);
        }

        for (int arrLength = tmp.length - 1; arrLength >= 0; arrLength--) {
            int temp = tmp[0];
            tmp[0] = tmp[arrLength];
            tmp[arrLength] = temp;
            adjustHeap(tmp, 0, arrLength);
        }
    }

    private void adjustHeap(int[] tmp, int pos, int tempLength) {
        while (pos * 2 + 1 < tempLength) {
            int maxValue = 2 * pos + 1;
            if (2 * pos + 2 < tempLength && tmp[maxValue] < tmp[2 * pos + 2]) {
                maxValue = 2 * pos + 2;
            }
            if(tmp[pos]>tmp[maxValue]) return;
            int temp = tmp[pos];
            tmp[pos] = tmp[maxValue];
            tmp[maxValue] = temp;
            pos = maxValue;


        }
    }

    public static void main(String[] args) {
        int[] tmp = new int[]{1, 3, 2, 5, 4, 9,6};
        MaxHeap maxHeap = new MaxHeap();
        maxHeap.sortHeap(tmp);
        System.out.println(Arrays.toString(tmp));

    }
}

```

[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
class Solution {
    public void sortHeap(int[] nums, int k) {
        for (int i = nums.length / 2 - 1; i >= 0; i--) {
            adjustHeap(nums, i, nums.length);
        }

        for (int i = nums.length - 1; i > nums.length - k - 1; i--) {
            int temp = nums[0];
            nums[0] = nums[i];
            nums[i] = temp;
            adjustHeap(nums, 0, i);
        }
    }

    public void adjustHeap(int[] nums, int pos, int templength) {
        while (2 * pos + 1 < templength) {
            int max = 2 * pos + 1;
            if (2 * pos + 2 < templength) {
                max = nums[2 * pos + 1] > nums[2 * pos + 2] ? 2 * pos + 1 : 2 * pos + 2;
            }
            if (nums[pos] > nums[max]) return;
            int temp = nums[pos];
            nums[pos] = nums[max];
            nums[max] = temp;
            pos = max;
        }
    }
    
    public int findKthLargest(int[] nums, int k) {
        sortHeap(nums, k);
        System.out.println(Arrays.toString(nums));
        return nums[nums.length - k];
    }
}
```

QuickSort  
3. [75. Sort Colors](https://leetcode.com/problems/sort-colors/)

Example:

```java
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

Solution:

```java
class Solution {
    public void sortColors(int[] nums) {
        quickSort(nums, 0, nums.length - 1);
    }
    public void quickSort (int[] nums, int p, int r) {
        if (p < r) {
            int q = partition (nums, p, r);
            quickSort (nums, p, q - 1);
            quickSort (nums, q + 1, r);
        }
    }
    
    public int partition (int[] nums, int p, int r) {
        int temp = nums[r];
        int i = p - 1;
        for (int j = p; j < r; j++) {
            if (nums[j] <= temp) {
                i = i + 1;
                int tmp1 = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp1;
            }
        }
        int tmp2 = nums[i + 1];
        nums[i + 1] = nums[r];
        nums[r] = tmp2;
        return i + 1;
    }
}
```

MergeSort
4. [148. Sort List](https://leetcode.com/problems/sort-list/)

Example1:

```java
Input: 4->2->1->3
Output: 1->2->3->4kjhhyhu
```

Example2:

```java
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

Solution:

```java
class Solution {
    public ListNode sortList(ListNode head) {
        return mergeSort(head);
    }

    public ListNode mergeSort(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode slow = head;
        ListNode fast = head;
        ListNode pre = null;
        while (fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        pre.next = null;
        ListNode head1 = mergeSort(head);
        ListNode head2 = mergeSort(slow);
        return merge(head1, head2);
    }

    public ListNode merge(ListNode head1, ListNode head2) {
        ListNode curr1 = head1;
        ListNode curr2 = head2;
        ListNode result = new ListNode(0), result1 = result;
        while (curr1 != null && curr2 != null) {
            if (curr1.val < curr2.val) {
                result.next = curr1;
                curr1 = curr1.next;
            } else {
                result.next = curr2;
                curr2 = curr2.next;
            }
            result = result.next;
        }
        if (curr1 != null) {
            result.next = curr1;
        }
        if (curr2 != null) {
            result.next = curr2;
        }
        return result1.next;
    }
}
```
