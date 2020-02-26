# 动态规划

## 区分分治法

1. 分治法：分解，求解，合并

2. 动态规划：对每个子问题只求解一次

example：

1. 钢条切割

自顶向下的递归求法：  
时间复杂度：2^n

```java
Cut_Rod(p, n)
if n == 0 return 0;
int q = -Integer.Maximum;
for i = 1 -> n
q = Math.max(q, pi + Cut_Rod(p, n - i));
return q;
```

动态规划：

//自底向上法

```java
int[] maxProfit = new int[n];
maxProfit[0] = 0;
maxProfit[1] = 1;
for i = 2 -> n
    for j = 0 -> i
        maxProfit[i] = Math.max(p[i], maxProfit[j] + maxProfit[i - j]);
```

Practice：

[343. Integer Break](https://leetcode.com/problems/integer-break/description/)

Example 1:

```java
Input: 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
Example 2:

Input: 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
```

Solution:

```java
class Solution {
    public int integerBreak(int n) {
        int[] res = new int[n + 1];
        res[0] = 0;
        res[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            res[i] = -Integer.MAX_VALUE;
            for (int j = 1; j < i; j++) {
                res[i] = Math.max(res[i], j * Math.max((i - j), res[i - j]));
            }
        }
        return res[n];
    }
}
```

[279. Perfect Squares](https://leetcode.com/problems/perfect-squares/description/)

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

```java
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

注意不要用sqrt的方法 ，耗性能

```java
class Solution {
    public int numSquares(int n) {
        int[] res = new int[n + 1];
        if (n == 0) return 0;
        res[0] = 0;
        res[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            res[i] = Integer.MAX_VALUE;
            for (int j = 1; i - j * j >= 0; j++) {
                res[i] = Math.min(res[i], res[i - j * j] + 1);
            }
        }
       // System.out.println(Arrays.toString(res));
        return res[n];
    }
}
```

2. LCS(Longest Common Sequence)

Practice:

[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

```java
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
       int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i < m + 1; i++) {dp[i][0] = 0;}
        for (int j = 0; j < n + 1; j++) {dp[0][j] = 0;}
        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                if (text1.charAt(i - 1) == (text2.charAt(j - 1))) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }
}
```

[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

```java
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

Solution:

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int maxans = 1;
        for (int i = 1; i < nums.length; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    maxval = Math.max(maxval, dp[j]);
                }
                dp[i] = maxval + 1;
            }
            maxans = Math.max(maxans, dp[i]);
        }
        return maxans;
    }
}
```

