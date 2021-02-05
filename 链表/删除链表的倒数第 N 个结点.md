### 快慢指针, O(n), 100%
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return head;
        }
        ListNode dummyNode = new ListNode(0, head);  // 哨兵节点，用来使删除头节点的特殊情况不用特殊处理
        ListNode pAhead = head;
        ListNode cur = head;
        ListNode prev = dummyNode;
        for (int i = 0; i < n; i++) {
            pAhead = pAhead.next;
        }
        while (pAhead != null) {
            pAhead = pAhead.next;
            prev = cur;
            cur = cur.next;
        }
        prev.next = cur.next;
        cur.next = null;
        return dummyNode.next;
    }
}
```
