# 自己写的

## 头插法

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode new_head = head;

        while (head.next != null) {
            ListNode next = head.next;
            head.next = next.next;
            next.next = new_head;
            new_head = next;
        }
        return new_head;
    }

    private void print(ListNode head) {
        while(head != null){
            System.out.print(head.val + " -> ");
            head = head.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = null;
        ListNode current = null;
        int[] data = {1, 2, 3, 4, 5};

        for(int num: data){
            ListNode node = new ListNode(num);
            if(head == null){
                head = node;
                current = node;
            }
            else{
                current.next = node;
                current = node;
            }
        }

        Solution solution = new Solution();
        solution.print(solution.reverseList(head));
    }
}
```