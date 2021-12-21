# 贪心算法

每一次选择都是最优解，不需要去考虑包含选择的子问题的解和不包含选择的子问题的解。

eg. Activity-Selector

```java
Recursive_Activity_Selector(s, f, k, n)
m = k + 1;
while (m <=n && s[m] < f(k)) m = m + 1;

if m <= n 
    return {am} U Recursive_Activity_Selector(s, f, m, n);
else 
    return null;
```

```java
Iterative_Activity_Selector(s, f)
n = s.length;
m = 0;
for (int i = 1; i <= n; i++) {
    if (s[i] >= f[m]) {
        A = A U Ai;
        m = i;
    }
}
return A;
```

1. [455.分配饼干](https://leetcode.com/problems/assign-cookies/)

```java
Input: [1,2,3], [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int glength = 0;
        int slength = 0;
        while (glength < g.length && slength < s.length) {
            if (g[glength] <= s[slength]) {
                glength++;
            }
            slength++;
        }
        return glength;
    }
}
```

2. []()