# 题目


# coding
- 正确coding
```java
      public ListNode oddEvenList(ListNode head) {
        // 解法一：双指针
        return oddEvenList01(head);
    }

    private static ListNode oddEvenList01(ListNode head){
        // 边界值判断
        if(head==null||head.next==null||head.next.next==null){
            return head;
        }
        // 定义奇数和偶数的头指针
        ListNode oddHead=head;
        ListNode evenHead=head.next;
        // 定义活动指针
        ListNode odd=head;
        ListNode even=head.next;
        // 开始迭代
        while(odd!=null&&odd.next!=null&&even!=null&&even.next!=null){
            // even=odd.next;
            odd.next=even.next;
            odd=odd.next;
            even.next=odd.next;
            even=even.next;
        }
        odd.next=evenHead;
        return oddHead;
    }
```


- 理解错误的coding（我理解成了奇数偶数前后的方式，题目是下标，但是我觉得这个coding也是有参考价值的）
```java
// 理解错误，这是奇数偶数，题目判断的是，位置的奇偶（更简单）
    public ListNode oddEvenList(ListNode head) {
        // 定义虚拟头节点
        ListNode oddDummy = new ListNode(-1);
        ListNode evenDummy = new ListNode(-1);
        // 定义动态指针
        ListNode oddCur = oddDummy;
        ListNode evenCur = evenDummy;
        ListNode cur = head;
        // 判断头节点的奇偶
        int headVal = cur.val;
        while(cur != null){
            if(cur.val % 2 == 0){
                evenCur.next = cur;
                evenCur = evenCur.next;
            }else{
                oddCur.next = cur;
                oddCur = oddCur.next;
            }
            cur = cur.next;
        }
        if(headVal % 2 == 0){
            evenCur.next = oddDummy.next;
            oddCur.next = null;
        }else{
            oddCur.next = evenDummy.next;
            evenCur.next = null;
        }
        return head;
    }   
```


# 总结
1. 这题总体来说和[leetCode86.分隔链表](leetCode86.%20分隔链表.md)这题的解法一样，使用虚拟节点的方式进行
2. 在链表中要善于使用虚拟头节点