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
```

**复杂度分析**

- 时间复杂度：O(n)，其中 n 是链表的长度。我们只需要遍历该链表三次。读者们也可以自行尝试在计算拷贝节点的随机指针的同时计算其后继指针，这样只需要遍历两次。
- 空间复杂度：O(1)，O(1)。注意返回值不计入空间复杂度。
- 

### 7. 102 · 带环链表（lint)


### 思路
---
自己可能不按答案那样写

### 代码

```java
public class Solution {
    public Boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }

        ListNode fast, slow;
        fast = head.next;
        slow = head;
        while (fast != slow) {
            if(fast==null || fast.next==null)
                return false;
            fast = fast.next.next;
            slow = slow.next;
        } 
        return true;
    }
}
```

**复杂度分析**

- 时间复杂度：O(n)，
- 空间复杂度：O(1)，
- 



### 7. 103 · 带环链表 II（lint)


### 思路
---
使用双指针判断链表中是否有环，慢指针每次走一步，快指针每次走两步，若链表中有环，则两指针必定相遇。
假设环的长度为l，环上入口距离链表头距离为a，两指针第一次相遇处距离环入口为b，则另一段环的长度为c=l-b，由于快指针走过的距离是慢指针的两倍，则有a+l+b=2*(a+b),又有l=b+c，可得a=c，故当判断有环时(slow==fast)时，移动头指针，同时移动慢指针，两指针相遇处即为环的入口。

### 代码

```java
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @return: The node where the cycle begins. if there is no cycle, return null
     */
    public ListNode detectCycle(ListNode head) {
        // write your code here
        ListNode fast = head, slow = head;    //lintCode的答案不太对
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow){
                while(head != slow){
                    head = head.next;
                    slow = slow.next;
                }               
            }
        }
        return slow;
    }
}
```

**复杂度分析**

- 时间复杂度：O(n)，其中 NN 为链表中节点的数目。在最初判断快慢指针是否相遇时，slow 指针走过的距离不会超过链表的总长度；随后寻找入环点时，走过的距离也不会超过链表的总长度。因此，总的执行时间为 O(N)+O(N)=O(N)。
- 空间复杂度：O(1)，

### 7. 103 · 带环链表 II（lint)


### 思路2
---
一个非常直观的思路是：我们遍历链表中的每个节点，并将它记录下来；一旦遇到了此前遍历过的节点，就可以判定链表中存在环。借助哈希表可以很方便地实现。

### 代码

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode pos = head;
        Set<ListNode> visited = new HashSet<ListNode>();
        while (pos != null) {
            if (visited.contains(pos)) {
                return pos;
            } else {
                visited.add(pos);
            }
            pos = pos.next;
        }
        return null;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/huan-xing-lian-biao-ii-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

**复杂度分析**

- 时间复杂度：O(n)，
- 空间复杂度：O(n)，

### 8. 160. Intersection of Two Linked Lists

### 思路1
---
判断两个链表是否相交，可以使用哈希集合存储链表节点。

首先遍历链表 \textit{headA}headA，并将链表 \textit{headA}headA 中的每个节点加入哈希集合中。然后遍历链表 \textit{headB}headB，对于遍历到的每个节点，判断该节点是否在哈希集合中：

如果当前节点不在哈希集合中，则继续遍历下一个节点；

如果当前节点在哈希集合中，则后面的节点都在哈希集合中，即从当前节点开始的所有节点都在两个链表的相交部分，因此在链表 \textit{headB}headB 中遍历到的第一个在哈希集合中的节点就是两个链表相交的节点，返回该节点。

如果链表 \textit{headB}headB 中的所有节点都不在哈希集合中，则两个链表不相交，返回 \text{null}null。


### 代码

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        Set<ListNode> visited = new HashSet<ListNode>();
        ListNode temp = headA;
        while (temp != null) {
            visited.add(temp);
            temp = temp.next;
        }
        temp = headB;
        while (temp != null) {
            if (visited.contains(temp)) {
                return temp;
            }
            temp = temp.next;
        }
        return null;
    }
}

```

**复杂度分析**

- 时间复杂度：O(n + m)，
- 空间复杂度：O(n)，

### 思路2
---

为什么 a, b 指针相遇的点一定是相交的起始节点? 我们证明一下：

将两条链表按相交的起始节点继续截断，链表 1 为: A + C，链表 2 为: B + C；

当 a 指针将链表 1 遍历完后，重定位到链表 2 的头节点，然后继续遍历直至相交点，此时 a 指针遍历的距离为 A + C + B；

同理 b 指针遍历的距离为 B + C + A；

### 代码

```java
public class Solution {
   public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
       while(headA != headB){
           if(headA != null){
               headA = headA.next;
           }else{
               headA =headB;
           }
           
           if(headB != null){
               headB = headB.next;
           }else{
               headB =headA;
           }
       }
        return headA;
    }
}

```

**复杂度分析**

- 时间复杂度：O(n + m)，
- 空间复杂度：O(1)，

9.146. LRU 缓存机制
https://leetcode-solution.cn/solutionDetail?type=3&id=12&max_id=2
---

### 思路
1. 哈希表表记录前节点。
2. 单向链表的节点，key，value两个值，就不用另一个hash表记录了
### 代码

```java
public class LRUCache {
    class ListNode{
    public int key, val; //22
    public ListNode next;
        public ListNode(int key, int val){
        this.key = key;
        this.val = val;
        this.next = null;
        }
    }
    /*
    * @param capacity: An integer
    */
    private Map<Integer, ListNode> keyToPrev ;///cc
    private ListNode dummy = new ListNode(0, 0);
    private ListNode tail = dummy;

    private int capacity, size;

    public LRUCache(int capacity) {
        // do intialization if necessary
        this.capacity = capacity; 
        this.keyToPrev = new HashMap<>();
    }
    /*
     * @param key: An integer
     * @return: An integer
     */
    
    public void moveToTail(int key){
        ListNode prev = keyToPrev.get(key);
        ListNode cur = prev.next;
        if(cur == tail){
            return;
        }
        prev.next = prev.next.next;//必须第一步；

        tail.next = cur; //tail 一开始？链表怎么相连的？
        cur.next = null;
        

        if (prev.next != null) { //zheli
            keyToPrev.put(prev.next.key, prev);
        }
        keyToPrev.put(cur.key, tail);
        tail = cur;
    }

    public int get(int key) {
        if (!keyToPrev.containsKey(key)) {
            return -1;
        }
        
        moveToTail(key);
        
        // the key has been moved to the end
        return tail.val;
    }

    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    public void set(int key, int value) {
        // get method will move the key to the end of the linked list
        if (get(key) != -1) {
            ListNode prev = keyToPrev.get(key);
            prev.next.val = value;
            return;
        }
        
        if (size < capacity) {
            size++;
            ListNode curt = new ListNode(key, value);
            tail.next = curt;
            keyToPrev.put(key, tail);
            
            tail = curt;
            return;
        }
        
        // replace the first node with new key, value
        ListNode first = dummy.next;
        keyToPrev.remove(first.key);
        
        first.key = key;
        first.val = value;
        keyToPrev.put(key, dummy);
        
        moveToTail(key);
    }
}
```

**复杂度分析**
- 时间复杂度：O(1)
- 空间复杂度：链表占用空间 O(N)O(N)，哈希表占用空间也是 O(N)O(N)，因此总的空间复杂度为 O(N)O(N)，其中 N 为容量大小，也就是题目中的 capacity。
```




