# Binary Search

## 题型判断

- find the first / last position

  - Given an sorted integer array - nums, and an integer - target. 

    Find the **any/first/last** position of target in nums.

    Return **-1** if target doesn’t exist.

- keep the part that must have target in it



## 解题模板

- 

## 例题分析

### 4. Median of Two Sorted Arrays

- 时间复杂度要求：O(log (m+n)) --> binary search
- <b>trick to find the median:</b> 
  - 分别找第 (m+n+1) / 2 个，和 (m+n+2) / 2 个，然后求其平均值即可，这对奇偶数均适用。
  - 若 m+n 为奇数的话，那么其实 (m+n+1) / 2 和 (m+n+2) / 2 的值相等，相当于两个相同的数字相加再除以2，还是其本身。

- 在两个数组中找到第K个元素



### [29. 两数相除](https://leetcode-cn.com/problems/divide-two-integers/)



### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

- 思路： 找到第一个比XXX大/小的值

  画图                                                         

- 代码



### 34. Find First and Last Position of Element in Sorted Array

- 常规找 first / last 

  

### 35. Search Insert Position

- find the first one > target
- 找到两个最近的值
- 注意三种情况

  - < start比较：start
- < end比较：end
  - 找不到大的: length



### 69. Sqrt(x)

- 思路：find thee first one e that e * e > x
- 优化：
  - original: start = 0, end = last 
  - 当 x > 2 时，end = x /2 
- 注意：
  - 大数溢出情况，使用long类型
- Follow up: What if return a double, not integer?
  - 



### 74. Search a 2D Matrix

- 思路1：start from right-up most element, if > current, move updown; else move left
- 思路2：binary search
  - [mid / n]\[mid % n]
  - 从一维数组到两位数组的转换
    - left = 0
    - right = m * n - 1



### 81. Search in Rotated Sorted Array II

- start和mid相等时，start++



### 153. Find Minimum in Rotated Sorted Array

- 没有重复值
- 找到第一个比最后一个值小的数
- \< last one, 那么en = mid



### 154. Find Minimum in Rotated Sorted Array II

- 有重复值
- 如果nums[mid] == target
  - en--
  - target每次都取nums[en]



### 162. Find Peak Element

- 注意边界
- 只需要和下一个值大小比较，缩近范围即可



### 278. First Bad Version

找到第一个为true的值

```java
if(f(mid) == false) {
	start = mid;
}else {
  end = mid;
}
if(f(start) == true)
  return start;
else
  return end;
```

