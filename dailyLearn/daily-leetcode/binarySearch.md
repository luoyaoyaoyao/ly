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

