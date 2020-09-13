# Dynamic Programming

## 题型判断



## 解题模板

- state
  - 包含当前字符在内的最值

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

### [32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)

- *dp*[*i*] 表示以下标 *i* 字符结尾的最长有效括号的长度
- transit func: 
  - *s*[*i*]=‘)’ 且 s[i - 1] =‘(’，也就是字符串形如 “……()”
    - *dp*[*i*]=*dp*[*i*−2]+2
  - *s*[*i*]=‘)’ 且 s[i - 1] =‘)’，也就是字符串形如 “……))” --> 若*s*[*i*−*dp*[*i*−1]−1]=‘(’
    - *dp*[*i*]=*dp*[*i*−1]+*dp*[*i*−*dp*[*i*−1]−2]+2



### 44. Wildcard Matching

![image-20200714003410646](/Users/vicki/Library/Application Support/typora-user-images/image-20200714003410646.png)



### 139. word break

*dp*[*i*]=*dp*[*j*] && *check*(*s*[*j*..*i*−1])

其中 check*(*s*[*j*..*i*−1]) 表示子串 s*[*j*..*i*−1] 是否出现在字典中



### 140. Word Break II

```java
用 List<String> 直接 dp 超时
```





### 70



###115. Distinct Subsequences

- 思路
  - 相等：以下两种情况相加
    - 算上当前字符：dp[i-1]\[j-1]
    - 不算上当前字符，以前的积累: 之前出现过的值dp[i]\[k], 0 < k < j
  - 不等：
    - 看左边的值，如果左边>0，则左边+1
- 注意



### 132. Palindrome Partitioning II

```
dp[i] = min([dp[j] + 1 for j in range(i) if s[j + 1, i] 是回文])
```



### 221. Maximal Square



### 256

### 265

### 300





卫生局