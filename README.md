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




2.两两交换链表中的节点
---
https://leetcode-solution.cn/solutionDetail?type=3&id=8&max_id=2

### 思路

1. 结果返回第二个节点
2. 移动Prehead 到下一组

### 代码

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode preHead = new ListNode(-1, head),res;
        preHead.next = head;
        res = head.next;
        ListNode firstNode = head, secondNode, nextNode;
        while(firstNode != null && firstNode.next != null){
            secondNode = firstNode.next;
            nextNode = secondNode.next;
            firstNode.next = nextNode;
            secondNode.next = firstNode;
            preHead.next = secondNode;
            preHead = firstNode;
            firstNode = nextNode;
        }
        return res;
        
    }
}
```

**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


3.翻转链表（二）
---
https://www.lintcode.com/problem/36/

### 思路



### 代码

```java
    public ListNode reverseBetween(ListNode head, int m, int n) {
        // write your code here
        ListNode dummy = new ListNode(0);
        ListNode prev = dummy;
        dummy.next = head;
        for(int i = 0; i < m - 1; i++){
            prev = prev.next;
        }
        ListNode start = prev.next, then = start.next;

        for(int j = 0; j < n - m; j++){
            start.next = then.next;
            then.next = prev.next; //这里不是等于start
            prev.next = then;
            then = start.next;
            // prev = start;
        }
        return dummy.next;

    }

```

**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


4.翻转链表
---
https://leetcode.com/problems/reverse-linked-list/

### 思路



### 代码

```java
class Solution {
   public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        while(head != null){
            ListNode nextNode = head.next;
            head.next = prev;
            prev = head;
            head = nextNode;
        }
        return prev;
    }
}
```

**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


5.86. Partition List
---
https://leetcode.com/problems/partition-list/

### 思路



### 代码

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode smallHead = new ListNode(0);
        ListNode bigHead = new ListNode(0);
        ListNode small = smallHead, big = bigHead;
        // smallHead.next = head;
        // bigHead.next = head;
        while(head != null){
            if(head.val < x){
                smallHead.next = head;
                smallHead = head;  
            }else {
                bigHead.next = head;
                bigHead = head;
            }
            head = head.next;
        }
        smallHead.next = big.next;
        bigHead.next = null;
        return small.next;
    }
}
```

**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


### 6. 109. 有序链表转换二叉搜索树


### 思路
---

1. 先找中点
2. 在遍历左右

### 代码

```java
public class Solution {
public TreeNode sortedListToBST(ListNode head) {
    if(head==null) return null;
    return toBST(head,null);
}
public TreeNode toBST(ListNode head, ListNode tail){
    ListNode slow = head;
    ListNode fast = head;
    if(head==tail) return null;
    
    while(fast!=tail&&fast.next!=tail){
        fast = fast.next.next;
        slow = slow.next;
    }
    TreeNode thead = new TreeNode(slow.val);
    thead.left = toBST(head,slow); // 尾部节点 是null 这里难想
    thead.right = toBST(slow.next,tail);
    return thead;
}

```

**复杂度分析**

- 时间复杂度：O(nlogn)
- 空间复杂度：O(nlogn)

