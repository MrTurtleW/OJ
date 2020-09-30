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
    public ListNode partition(ListNode head, int x) {
        if (head == null)
            return null;
        ListNode sentinel = new ListNode(0, head);
        ListNode current = sentinel;
        ListNode pre = null;

        while (head != null) {
            ListNode next = head.next;
            if (head.val < x) {
                if (pre != null) {
                    head.next = current.next;
                    current.next = head;
                    pre.next = next;
                }
                current = current.next;
            }
            else {
                pre = head;
            }
            head = next;
        }
        return sentinel.next;
    }
}
```

