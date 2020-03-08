# 自己写的

```java
class Solution {

    public ListNode reverseKGroup(ListNode head, int k) {
        int n = 0;
        ListNode current = head;
        while (current != null) {
            current = current.next;
            n++;
        }

        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        current = head;
        ListNode prev = sentinel;
        while (n >= k) {
            // 头插法转置链表
            for (int i = 0; i < k-1; i++) {
                ListNode next = current.next;
                current.next = next.next;
                next.next = prev.next;
                prev.next = next;
            }
            prev = current;
            current = current.next;
            n -= k;
        }

        return sentinel.next;
    }
}
```