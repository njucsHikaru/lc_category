# Backtracking

## 题型判断

回溯是一种通过穷举所有可能情况来找到所有解的算法。如果一个候选解最后被发现并不是可行解，回溯算法会舍弃它，并在前面的一些步骤做出一些修改，并重新尝试找到可行解。

## 解题模板

- curStr, List<String> res

```java
	public void backtrack(String combination, String next_digits) {
    // terminate condition
    if (XXX) {
      // the combination is done
      output.add(combination);
      return;
    }
    // iterate over the next available input
    for (int i = 0; i < XXX; i++) {
      // append the current letter to the combination
      // and proceed to the next digits
      backtrack(combination + letter, next_digits.substring(1));
    }
  }
```



## 例题分析

### [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

- 思路

  给出如下回溯函数 backtrack(combination, next_digits) ，它将一个目前已经产生的组合 combination 和接下来准备要输入的数字 next_digits 作为参数。

  如果没有更多的数字需要被输入，那意味着当前的组合已经产生好了。
  如果还有数字需要被输入：
  遍历下一个数字所对应的所有映射的字母。
  将当前的字母添加到组合最后，也就是 combination = combination + letter 。
  重复这个过程，输入剩下的数字： backtrack(combination + letter, next_digits[1:]) 。

- 代码

```java
class Solution {
  Map<String, String> phone = new HashMap<String, String>() {{
    put("2", "abc");
    put("3", "def");
    put("4", "ghi");
    put("5", "jkl");
    put("6", "mno");
    put("7", "pqrs");
    put("8", "tuv");
    put("9", "wxyz");
  }};

  List<String> output = new ArrayList<String>();

  public void backtrack(String combination, String next_digits) {
    // if there is no more digits to check
    if (next_digits.length() == 0) {
      // the combination is done
      output.add(combination);
    }
    // if there are still digits to check
    else {
      // iterate over all letters which map 
      // the next available digit
      String digit = next_digits.substring(0, 1);
      String letters = phone.get(digit);
      for (int i = 0; i < letters.length(); i++) {
        String letter = phone.get(digit).substring(i, i + 1);
        // append the current letter to the combination
        // and proceed to the next digits
        backtrack(combination + letter, next_digits.substring(1));
      }
    }
  }

  public List<String> letterCombinations(String digits) {
    if (digits.length() != 0)
      backtrack("", digits);
    return output;
  }
}
```



###[22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

- DFS

  当前左右括号都有大于 0 个可以使用的时候，才产生分支；

  产生左分支的时候，只看当前是否还有左括号可以使用；

  产生右分支的时候，还受到左分支的限制，右边剩余可以使用的括号数量一定得在严格大于左边剩余的数量的时候，才可以产生分支；

  在左边和右边剩余的括号数都等于 0 的时候结算。

  ```java
  	private void dfs(String curStr, int left, int right, List<String> res) {
          // 在递归终止的时候，直接把它添加到结果集即可，注意与「力扣」第 46 题、第 39 题区分
          if (left == 0 && right == 0) {
              res.add(curStr);
              return;
          }
          // 剪枝（如图，左括号可以使用的个数严格大于右括号可以使用的个数，才剪枝，注意这个细节）
          if (left > right) {
              return;
          }
          if (left > 0) {
              dfs(curStr + "(", left - 1, right, res);
          }
          if (right > 0) {
              dfs(curStr + ")", left, right - 1, res);
          }
      }
  ```

  

