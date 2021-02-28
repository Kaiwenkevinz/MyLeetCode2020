### 优先队列最小堆 O(nlogk) 66.55%
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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0 || (lists.length == 1 && lists[0] == null)) {
            return null;
        }

        Queue<ListNode> pq = new PriorityQueue<>((a, b) -> {  // 最小堆，a - b
            return a.val - b.val;
        });
        ListNode head = new ListNode(-1);
        ListNode cur = head;
        for (ListNode node : lists) {
            if (node != null) {
                pq.offer(node);
            }
        }
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            cur.next = new ListNode(node.val);
            cur = cur.next;
            if (node.next != null) {
                pq.offer(node.next);
            }
        }
        
        return head.next;
    }
}
```


### 链表两两合并 O(nk) 14.89%
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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0 || (lists.length == 1 && lists[0] == null)) {
            return null;
        }

        ListNode head = new ListNode(Integer.MIN_VALUE);
        for (int i = 0; i < lists.length; i++) {
            head = mergeTwoLists(head, lists[i]);
        }
        return head.next;
    }

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(-1);
        ListNode cur = head;
        while (l1 != null && l2 != null) {
            ListNode node = null;
            if (l1.val < l2.val) {
                node = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                node = new ListNode(l2.val);
                l2 = l2.next;
            }
            cur.next = node;
            cur = cur.next;
        }
        while (l1 != null) {
            ListNode node = new ListNode(l1.val);
            cur.next = node;
            cur = cur.next;
            l1 = l1.next;
        }
        while (l2 != null) {
            ListNode node = new ListNode(l2.val);
            cur.next = node;
            cur = cur.next;
            l2 = l2.next;
        }
        return head.next;
    }
}
```
