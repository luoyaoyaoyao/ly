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



