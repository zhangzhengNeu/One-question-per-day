# One-question-per-day



1.旋转链表
---

### 思路
1. 计算链表长度
2. 先成环，再拆环
3. 关于指针问题

### 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        ListNode iter = head;
        int len = 1;
        
        while(iter.next != null){
            iter = iter.next;
            len++;
        }
       
        int add = len - k % len;
        iter.next = head;
        
        if (add == len) {
            return head;
        }

        while(add-- > 0){
            iter = iter.next;
        }
        ListNode resHead = iter.next;
        iter.next = null;
        return resHead;

    }
    private int getLength(ListNode head){
        int n = 1;
        
        while(head.next != null){
            head = head.next;
            n++;
        }
        return n;
    }
}
```

**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


