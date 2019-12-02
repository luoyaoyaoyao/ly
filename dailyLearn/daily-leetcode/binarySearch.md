# 二分查找

## Introduction

Although the basic idea of binary search is comparatively straightforward, the details can be surprisingly tricky...  
实践证明：二分查找细节真的很多，需要好好理解

## 实现三大类模板

* 基本的二分查找算法

* 左侧边界的二分查找

* 右侧边界的二分查找

## 实现技巧

* 不要出现else, 用else if(),把所有情况考虑完全

* 注意搜索区间和while终止条件

* 如需要搜索左右边界，只要在 nums[mid] == target 时做修改即可。搜索右侧时需要减一

### 基本的二分查找算法

```java
int binarySearch(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1; // 注意

    while(left <= right) { // 注意
        int mid = (right + left) / 2;
        if(nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
        }
    return -1;
}
```

### 左侧边界的二分查找

```java
int left_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0;
    int right = nums.length; // 注意

    while (left < right) { // 注意
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
}
```

### 右侧边界的二分查找

```java
int right_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0, right = nums.length;

    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            left = mid + 1; // 注意
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid;
        }
    }
    return left - 1; // 注意
}
```

[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
       if (nums == null || nums.length == 0) return new int[]{-1, -1};
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                right = mid;
            }else if (nums[mid] < target) {
                left = mid + 1;
            }else if (nums[mid] > target) {
                right = mid -1;
            }
        }
        while ((right + 1) <= nums.length - 1 && nums[right + 1] == nums[left]) {
            right = right + 1;
        }
        return nums[left] == target?  new int[]{left, right} : new int[]{-1, -1}; 
    }
}
```

[540. Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        if (nums == null) return -1;
        if (nums.length == 1) return nums[0];
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] != nums[mid - 1] && nums[mid] != nums[mid + 1]) return nums[mid];
            else if (mid % 2 == 0) {
                if (nums[mid] == nums[mid + 1]) {
                    left = mid + 2;
                } else {
                    right = mid - 2;
                }
            } else if (mid % 2 != 0) {
                if (nums[mid] == nums[mid - 1]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }

        }
        return nums[left];
    }
}
```

