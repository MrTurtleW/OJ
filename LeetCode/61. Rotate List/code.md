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
        ListNode current = head;
        if (head == null)
            return null;

        if (k == 0)
            return head;
        int count = 1;
        while (current.next != null) {
            current = current.next;
            count++;
        }
        current.next = head;
        k %= count;
        k = count - k;

        for (int i = 0; i < k; i++) {
            current = current.next;
        }
        head = current.next;
        current.next = null;
        return head;
    }
}
```

