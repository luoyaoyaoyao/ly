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