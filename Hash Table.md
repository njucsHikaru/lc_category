# Hash Table

## 题型判断



## 解题模板

- 空间换时间
  - 查找，插入，删除: O(1)
- HashMap

## 例题分析

### Two Sum

- 解题思路
  - 已知一个array和target，找出一个pair的和为target
  - 遍历数组，在剩下的值中找有没有target - current
  - 可以直接在现有的hashmap中找： 
    - 不在：比如存在pair，那么在剩下的值里，遍历到第二个值时会找到当前这个值
    - 在：return
- 代码思路
  - 遍历一遍数组
  - 查询__<u>现有的hashmap</u>__中是否有符合条件的值
  - 将已有的数字存到hashmap中
- 复杂度
  - time: O(n)
  - Space: O(n)



### 36. Valid Sudoku

- 分别用rows[], columns[], boxs[] 三个hashmap数组来存
- 把number和位置放进去，看是否会重复，count > 1时就return false
  - rows[]: 每一行 ，rows[j] = (num, +1)
  - columns[]: 每一列，columns[i] = (num, +1)
  - boxes: 每一个九宫格，boxes[] = (num, +1)
    - 根据i, j 判断在哪个九宫格：i / 3代表纵向，j / 3代表横向。所以是i / 3 * 3 + j / 3

