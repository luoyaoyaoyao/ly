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