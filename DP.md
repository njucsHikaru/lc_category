# Dynamic Programming

## 题型判断



## 解题模板

- 

## 例题分析

### 5. Longest Palindromic Substring

- 解题思路

  - 最长回文子串 - 
  - 判断是否是回文：
    - state: boolean dp[i]\[j] --  s(i, j) 是否是回文串
    - transit function: s[i]和s[j]是否相等，相等判断 s(i+1, j-1) 是否是回文串
    - Initialization：
      - Len = 1：true
      - len = 2：比较两个字符是否相同
    - 遍历顺序：本来就只要填写半个正方形，从小到大填充

- 代码部分

  - ```java
    dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);
    ```

    

###10. Regular Expression Matching

- 双序列字符串
- dp[i]\[j] : string1的前i个和string2的前j个是否匹配
- 转换方程：
  - Str2[j] == '.'  => dp[i-1]\[j-1]
  - Str2[j] == '*'  => 观察前一个字符
    - 正常字符: dp[i-1]\[j]
      - zero: dp[i]\[j-1]o
      - More:

### 70

### 221

### 256

### 265

### 300





卫生局