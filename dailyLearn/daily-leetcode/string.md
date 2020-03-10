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

2. [409. Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)

```java
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

```java
class Solution {
    public int longestPalindrome(String s) {
        int count = 0;
        int[] num = new int[123];
        for (char ch : s.toCharArray()) {
            num[ch]++;
        }
        for (int i : num) {
            count += i / 2 * 2;
        }
        return count < s.length() ? count + 1 : count;
    }
}
```

3. [205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

```java
Input: s = "egg", t = "add"
Output: true
```

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int[] preIndexOfS = new int[256];
        int[] preIndexOfT = new int[256];
        for (int i = 0; i < s.length(); i++) {
            char sc = s.charAt(i), tc = t.charAt(i);
            if (preIndexOfS[sc] != preIndexOfT[tc]) {
                return false;
            }
            preIndexOfS[sc] = i + 1;
            preIndexOfT[tc] = i + 1;
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        return isIsomorphicHelper(s, t) && isIsomorphicHelper(t, s);
    }

    public boolean isIsomorphicHelper(String s, String t) {
        Map<Character, Character> hashMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            if (hashMap.containsKey(s.charAt(i))) {
                if (hashMap.get(s.charAt(i)) != t.charAt(i)) {
                    return false;
                }
            } else {
                hashMap.put(s.charAt(i), t.charAt(i));
            }
        }
        return true;
    }
}
```

4. [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

```java
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

```java
class Solution {
    int count = 0;
    public int countSubstrings(String s) {
        for (int i = 0; i < s.length(); i++) {
            countSubstringHelper(s, i, i);
            countSubstringHelper(s, i, i + 1);;
        }
        return count;
    }
    public int countSubstringHelper(String s, int start, int end) {
        while (start >= 0 && end < s.length() && s.charAt(start) == s.charAt(end)) {
                count++;
                start--;
                end++;
        }
        return count;
    }
}
```

5. [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/description/)

```java
Input: 121
Output: true
```

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) return false;
        String num = String.valueOf(x);
        int start = 0;
        int end = num.length() - 1;
        while (start <= end) {
            if (num.charAt(start++) != num.charAt(end)--) {
                return false;
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) return false;
        int temp = x;
        int result = 0;
        int remainder = 0;
        while (temp != 0 || remainder != 0) {
            remainder = temp % 10;
            result = (result + remiander) * 10;
            temp = temp / 10;
        }
        return result == x;
    }
}
```

6. [696. Count Binary Substrings](https://leetcode.com/problems/count-binary-substrings/description/)

```java
class Solution {
    public int countBinarySubstrings(String s) {
        if (s.length() == 0) return 1;
        int ans = 0;
        int preCount = 0; int currCount = 1;
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                currCount++;
            } else {
                preCount = currCount;
                currCount = 1;
            }
            if (preCount >= currCount) {
                ans += 1;
            }
        }
        return ans;
    }
}
```