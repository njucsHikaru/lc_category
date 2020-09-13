# Backtracking

## 题型判断

搜索问题主要使用回溯法。

回溯是一种通过穷举所有可能情况来找到所有解的算法。如果一个候选解最后被发现并不是可行解，回溯算法会舍弃它，并在前面的一些步骤做出一些修改，并重新尝试找到可行解。

https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/

“回溯”指的是“状态重置”，可以理解为“回到过去”、“恢复现场”，是在编码的过程中，是为了节约空间而使用的一种技巧。而回溯其实是“深度优先遍历”特有的一种现象。之所以是“深度优先遍历”，是因为我们要解决的问题通常是在一棵树上完成的，在这棵树上搜索需要的答案，一般使用深度优先遍历。



面试中主要有三种类型的排列问题：

https://leetcode-cn.com/problems/permutation-sequence/solution/pai-lie-zu-he-zhi-di-kge-pai-lie-golden-monkey-by-/

- 全排列
  - 如果排列的顺序不重要，可以使用“交换”的思想回溯写出全排列。生成 N!N! 个全排列需要时间 \mathcal{O}(N \times N!)O(N×N!)。该算法可以解决第一类问题。
- [下一个排列](https://leetcode-cn.com/articles/next-permutation/)
  - D.E. Knuth 算法按照字典顺序生成全排列，在O(*N*) 时间内完成。该算法可以解决第二类问题
- 60 第 k 个排列
  - 排列组合，算在哪个区间
    - dfs - recursion
    - iteration



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

  

### 39. Combination Sum

### 40. Combination Sum II

- 排序

- 去重

- 剪枝: 从第二个相同的值开始，可以等同于第一个值。可以看画的tree，branch一样的

  ```java
  if (i > begin && candidates[i] == candidates[i - 1]) {
  		continue;
  }
  ```

  

### 37. Sudoku Solver

- 约束编程

  基本的意思是在放置每个数字时都设置约束。在数独上放置一个数字后立即排除当前 行，列和子方块对该数字的使用。这会传播 约束条件 并有利于减少需要考虑组合的个数。

- 回溯

  但是该组合不是最优的并且不能继续放置数字了。该怎么办？ *回溯*。
  意思是回退，来改变之前放置的数字并且继续尝试。如果还是不行，再次 *回溯*。



### 46. Permutations

- 使用boolean[] used = new boolean[len]记录是否有使用过



###47. Permutations II

- 剪枝：

  ```java
  if(i>0 && nums[i] == nums[i - 1] && !used[i-1])
  	continue;
  ```



### 51. N-Queens

![image-20200714000137607](/Users/vicki/Library/Application Support/typora-user-images/image-20200714000137607.png)



### 52. N-Queens II

回溯，从第一行里面开始尝试放值，依次放到第n行为止结束。

存储：每行，每列数组存下来

判断valid：{遍历每行} 判断对应的列，及计算出的斜线上是否出现冲突的地方



### 60. Permutation Sequence



### 77. Combinations

### 78. Subsets

### 90. Subsets II

```java
class Solution {
    ArrayList<List<Integer>> res=new ArrayList<>();
    ArrayList<Integer> one_path=new ArrayList<>();//一个可能的子集
    int n;
    int [] nums;
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        this.nums=nums;
        n=nums.length;
        //先排序，这样相同的两个元素必相邻
        Arrays.sort(nums);
        backtarck(0);
        res.add(new ArrayList<Integer>());//补上一个空集
        return res;
    }
    private void backtarck(int i){//将要填入下标为i的元素，也就是说该层从nums[i]处的元素开始for循环
        if(i==n){
            return;
        }
        //再dfs地加子节点
        for(int j=i;j<n;j++){//做的是子集，子集是组合，所以是从当前元素开始遍历
               if(j>i&&nums[j]==nums[j-1]) continue;//同层重复，跳过
               one_path.add(nums[j]);
               res.add(new ArrayList<Integer>(one_path));
               backtarck(j+1);
               one_path.remove(one_path.size()-1);//撤销选择

        }
    }
}
```



### 79

### 89

### 93

### 131. Palindrome Partitioning

<img src="/Users/vicki/Library/Application Support/typora-user-images/image-20200817211204908.png" alt="image-20200817211204908" style="zoom:50%;" />

产生前缀字符串的时候，判断前缀字符串是否是回文。

- 如果前缀字符串是回文，则可以产生分支和结点；
- 如果前缀字符串不是回文，则不产生分支和结点，这一步是剪枝操作