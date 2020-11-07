```java
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null)
            return null;
        ListNode sentinel = new ListNode();
        sentinel.next = head;
        ListNode prev = sentinel, start=sentinel, next;
        ListNode current = head;

        int index = 0;

        while (current != null) {
            next = current.next;

            if (index == m-1)
                start = prev;
            else if (index == n) {
                break;
            }

            else if (index >= m) {
                current.next = prev;
            }

            prev = current;
            current = next;
            index++;
        }

        start.next.next = current;
        start.next = prev;
        return sentinel.next;
    }

    ListNode buildList(int[] array) {
        ListNode head = new ListNode();

        ListNode current = head;
        for (int i : array) {
            current.next = new ListNode(i);
            current = current.next;
        }

        return head.next;
    }

    void print(ListNode head) {
        while (head != null) {
            System.out.println(head.val);
            head = head.next;
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        solution.print(solution.reverseBetween(solution.buildList(new int[]{1,2,3,4,5,6,7,8}), 2, 7));
    }
}
```

