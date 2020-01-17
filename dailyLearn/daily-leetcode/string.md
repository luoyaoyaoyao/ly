# String

1. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```java
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Solution1: Sliding window**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int ans = 0;
		int i = 0;
		int j = 0;
		Set<Character> hashSet = new HashSet<>();
		int n = s.length();
		while (i < n && j < n) {
			if (!hashSet.contains(s.charAt(j))) {
				hashSet.add(s.charAt(j++));
				ans = Math.max(ans, j - i);
			} else {
				hashSet.remove(s.charAt(i++));
			}
		}
		return ans;
    }
}
```

**Solution2: Sliding window with HashMap**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int ans = 0;
        int i = -1;
        Map<Character, Integer> hashMap = new HashMap<>();
        int n = s.length();
        for (int j = 0; j < n; j++) {
            if (hashMap.containsKey(s.charAt(j))) {
                i = Math.max(i, hashMap.get(s.charAt(j)));
            }
            ans = Math.max(ans, j - i);
            hashMap.put(s.charAt(j), j);
        }

        return ans;
    }
}
```

2. [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

```java
A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```

```java

```

3. [718. Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

```java
Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

```java

```