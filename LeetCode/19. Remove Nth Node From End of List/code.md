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
        if (head == null)
            return null;

        int i = 0;
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode current = head, prev = sentinel;

        while (current != null) {
            if (i >= n)
                prev = prev.next;
            current = current.next;

            i++;
        }
        if (prev.next != null)
            prev.next = prev.next.next;
        return sentinel.next;
    }
}
```