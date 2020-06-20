# Two Pointer

## 题型判断

- <b><u>已排序</u></b>的array中

## 解题模板

- 

## 例题分析

### *11. Container With Most Water

- 从最大的宽度开始计算

- 从两 边往中间缩小
  - 缩小短的边，保留长的边
  - 缩小过程中不断比较面积大小，保留Max



### 1. 2 sum



### 15. 3 sum

- 排序
- 循环一个值，找two sum



### [16. 最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)

首先进行数组排序，时间复杂度 O(nlogn)
在数组 nums 中，进行遍历，每遍历一个值利用其下标i，形成一个固定值 nums[i]
再使用前指针指向 start = i + 1 处，后指针指向 end = nums.length - 1 处，也就是结尾处
根据 sum = nums[i] + nums[start] + nums[end] 的结果，判断 sum 与目标 target 的距离，如果更近则更新结果 ans
同时判断 sum 与 target 的大小关系，因为数组有序，如果 sum > target 则 end--，如果 sum < target 则 start++，如果 sum == target 则说明距离为 0 直接返回结果

```java
		public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int ans = nums[0] + nums[1] + nums[2];
        for(int i=0;i<nums.length;i++) {
            int start = i+1, end = nums.length - 1;
            while(start < end) {
                int sum = nums[start] + nums[end] + nums[i];
                if(Math.abs(target - sum) < Math.abs(target - ans))
                    ans = sum;
                if(sum > target)
                    end--;
                else if(sum < target)
                    start++;
                else
                    return ans;
            }
        }
        return ans;
    }
```



### *[18. 四数之和](https://leetcode-cn.com/problems/4sum/)

- 思路

  - 四数之和与前面三数之和的思路几乎是一样的。
    如果前面的三数之和会做了的话，这里其实就是在前面的基础上多添加一个遍历的指针而已。
  - 使用四个指针(a<b<c<d)。固定最小的a和b在左边，c=b+1,d=_size-1 移动两个指针包夹求解。
     保存使得nums[a]+nums[b]+nums[c]+nums[d]==target的解。偏大时d左移，偏小时c右移。c和d相
     遇时，表示以当前的a和b为最小值的解已经全部求得。b++,进入下一轮循环b循环，当b循环结束后。
     a++，进入下一轮a循环。 即(a在最外层循环，里面嵌套b循环，再嵌套双指针c,d包夹求解)。

- 重复解

  上面的解法存在重复解的原因是因为移动指针时可能出现重复数字的情况。

  所以我们要确保移动指针后， 对应的数字要发生改变才行。

- 代码

```java
	public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> lists = new ArrayList<>();
            Arrays.sort(nums);
            if (nums.length < 4)
                return lists;
            int a, b, c, d;
            for (a = 0; a <= nums.length - 4; a++) {
                if (a > 0 && nums[a] == nums[a - 1])
                    continue;
                for (b = a + 1; b <= nums.length - 3; b++) {
                    if (b > a + 1 && nums[b] == nums[b - 1])
                        continue;
                    c = b + 1;
                    d = nums.length - 1;
                    while (c < d) {
                        if (nums[a] + nums[b] + nums[c] + nums[d] < target)
                            c++;
                        else if (nums[a] + nums[b] + nums[c] + nums[d] > target) {
                            d--;
                        } else {
                            lists.add(Arrays.asList(nums[a],nums[b],nums[c],nums[d]));
                            while (c < d && nums[c + 1] == nums[c]) 
                                c++;
                            while (c < d && nums[d - 1] == nums[d])
                                d--;
                            c++;
                            d--;
                        }
                    }
                }
            }
            return lists;
    }
```





