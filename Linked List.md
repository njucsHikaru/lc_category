# Linked List

## 题型判断



## 解题模板

- ListNode dummy = new ListNode(0);

## 例题分析

### 2. Add Two Numbers

- 解题思路
  - 遍历两个数组
  - 加法：当前位 + 进位
  - 遍历结束，考虑最后的进位
- 复杂度
  - O(m + n)
- 代码规范
  - 命名：carry, sum



### [14. 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

- 解题思路

  当字符串数组长度为 0 时则公共前缀为空，直接返回
  令最长公共前缀 ans 的值为第一个字符串，进行初始化
  遍历后面的字符串，依次将其与 ans 进行比较，两两找出公共前缀，最终结果即为最长公共前缀
  如果查找过程中出现了 ans 为空的情况，则公共前缀不存在直接返回

- 时间复杂度

  - O(s)，s 为所有字符串的长度之和

- 代码

```java
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) 
            return "";
        String ans = strs[0];
        for(int i = 1; i < strs.length; i++) {
            int j = 0;
            for(; j < ans.length() && j < strs[i].length(); j++) {
                if(ans.charAt(j) != strs[i].charAt(j))
                    break;
            }
            ans = ans.substring(0, j);
            if(ans.equals(""))
                return ans;
        }
        return ans;
    }
```



### [19. 删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

- 思路
  - 遍历第一遍，找出一共有多少个节点 (sum)
  - 找到第 sum - N  个节点, 删除它的下一个节点
- 代码

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    int length  = 0;
    ListNode first = head;
    while (first != null) {
        length++;
        first = first.next;
    }
    length -= n;
    first = dummy;
    while (length > 0) {
        length--;
        first = first.next;
    }
    first.next = first.next.next;
    return dummy.next;
}
```



### [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

- 递归 recursion

  两个链表头部值较小的一个节点与剩下元素的 `merge` 操作结果合并

  ```java
  	public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
          if (l1 == null) {
              return l2;
          }
          else if (l2 == null) {
              return l1;
          }
          else if (l1.val < l2.val) {
              l1.next = mergeTwoLists(l1.next, l2);
              return l1;
          }
          else {
              l2.next = mergeTwoLists(l1, l2.next);
              return l2;
          }
  
      }
  ```

  复杂度：

  - Time: O*(*n*+*m)

  - Space: O*(*n*+*m)

    栈空间的大小取决于递归调用的深度。

    结束递归调用时 `mergeTwoLists` 函数最多调用 n+m*n*+*m* 次，因此空间复杂度为 O*(*n*+*m)。

- 迭代 iteration

  ```java
  	public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
          ListNode dummy = new ListNode(0);
          ListNode prev = dummy;
          while (l1 != null && l2 != null) {
              if (l1.val <= l2.val) {
                  prev.next = l1;
                  l1 = l1.next;
              } else {
                  prev.next = l2;
                  l2 = l2.next;
              }
              prev = prev.next;
          }
          // 合并后 l1 和 l2 最多只有一个还未被合并完，我们直接将链表末尾指向未合并完的链表即可
          prev.next = l1 == null ? l2 : l1;
          return dummy.next;
      }
  ```

  复杂度：

  - Time: O*(*n*+*m)
  - Space: O*(*1)

### [23. 合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

- 优先队列

  把每个list的第一个元素放进去，使用最小堆找出最小的元素，然后把指针指向这个元素所属的list的下一个值。

  ```java
  		public ListNode mergeKLists(ListNode[] lists) {
          if (lists == null || lists.length == 0) return null;
          PriorityQueue<ListNode> queue = new PriorityQueue<>(lists.length, new Comparator<ListNode>() {
              @Override
              public int compare(ListNode o1, ListNode o2) {
                  if (o1.val < o2.val) return -1;
                  else if (o1.val == o2.val) return 0;
                  else return 1;
              }
          });
          ListNode dummy = new ListNode(0);
          ListNode p = dummy;
          for (ListNode node : lists) {
              if (node != null) queue.add(node);
          }
          while (!queue.isEmpty()) {
              p.next = queue.poll();
              p = p.next;
              if (p.next != null) queue.add(p.next);
          }
          return dummy.next;
      }
  ```

  

- 分治 - 链表两两合并

```java
		public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        return merge(lists, 0, lists.length - 1);
    }

    private ListNode merge(ListNode[] lists, int left, int right) {
        if (left == right) return lists[left];
        int mid = left + (right - left) / 2;
        ListNode l1 = merge(lists, left, mid);
        ListNode l2 = merge(lists, mid + 1, right);
        return mergeTwoLists(l1, l2);
    }

    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }
    }
```



### [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

- 递归

  ```java
      public ListNode swapPairs(ListNode head) {
          if(head == null || head.next == null){
              return head;
          }
          ListNode next = head.next;
          head.next = swapPairs(next.next);
          next.next = head;
          return next;
      }
  ```

  

- 迭代

```java
	public ListNode swapPairs(ListNode head) {
        ListNode pre = new ListNode(0);
        pre.next = head;
        ListNode temp = pre;
        while(temp.next != null && temp.next.next != null) {
            ListNode start = temp.next;
            ListNode end = temp.next.next;
            temp.next = end;
            start.next = end.next;
            end.next = start;
            temp = start;
        }
        return pre.next;
    }
```



### [25. K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

- 思路

  链表分区为已翻转部分+待翻转部分+未翻转部分
  每次翻转前，要确定翻转链表的范围，这个必须通过 k 此循环来确定
  需记录翻转链表前驱和后继，方便翻转完成后把已翻转部分和未翻转部分连接起来
  初始需要两个变量 pre 和 end，pre 代表待翻转链表的前驱，end 代表待翻转链表的末尾
  经过k此循环，end 到达末尾，记录待翻转链表的后继 next = end.next
  翻转链表，然后将三部分链表连接起来，然后重置 pre 和 end 指针，然后进入下一次循环
  特殊情况，当翻转部分长度不足 k 时，在定位 end 完成后，end==null，已经到达末尾，说明题目已完成，直接返回即可

- 代码

```java
public ListNode reverseKGroup(ListNode head, int k) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;

    ListNode pre = dummy;
    ListNode end = dummy;

    while (end.next != null) {
        for (int i = 0; i < k && end != null; i++) end = end.next;
        if (end == null) break;
        ListNode start = pre.next;
        ListNode next = end.next;
        end.next = null;
        pre.next = reverse(start);
        start.next = next;
        pre = start;
        end = pre;
    }
    return dummy.next;
}

private ListNode reverse(ListNode head) {
    ListNode pre = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = pre;
        pre = curr;
        curr = next;
    }
    return pre;
}
```

