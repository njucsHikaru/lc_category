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
  

