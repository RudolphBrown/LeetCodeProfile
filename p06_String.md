#### 0003 Longest Substring Without Repeating Characters

```
给定一个字符串， 寻找字符串中最长的不重复最长子串

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```



1. 滑动窗口
   * C++

| a    | b    | c    | a           | b           | e    | f    |
| ---- | ---- | ---- | ----------- | ----------- | ---- | ---- |
| ①ptr | ③ptr | ⑤ptr | ②重复，断开 | ④重复，断开 |      | ⑥    |

​	

```c++
/** Sliding Window
 * Time Complexity: O(len(s))
 * Space Complexity: O(len(charset))
 */
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        
        int freq[256] = {0};
        
        int l = 0, r = -1; // sliding window: s[l...r]
        int res = 0;
        
        while( r + 1 < s.size()) { 
            
            if( freq[s[r + 1]] == 0 ) // peek
                freq[s[++r]] ++;
            else
                freq[s[l++]] --;
            
            res = max(res, r - l + 1);
                
        }
        
        return res; 
    }
};
```



2. 使用集合

   * Java

   ```java
   public int lengthOfLongestSubstring(String s) {
       int l = 0, r = 0, max = 0;
       Set<Character> set = new HashSet<>();
       
       while (r < s.length()) {
           if (!set.contains(s.charAt(r))) {
               set.add(s.charAt(r++));
               max = Math.max(max, set.size());
           } else {
               set.remove(s.charAt(l++));
           }
       }
       
       return max;
   }
   ```

   

#### 0028 Implement strStr()

1. My sucks Java Solution

```java
class Solution {
    public int strStr(String haystack, String needle) {
        
        int haystackLen = haystack.length();
        int needleLen = needle.length();
        
        if (needleLen == 0)
            return 0;
        
        for (int i = 0; i <= haystackLen - needleLen; i++) {
            for ( int j = 0; j < needleLen && haystack.charAt(i + j) == needle.charAt(j); j++) {
                if ( j + 1 == needleLen ) // needle 找到末尾并且值依然对应
                    return i;
            }       
        }
        return -1;
    }
}
```

2. Excellent C++  Solution

一个循环明明可以控制两个指针， 为什么一定要用两个循环来控制？

```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle == "") return 0;
        if(haystack == "") return -1;
        int i = 0, j = 0;
        while(i < haystack.size() && j < needle.size()){
            if(haystack[i] == needle[j]){
                ++i;
                ++j;
            }
            else{
                i = i - j + 1;
                j = 0;
            }
        }
        if(j == needle.size()) return i - j;
        return -1;
    }
};
```

