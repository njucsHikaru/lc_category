# Sliding Window

## 题型判断

- 用以解决数组/字符串的子元素问题，将嵌套循环问题（暴搜），转换为单循环问题，降低时间复杂度。
- 

## 解题模板

- 我们在字符串 S 中使用双指针中的左右指针技巧，初始化 left = right = 0，把索引闭区间 [left, right] 称为一个「窗口」。

- 我们先不断地增加 right 指针扩大窗口 [left, right]，直到窗口中的字符串符合要求（包含了 T 中的所有字符）。

- 此时，我们停止增加 right，转而不断增加 left 指针缩小窗口 [left, right]，直到窗口中的字符串不再符合要求（不包含 T 中的所有字符了）。同时，每次增加 left，我们都要更新一轮结果。

- 重复第 2 和第 3 步，直到 right 到达字符串 S 的尽头。

  ```java
  public int slidingWindowTemplate(String[] a, ...) {
      // 输入参数有效性判断
      if (...) {
          ...
      }
  
      // 申请一个散列，用于记录窗口中具体元素的个数情况
      // 这里用数组的形式呈现，也可以考虑其他数据结构
      int[] hash = new int[...];
  
      // 预处理(可省), 一般情况是改变 hash
      ...
  
      // l 表示左指针
      // count 记录当前的条件，具体根据题目要求来定义
      // result 用来存放结果
      int l = 0, count = ..., result = ...;
      for (int r = 0; r < A.length; ++r) {
          // 更新新元素在散列中的数量
          hash[A[r]]--;
  
          // 根据窗口的变更结果来改变条件值
          if (hash[A[r]] == ...) {
              count++;
          }
  
          // 如果当前条件不满足，移动左指针直至条件满足为止
          while (count > K || ...) {
              ...
              if (...) {
                  count--;
              }
              hash[A[l]]++;
              l++;
          }
  
          // 更新结果
          results = ...
      }
  
      return results;
  }
  
  ```

  

## 例题分析

### 3. Longest Substring Without Repeating Characters

```java
public int lengthOfLongestSubstring(String s) {
    if(s == null || s.length() == 0) {
      return 0;
    }   
		int[] map = new int[128];
    int l = 0, r = 0, rst = 0;
    while(r < s.length()) {
        map[s.charAt(r)]++;
        while(l <= r && map[s.charAt(r)] > 1) {	//contain repeating characters
            //move the left pointer to minimize the window until it meets the requirement
            char ch = s.charAt(l);
            map[ch]--;
            l++;
        }
        rst = Math.max(rst, r - l + 1);
        r++;
    }
    return rst;
}
```

### 28. Implement strStr()

- O((N-L)*L)
- Rabin Karp
  - 

### 76. Minimum Window Substring

给定一个字符串 S 和一个字符串 T，请在 S 中找出包含 T 所有字母的最小子串。

`输入: S = "ADOBECODEBANC", T = "ABC"	输出: "BANC"`

从最左边开始窗口，记录窗口的开始和结束位置，默认都是0

判断当前字母是否在string中，如果在则扩大窗口，直到包含所有的字母；

- 当前窗口内包含更小的
- 没有滑到的位置包含更小的

--> 缩小窗口

- 满足要求，继续从左缩小
- 不满足，停止缩小，从右边扩大窗口

```
如何快速判断S中的子串包含了T的所有字符？--如何判断 window 即子串 s[left...right] 是否符合要求，是否包含 t 的所有字符呢？
1. HashMap: store all the characters and their number / new int[128]
- winFreq
- tFreq
2. match: 当前有多少个T中的字符已经满足个数条件
- 滑动时，当前字符在win中的val等于t中的val，则match++
- 当match等同于required时，满足条件了，先保存现在的left和right

https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems
```



### 159. Longest Substring with At Most Two Distinct Characters

```java
public int lengthOfLongestSubstringTwoDistinct(String s) {
    if(s == null || s.length() == 0) {
      return 0;            
    }
    int rst = 0, l = 0, r = 0;
    int[] map = new int[128];
    int num = 0;
    while(r < s.length()) {
        map[s.charAt(r)]++;
        if(map[s.charAt(r)] == 1) {
            num++;
        }
        while(l <= r && num > 2) {
            char ch = s.charAt(l);
            map[ch]--;
            if(map[ch] == 0) {
                num--;
            }
            l++;
        }
        if(r - l + 1 > rst) {
            rst = r - l + 1;
        }
        r++;
    }
    return rst;
}
```


### 239. Sliding Window Maximum - 单调队列



### 438. Find All Anagrams in a String







