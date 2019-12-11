# database

[627. Swap Salary](https://leetcode.com/problems/swap-salary/)

```java
update salary set sex = if(sex = 'm', 'f', 'm');
```

```java
UPDATE salary
SET
    sex = CASE sex
        WHEN 'm' THEN 'f'
        ELSE 'm'
    END;
```