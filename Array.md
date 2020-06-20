# Array & String

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

