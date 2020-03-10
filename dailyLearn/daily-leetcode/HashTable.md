# HashTable

Points:  

1. 优点: 在合理假设下，在散列表中查找一个元素的平均时间是O(1).

2. 哈希冲突

3. 散列技术（直接寻址表，散列表，散列函数，etc.）.

Practice:

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

Solution 1:

```java
public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        Arrays.stream.forEach(x -> hashMap.put(num, hashMap.getOrDefault(x, 0) + 1));
        for (Map.Entry<Integer, Integer> entry: hashMap.entrySet()){
            if (entry.getValue() == 1){
                return entry.getKey();
            }
        }
        return 0;
    }
```

Solution 2:

```java
public int singleNumber(int[] nums) {
        for (int i = 0; i < nums.length-1; i++){
             nums[i+1] ^= nums[i];
        }
        return nums[nums.length-1];
    }
```

3. [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

```java
Input: [1,2,3,1]
Output: true
```

```java
public boolean containsDuplicate(int[] nums) {
    Arrays.sort(nums);
    for (int i = 0; i < nums.length - 1; ++i) {
        if (nums[i] == nums[i + 1]) return true;
    }
    return false;
}
```

4. [594. Longest Harmonious Subsequence](https://leetcode.com/problems/longest-harmonious-subsequence/)

```java
Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].
```

```java
class Solution {
    public int findLHS(int[] nums) {
        int ans = 0;
        Map<Integer, Integer> hashMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            hashMap.put(nums[i], hashMap.getOrDefault(nums[i], 0) + 1);
        }
        for (int num : hashMap.keySet()) {
            if (hashMap.containsKey(num + 1)) {
                ans = Math.max(ans, hashMap.get(num) + hashMap.get(num + 1));
            }
        }
        return ans;
    }
}
```