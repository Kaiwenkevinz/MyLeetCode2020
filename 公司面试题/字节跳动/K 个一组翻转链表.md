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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(-1);  // 哨兵节点
        dummy.next = head; // 连接哨兵节点和链表头
        ListNode pre = dummy; // 将要反转的链表的头的上一个节点
        while (true) {
            ListNode start = pre.next; // 将要反转的链表的头
            ListNode end = pre; //将要反转的链表的尾节点，先设置成pre，后面会更新end的位置
            int i = 0;
            while (i < k && end.next != null) { // 确认end的位置，也就是将要反转的链表的尾节点
                end = end.next;
                i++;
            }
            if (i < k) {  // 说明剩余链表数量小于k，不用反转了
                break;
            }
            // 即将反转链表，在反转之前，保留现在的链表头和链表尾，方便反转完链表后重新把整个链表接起来
            ListNode willBeTail = start;
            ListNode willBeHead = end;
            ListNode endNext = end.next;
            
            end.next = null;  // 断开链表
            reverse(start);  // 反转
            pre.next = willBeHead;  // 把新的表头接上
            willBeTail.next = endNext;  // 把剩余的链表接上
            pre = willBeTail;  // 更新pre，准备下一轮反转
        }
        return dummy.next;
    }

    public void reverse(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode nextCur = cur.next;
            cur.next = pre;
            pre = cur;
            cur = nextCur;
        }
    }
}
```
