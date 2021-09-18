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


### 7. 138. Copy List with Random Pointer


### 思路
---

1. O(n)方法好想一点

### 代码

```java
public RandomListNode copyRandomList(RandomListNode head) {
  if (head == null) return null;
  
  Map<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
  
  // loop 1. copy all the nodes
  RandomListNode node = head;
  while (node != null) {
    map.put(node, new RandomListNode(node.label));
    node = node.next;
  }
  
  // loop 2. assign next and random pointers
  node = head;
  while (node != null) {
    map.get(node).next = map.get(node.next);
    map.get(node).random = map.get(node.random);
    node = node.next;
  }
  
  return map.get(head);
}

```

**复杂度分析**

- 时间复杂度：O(n)
- 空间复杂度：O(n)，其中 nn 是链表的长度。为哈希表的空间开销。


### 7. 138. Copy List with Random Pointer


### 思路
---
https://leetcode-cn.com/problems/copy-list-with-random-pointer/solution/fu-zhi-dai-sui-ji-zhi-zhen-de-lian-biao-rblsf/

1. dfs 方法不太理解
2. 本题要求我们对一个特殊的链表进行深拷贝。如果是普通链表，我们可以直接按照遍历的顺序创建链表节点。而本题中因为随机指针的存在，当我们拷贝节点时，「当前节点的随机指针指向的节点」可能还没创建，因此我们需要变换思路。一个可行方案是，我们利用回溯的方式，让每个节点的拷贝操作相互独立。对于当前节点，我们首先要进行拷贝，然后我们进行「当前节点的后继节点」和「当前节点的随机指针指向的节点」拷贝，拷贝完成后将创建的新节点的指针返回，即可完成当前节点的两指针的赋值。

具体地，我们用哈希表记录每一个节点对应新节点的创建情况。遍历该链表的过程中，我们检查「当前节点的后继节点」和「当前节点的随机指针指向的节点」的创建情况。如果这两个节点中的任何一个节点的新节点没有被创建，我们都立刻递归地进行创建。当我们拷贝完成，回溯到当前层时，我们即可完成当前节点的指针赋值。注意一个节点可能被多个其他节点指向，因此我们可能递归地多次尝试拷贝某个节点，为了防止重复拷贝，我们需要首先检查当前节点是否被拷贝过，如果已经拷贝过，我们可以直接从哈希表中取出拷贝后的节点的指针并返回即可。

在实际代码中，我们需要特别判断给定节点为空节点的情况。

### 代码

```java
class Solution {
    Map<Node, Node> cachedNode = new HashMap<Node, Node>();

    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }
        if (!cachedNode.containsKey(head)) {
            Node headNew = new Node(head.val);
            cachedNode.put(head, headNew);
            headNew.next = copyRandomList(head.next);
            headNew.random = copyRandomList(head.random);
        }
        return cachedNode.get(head);
    }
}

```

**复杂度分析**

- 时间复杂度：O(n)，其中 n 是链表的长度。对于每个节点，我们至多访问其「后继节点」和「随机指针指向的节点」各一次，均摊每个点至多被访问两次。
- 空间复杂度：O(n)，其中 n 是链表的长度。为哈希表的空间开销。

### 7. 138. Copy List with Random Pointer


### 思路
---
空间复杂度可以省去哈希表，为O1, 把复制的节点拼接在源节点后面，然后再拆分。

注意到方法一需要使用哈希表记录每一个节点对应新节点的创建情况，而我们可以使用一个小技巧来省去哈希表的空间。

当我们完成了拷贝节点的随机指针的赋值，我们只需要将这个链表按照原节点与拷贝节点的种类进行拆分即可，只需要遍历一次。同样需要注意最后一个拷贝节点的后继节点为空，我们需要特别判断这种情况。


### 代码

```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }
        for (Node node = head; node != null; node = node.next.next) {
            Node nodeNew = new Node(node.val);
            nodeNew.next = node.next;
            node.next = nodeNew;
        }
        for (Node node = head; node != null; node = node.next.next) {
            Node nodeNew = node.next;
            nodeNew.random = (node.random != null) ? node.random.next : null;
        }
        Node headNew = head.next;
        for (Node node = head; node != null; node = node.next) {
            Node nodeNew = node.next;
            node.next = node.next.next;
            nodeNew.next = (nodeNew.next != null) ? nodeNew.next.next : null;
        }
        return headNew;
    }
}


**复杂度分析**

- 时间复杂度：O(n)，其中 n 是链表的长度。我们只需要遍历该链表三次。读者们也可以自行尝试在计算拷贝节点的随机指针的同时计算其后继指针，这样只需要遍历两次。
- 空间复杂度：O(1)，O(1)。注意返回值不计入空间复杂度。
- 

