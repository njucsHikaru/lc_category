# Greedy

生活中的经验：

在以前还使用现金购物的时候，如果我们不想让对方找钱，付款的时候我们会尽量选择面值大的纸币给对方，这样才会使得我们给对方的纸币张数最少，对方点钱的时候也最方便。

[12. 整数转罗马数字](https://leetcode-cn.com/problems/integer-to-roman/)

- 思路

  - 每一步都使用当前较大的罗马数字作为加法因子，最后得到罗马数字表示就是长度最少的。

- 代码

  ```java
  public String intToRoman(int num) {
      // 把阿拉伯数字与罗马数字可能出现的所有情况和对应关系，放在两个数组中
      // 并且按照阿拉伯数字的大小降序排列，这是贪心选择思想
      int[] nums = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
      String[] romans = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
     	StringBuilder stringBuilder = new StringBuilder();
      int index = 0;
      while (index < 13) {
          // 特别注意：这里是等号
          while (num >= nums[index]) {
              // 注意：这里是等于号，表示尽量使用大的"面值"
              stringBuilder.append(romans[index]);
              num -= nums[index];
          }
          index++;
      }
      return stringBuilder.toString();
  }
  ```
  

### 12. Integer to Roman

- Arr1: 数字
- Arr2: string，和arr1相对应
- greedy：先匹配最大的，再匹配小的

### 45. Jump Game II

我们每次在可跳范围内选择可以使得跳的更远的位置。

我们用 end 表示当前能跳的边界，对于上边第一个图的橙色 1，第二个图中就是橙色的 4，遍历数组的时候，到了边界，我们就重新更新新的边界。

```java
public int jump(int[] nums) {
    int end = 0;
    int maxPosition = 0; 
    int steps = 0;
    for(int i = 0; i < nums.length - 1; i++){
        //找能跳的最远的
        maxPosition = Math.max(maxPosition, nums[i] + i); 
        if( i == end){ //遇到边界，就更新边界，并且步数加一
            end = maxPosition;
            steps++;
        }
    }
    return steps;
}
```



### 57. Insert Interval

遍历Intervals，和当前interval进行merge

- M1

  - 给个容器List放区间

  - 先把起点比自己小的都放进去
  - 放自己，合并当前区间

  - 后面的继续放进来，和当前区间判断是否需要合并

- M2
  - Newinterval: ns, ne
  - if ns > i.e
    - Add(interval)
  - if ne < i.s
    - add({ns, ne})
    - add(remaining intervals)
    - return
  - else
    - merge new interval and current interval
  - Last: add {ns, ne}



### 134. Gas Station

https://leetcode-cn.com/problems/gas-station/solution/jia-you-zhan-by-leetcode/

