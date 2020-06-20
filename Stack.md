# Stack

## 题型分析

- 什么时候使用栈？

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

  

