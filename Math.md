# Math & String



### [7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

- 思路

  - 通过模运算倒序

- **考虑溢出的情况**

  ~~~java
  if (rst > Integer.MAX_VALUE / 10 || (rst == Integer.MAX_VALUE / 10 && remains > 7)) 
  		return 0;
  if (rst < Integer.MIN_VALUE / 10 || (rst == Integer.MIN_VALUE / 10 && remains < -8)) 
  		return 0;
  ~~~



### [13. 罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/)

- 思路
  - 用一个map存下所有的1个和2个的可能性 / 函数判断
    - 比较两个字符是否在map里，不在的话就看第一个字符
    - 特殊字符有：IV, IX, XL, XC, CD, CM; 其他的当前字符都要大于等于下一个，所以可以基于此进行判断
- 代码

```java
		public int romanToInt(String s) {
        int sum = 0;
        int preNum = getValue(s.charAt(0));
        for(int i = 1;i < s.length(); i ++) {
            int num = getValue(s.charAt(i));
            if(preNum < num) {
                sum -= preNum;
            } else {
                sum += preNum;
            }
            preNum = num;
        }
        sum += preNum;
        return sum;
    }
    
    private int getValue(char ch) {
        switch(ch) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
            default: return 0;
        }
    }
```









