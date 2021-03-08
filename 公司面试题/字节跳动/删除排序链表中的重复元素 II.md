哨兵节点，用于方便头节点的检查  
prev节点，用于保存第一个重复的节点的前一个节点  
cur节点，用于检查重复的节点  
diffNode，用于保存第一个不是重复的节点，便于将prev连接diffNode，以达到删除重复节点的效果
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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode temp = new ListNode(-1);  // 哨兵节点
        temp.next = head;
        ListNode cur = head;
        ListNode prev = temp;
        ListNode diffNode = cur;  // 第一个和cur不一样的节点

        while (cur != null) {
            int count = 0;
            while (diffNode != null && diffNode.val == cur.val) {  // 找到第一个和cur不一样的节点
                diffNode = diffNode.next;
                count++;
            }
            if (count > 1) { // count > 1 说明有重复的节点（重复的节点的个数至少是2个或以上，一个节点不存在重复）
                prev.next = diffNode;
            } else {
                prev = cur;
            }
            cur = diffNode;
        }
        return temp.next;
    }
}
```
