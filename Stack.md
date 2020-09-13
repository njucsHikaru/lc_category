# Stack

## 题型分析

- 什么时候使用栈？ 回到上一个
- 单调栈： 一个栈，里面的元素的大小按照他们所在栈内的位置，满足一定的单调性。
  - 

## 解题模板



## 例题分析

### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

- 思路

  - 只有一种括号的时候：【计数方法】 遇到右括号时，必须有左括号。所以可以使用var来对左括号计数，遇到右括号时减一

  - 有多种括号：

    初始化栈 S。
    一次处理表达式的每个括号。
    如果遇到开括号，我们只需将其推到栈上即可。这意味着我们将稍后处理它，让我们简单地转到前面的 子表达式。
    如果我们遇到一个闭括号，那么我们检查栈顶的元素。如果栈顶的元素是一个 相同类型的 左括号，那么我们将它从栈中弹出并继续处理。否则，这意味着表达式无效。
    如果到最后我们剩下的栈中仍然有元素，那么这意味着表达式无效。

- 代码

  ```java
  class Solution {
    private HashMap<Character, Character> mappings;
    public Solution() {
      this.mappings = new HashMap<Character, Character>();
      this.mappings.put(')', '(');
      this.mappings.put('}', '{');
      this.mappings.put(']', '[');
    }
    public boolean isValid(String s) {
      Stack<Character> stack = new Stack<Character>();
      for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (this.mappings.containsKey(c)) {
          if (stack.isEmpty() || stack.pop() != this.mappings.get(c)) {
            return false;
          }
        } else {
          stack.push(c);
        }
      }
      return stack.isEmpty();
    }
  }
  ```

  

### 42. Trapping Rain Water



### 71. Simplify Path



## 单调栈

一个栈，里面的元素的大小按照他们所在栈内的位置，满足一定的单调性。

### google interview 题

给一个数组，返回一个大小相同的数组。

返回的数组的第i个位置的值应当是，对于原数组中的第i个元素，至少往右走多少步，才能遇到一个比自己大的元素；若已经是最后一个元素，则在返回数组的对应位置放上-1.

```
Input: 5, 3, 1, 2, 4
Return: -1, 3, 1, 1, -1
```

找到上一个比自己大的元素。

- 把比当前小的peek()都pop & update the corresponding value in the specific position.

0, 1, 2, 3 -- 5, 3, 1, 2 -- pop 1 {-1, -1, 1, -1, -1}

0, 1, 3, 4 -- 5, 3, 2, 4 -- pop 2; pop 3 {-1, 3, 1, 1, -1}

5, -- return {-1, 3, 1, 1, -1}



### 84. Largest Rectangle in Histogram

**反证法：最后的结果中的最大矩形的上边框，一定和某一个bar的顶重合，否则我们一定可以通过提高上边框来增加这个矩形的面积。**

我们计算的矩形左右边框都已经到达了极限。 -- 计算每个矩形的高度达到极限的面积，进行比较。

-- 找到左边第一个比当前值小的x1 & 找到右边第一个比当前值小的x2	-- x1+1; x2-1

(x2-1 - (x1 + 1)) = x1 + x2 - 2

2，1，5，6，2，3

1，2，3，4，5，6

单调递增栈 -- 找到上一个比自己小的元素

2 

2，1 -- 1 -- 0【2：0】【1：0 - 2】

1，5 -- 1【3：2】

1，5，6 -- 5【4：3】

1，5，6，2 -- 1，2 -- 1【5：2】【4：3 - 5】【3：2 - 5】

1，2，3 -- 2【6：5】



1: 0~2：1 *

2: 0~7：6 *

3: 2~5：2 * 

4: 3~5：1 *

5: 2~7：4 *

6: 5~7：1 *





