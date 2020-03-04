# 动态规划

## 区分分治法

1. 分治法：分解，求解，合并

2. 动态规划：最优子结构，重复子问题，对每个子问题只求解一次

example：

### 钢条切割

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
        res[1] = 1;
        for (int i = 2; i <= n=; i++) {
            res[i] = -Integer.MAX_VALUE;
            for (int j = 1; 2 * j <= i; j++) {
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

[91. Decode Ways](https://leetcode.com/problems/decode-ways/)

```java
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

```java
class Solution {
    public int numDecodings(String s) {
        int[] dp = new int[s.length() + 1];
        dp[0] = 1;
        dp[1] = s.charAt(0) == '0' ? 0 : 1;
        for (int i = 2; i <= s.length(); i++) {
            int first = Integer.valueOf(s.substring(i - 1, i));
            int second = Integer.valueOf(s.substring(i - 2, i));
            if (first > 0 && first <= 9) {
                dp[i] += dp[i - 1];
            }
            if (second >= 10 && second <= 26) {
                dp[i] += dp[i - 2];
            }
        }
        return dp[s.length()];
    }
    
}
```

### LCS(Longest Common Sequence)

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

[646. Maximum Length of Pair Chain](https://leetcode.com/problems/maximum-length-of-pair-chain/)

```java
Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]
```

```java
class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[0] - b[0]);
        int length  = pairs.length;
        if (length == 0) return 0;
        int[] dp = new int[length];
        int maxans = 0;
        for (int i = 0; i < length; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) {
                if (pairs[j][1] < pairs[i][0]) {
                    maxval = Math.max(maxval, dp[j]);
                }
            }
            dp[i] = maxval + 1;
        }
        return Arrays.stream(dp).max().orElse(0);
    }
}
```

[376. Wiggle Subsequence](https://leetcode.com/problems/wiggle-subsequence/description/)

```java
Input: [1,17,5,10,13,15,10,5,16,8]
Output: 7
Explanation: There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].
```

```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        int[] dp = new int[nums.length];
        int[] s = new int[nums.length];
        s[0] = 0;
        for (int i = 0; i < nums.length; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j] && s[j] <= 0) {
                    s[i] = maxval > dp[j] + 1 ? s[j] : 1;
                    maxval = Math.max(maxval, dp[j]);
                } else if (nums[i] < nums[j] && s[j] >= 0) {
                    s[i] = maxval > dp[j] + 1 ? s[j] : -1;
                    maxval = Math.max(maxval, dp[j]);
                }
            }
            dp[i] = maxval + 1;
        }
        return Arrays.stream(dp).max().orElse(0);
    }
}
```

O(N)时间复杂度：

```java
public int wiggleMaxLength(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }
    int up = 1, down = 1;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] > nums[i - 1]) {
            up = down + 1;
        } else if (nums[i] < nums[i - 1]) {
            down = up + 1;
        }
    }
    return Math.max(up, down);
}
```

### Matrix

[64. Minimum Path Sum (Medium)](https://leetcode.com/problems/minimum-path-sum/description/)

```java
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid.length == 0 || grid == null) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 && j != 0) {grid[i][j] += grid[i][j - 1];}
                if (i != 0 && j == 0) {grid[i][j] += grid[i - 1][j];}
                if (i != 0 && j != 0) {dp[i][j] = Math.min(dp[i - 1][j] + grid[i][j], dp[i][j - 1] + grid[i][j]);}
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

[62. Unique Paths](https://leetcode.com/problems/unique-paths/)

```java
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 0 || n == 0) return 0;
        int[][] dp = new int[m][n];
        Arrays.fill(dp, 1);
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

### Array Range

[303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)

```java
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

```java
class NumArray {

    private int[] dp;
    public NumArray(int[] nums) {
        dp = new int[nums.length];
        if (nums.length == 0) return;
        dp[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            dp[i] = nums[i] + dp[i - 1];
        }
    }
    public int sumRange(int i, int j) {
        if (i == 0) return dp[j];
        return dp[j] - dp[i - 1];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```

[413. Arithmetic Slices](https://leetcode.com/problems/arithmetic-slices/description/)

```java
A = [1, 2, 3, 4]

return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.
```

```java
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        if (A.length <= 2) return 0;
        int[] dp = new int[A.length];
        int sum = 0;
        for (int i = 2; i < A.length; i++) {
            if (A[i] - A[i - 1] == A[i - 1] - A[i - 2]) {
                dp[i] = dp[i - 1] + 1;
            }
            sum += dp[i];
        }
        return sum;
    }
}
```

### 股票

[309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```java
Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0 || prices == null) return 0;
        int b1 = -prices[0];
        int s1 = 0;
        int s2 = 0;
        for (int i = 1; i < prices.length; i++) {
            int b0 = Math.max(s2 - prices[i], b1);
            int s0 = Math.max(b1 + prices[i], s1);
            s2 = s1;
            s1 = s0;
            b1 = b0;
        }
        return s1;
    }
}
```

[714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```java
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        if (prices.length == 0 || prices == null) return 0;
        int n = prices.length;
        int s0 = 0;
        int b0 = -prices[0];
        for (int i = 1; i < n; i++) {
            b0 = Math.max(s0 - prices[i], b0);  
            s0 = Math.max(b0 + prices[i] - fee, s0);
        }
        return s0;
    }
}
```

### 字符串编辑

```java
Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        int minstep = 0;
        for (int i = 1; i < m + 1; i++) {
            int maxval = 0;
            for (int j = 1; j < n + 1; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return m + n - 2 * dp[m][n];
    }
}
```

[650. 2 Keys Keyboard](https://leetcode.com/problems/2-keys-keyboard/)

```java
Input: 3
Output: 3
Explanation:
Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.
```

```java
class Solution {
    public int minSteps(int n) {
        int[] dp = new int[n + 1];
        for (int i = 2; i <= n; i++) {
            dp[i] = i;
            for (int j = i - 1; j > 0; j--) {
                if (i % j == 0) {
                    dp[i] = Math.min(dp[i], dp[j] + i / j);
                }
            }
        }
        System.out.println(Arrays.toString(dp));
        return dp[n];
    }
}
```