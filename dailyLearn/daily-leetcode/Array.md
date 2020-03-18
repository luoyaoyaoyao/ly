# Array

1. [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

```java
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> result = new ArrayList<>();
        for (int n : nums) {
            int val = Math.abs(n) - 1;
            nums[val] = -Math.abs(nums[val]);
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                result.add(i + 1);
            }
        }
        return result;
    }
}
```

2. [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```java
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) return 0;
        int min = prices[0];
        int profit = 0;
        for (int price : prices) {
            min = Math.min(price, min);
            profit = Math.max(price - min, profit);
        }
        return profit;
    }
}
```

[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

```java
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int id = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[id++] = nums[i];
            }
        }
        while (id < nums.length) {
            nums[id++] = 0;
        }
    }
}
```

[566. Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)

```java
Input: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
Output: 
[[1,2,3,4]]
Explanation:
The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
```

```java
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        if (nums.length * nums[0].length != r * c || nums.length == 0) return nums;
        int[][] res = new int[r][c];
        int rows = 0;
        int cols = 0;
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                res[rows][cols++] = nums[i][j];
                if (cols == c) {
                    rows++;
                    cols = 0;
                }
            }
        }
        return res;
    }
}
```

[485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/)

```java
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        if (nums.length == 0) return 0;
        int curr = 0;
        int max =0;
        for (int i = 0; i < nums.length; i++) {
            curr = nums[i] == 0 ? 0 : curr + 1;
            max = Math.max(max, curr);
        }
        return max;
    }
}
```

[240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

```java
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = 5, return true.

Given target = 20, return false.

```java

```