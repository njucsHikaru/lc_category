# Array & String

## 题型判断

- Sorted Array
- Subarray
- two pointer



## 例题分析

### 5. Longest Palindromic Substring

- space: O(1)	---	time: O(n^2)

- Expand Around Center
- 分情况：奇数 、 偶数
- 在每个位置拓展查询最长的回文串



### [6. Z 字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)

- 按行排序

  从左到右迭代 ss，将每个字符添加到合适的行。可以使用当前行和当前方向这两个变量对合适的行进行跟踪。

  只有当我们向上移动到最上面的行或向下移动到最下面的行时，当前方向才会发生改变。

- **按行访问**

  https://leetcode-cn.com/submissions/detail/77710046/



### [8. 字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)

- 考察：模拟的是日常开发中对于原始数据的处理



### [26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

- 思路

  数组完成排序后，我们可以放置两个指针 i 和 j，其中 i 是慢指针，而 j 是快指针。

  nums[i] = nums[j]，我们就增加 j 以跳过重复项。

  nums[j] != nums[i]，跳过重复项的运行已经结束，因此我们必须把它 nums[j] 的值复制到 nums[i + 1]。然后递增 i，接着我们将再次重复相同的过程，直到 j 到达数组的末尾为止。

- 代码

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```



### [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

- 思路

  当 nums[j] 与给定的值相等时，递增 j 以跳过该元素。

  当 nums[j] ！= val， 我们复制 nums[j] 到 nums[i] 并同时递增两个索引。重复这一过程，直到 j 到达数组的末尾，该数组的新长度为 i。

- 代码

```java
public int removeElement(int[] nums, int val) {
    int i = 0;
    for (int j = 0; j < nums.length; j++) {
        if (nums[j] != val) {
            nums[i] = nums[j];
            i++;
        }
    }
    return i;
}
```



### 28. Implement strStr()

KMP 算法（Knuth-Morris-Pratt 算法）是一个著名的字符串匹配算法

https://leetcode-cn.com/problems/implement-strstr/solution/kmp-suan-fa-xiang-jie-by-labuladong/



### 30. Substring with Concatenation of All Words

- 思路1
  - 哈希表， O(n^2)
  - 
- 思路2
  - 滑动窗口



### [31. 下一个排列](https://leetcode-cn.com/problems/next-permutation/)

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

- 思路

  创建比当前更大的排列：将数字 a[i-1] 替换为位于其右侧区域的数字中比它更大的数字，例如 a[j]

  可以画个折线图来看一下，比较直观。最后一个波谷a及后面最后一个比a大的值b，swap

  - 从后往前，找到第一个a[i]<a[i+1]的值，然后从最后一个值开始找到a[j]>a[i]; 交换i和j

  - 将「大数」换到前面后，需要将「大数」后面的所有数重置为升序，升序排列就是最小的排列。以 123465 为例：首先按照上一步，交换 5 和 4，得到 123564；然后需要将 5 之后的数重置为升序，得到 123546。显然 123546 比 123564 更小，123546 就是 123465 的下一个排列 ——因为之后一定是逆序的，所以直接reverse即可调整为升序。

- 代码

- 找到a[i-1] < a[i]
- 在i后找到a[j]正好刚刚大于a[i-1]  --  下一个比当前大的，所以需要正好比它大
- 交换a[i-1]和a[j]，且因为a[i]到后面倒是从大到小，所以reverse



### 41. First Missing Positive

**Your algorithm should run in *O*(*n*) time and uses constant extra space.**

- hash: 空间复杂度不符合要求
- binary search: 时间复杂度不符合要求
- 将数组视为哈希表：
  - 交换
    - 注意交换条件
    - 防止死循环
  - 遍历





### 43. Multiply Strings

- 普通竖式：遍历 `num2` 每一位与 `num1` 进行相乘，将每一步的结果进行累加
- 优化竖式：该算法是通过两数相乘时，乘数某位与被乘数某位相乘，与产生结果的位置的规律来完成。
  - 乘数 num1 位数为 M，被乘数 num2 位数为 N， num1 x num2 结果 res 最大总位数为 M+N
  - num1[i] x num2[j] 的结果为 tmp 
    - 位数为两位，"0x","xy"的形式
    - 其第一位位于 res[i+j]
    - 第二位位于 res[i+j+1]

- 代码

  ```java
  public String multiply(String num1, String num2) {
          int m=num1.length(), n=num2.length();
          int[] res_arr = new int[m+n];
          for(int i = m - 1; i >= 0; i--){
              for(int j = n - 1; j >= 0; j--){
                  //current 2 digits product
                  int curProd = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                  //digits in result
                  int carry = i+j, base = i+j+1;
                  //current sum on this 2 digits
                  int sum = curProd + res_arr[base];
                  //sum up for `[i + j`, `i + j + 1]` digits
                  res_arr[carry] += sum/10;
                  res_arr[base] = sum%10;
              }
          }
          //convert to string
          StringBuilder sb = new StringBuilder();
          for(int p : res_arr){
              //take care of leading 0
              if(!(sb.length() == 0 && p == 0)) sb.append(p);
          } 
          return sb.length() == 0 ? "0" : sb.toString();        
      }
  ```

  

### 48. Rotate Image

- #### 方法 1 ：转置加翻转

- #### 方法 2 ：旋转四个矩形

- #### 方法 3：在单次循环中旋转 4 个矩形



### 49. Group Anagrams

- 思路1：常规

  ```java
  class Solution {
      public List<List<String>> groupAnagrams(String[] strs) {
          if (strs.length == 0) return new ArrayList();
          Map<String, List> ans = new HashMap<String, List>();
          for (String s : strs) {
              char[] ca = s.toCharArray();
              Arrays.sort(ca);
              String key = String.valueOf(ca);
              if (!ans.containsKey(key)) ans.put(key, new ArrayList());
              ans.get(key).add(s);
          }
          return new ArrayList(ans.values());
      }
  }
  ```

  

- 思路2：神奇的key分类

  int[] matrix = new int[26];

  把单词abcba的分类key定义为：221



### 54. Spiral Matrix

- 按照顺序加右，下，左，上直到边界。

- 遍历-过程中更新边界信息。

- 交错的时候结束。

首先设定上下左右边界
其次向右移动到最右，此时第一行因为已经使用过了，可以将其从图中删去，体现在代码中就是重新定义上边界
判断若重新定义后，上下边界交错，表明螺旋矩阵遍历结束，跳出循环，返回答案
若上下边界不交错，则遍历还未结束，接着向下向左向上移动，操作过程与第一，二步同理
不断循环以上步骤，直到某两条边界交错，跳出循环，返回答案



### 66. Plus One

加法：

1. 不是9就直接+1 return
2. 是9，就把当前位置为0。继续向前遍历。

结束循环都没有return，则为10...0



### 73. Set Matrix Zeroes

#### 神奇的空间位置记录方式

Given a *m* x *n* matrix, if an element is 0, set its entire row and column to 0. Do it [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm).

观察一下最后结果和当前matrix的关系

- 额外空间
  - row_set, column_set记录行列为0
  - 遍历矩阵根据上述信息置为0
- O(1) space
  - 只更新已经遍历过的表格 
    - 再加一次遍历，时间复杂度高
  - 优化：找一个位置记录。后面再统一遍历
    - 使用第一行和第一列进行记录
    - 更新时，最后更新第一行和第一列
    - 剪枝：















### 163. Missing Ranges

- 下一个要找的数字
- 已有的选项a，去匹配要找的数字n = 下界
  - n1[a] < n: a++
  - n1[a] == n: i++
  - n1[a] > n: add range; n = n1[a] + 1
- 判断最后n和上界的关系



### 229. Majority Element II

- in linear time and in O(1) space
- 摩尔投票法：解决的问题是如何在任意多的候选人中，选出票数超过一半的那个人。注意，是超出一半票数的那个人。
  - 抵消阶段：两个不同投票进行对坑，并且同时抵消掉各一张票，如果两个投票相同，则累加可抵消的次数
    - 初始化候选人和抵消计数
    - 抵消计数为0时，无效抵消，更换新的candidate为当前值
  - 计数阶段：在抵消阶段最后得到的抵消计数只要不为0，那这个候选人是有可能超过一半的票数的，为了验证，则需要遍历一次，统计票数，才可确定



