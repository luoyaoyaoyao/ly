# Fibnacci

## DP

[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

```java
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) return n;
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

[198. House Robber](https://leetcode.com/problems/house-robber/)

```java
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        int pre1 = 0; int pre2 = 0;
        for (int i = 0; i < nums.length; i++) {
            int curr = Math.max(pre1 + nums[i], pre2);
            pre1 = pre2;
            pre2 = curr; 
        }
        return pre2;
    }
}
```

[213. House Robber II](https://leetcode.com/problems/house-robber-ii/)

```java
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        if (nums.length == 1) return nums[0];
        return Math.max(rob(nums, 0, nums.length - 1), rob(nums, 1, nums.length));
        }
        public int rob(int[] nums, int start, int end) {
            int pre1 = 0;
            int pre2 = 0;
            for (int i = start; i < end; i++) {
                int curr = Math.max(pre1 + nums[i], pre2);
                pre1 = pre2;
                pre2 = curr;
            }
            System.out.println(pre2);
            return pre2;
        }
}
```

## Finacci heap