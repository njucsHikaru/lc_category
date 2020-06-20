# Binary Search

## 题型判断



## 解题模板

- 

## 例题分析

### 4. Median of Two Sorted Arrays

- 时间复杂度要求：O(log (m+n)) --> binary search
- <b>trick to find the median:</b> 
  - 分别找第 (m+n+1) / 2 个，和 (m+n+2) / 2 个，然后求其平均值即可，这对奇偶数均适用。
  - 若 m+n 为奇数的话，那么其实 (m+n+1) / 2 和 (m+n+2) / 2 的值相等，相当于两个相同的数字相加再除以2，还是其本身。

- 在两个数组中找到第K个元素

