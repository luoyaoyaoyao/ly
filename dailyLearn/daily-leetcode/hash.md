# hash

1. [Two Sum](https://leetcode.com/problems/two-sum/)

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```java
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

Answer:

```java
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (hashMap.containsKey(target - nums[i])) {
                return new int[]{i, hashMap.get(target - nums[i])};
            }
            hashMap.put(nums[i], i);
        }
        return null;
    }
}
```

2. [Unique Number of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences/)

```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> hashMap = new HashMap<>();
        Arrays.stream(arr).forEach(x -> hashMap.put(x,hashMap.getOrDefault(x, 0) + 1));
        return new HashSet(hashMap.values()).size() == hashMap.size();
    }
}
```

3. [Single Number](https://leetcode.com/problems/single-number/)
