```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class Solution {
    public ListNode swapPairs(ListNode head){
        ListNode newHead = head, current = head, prev = null;
        while (current != null && current.next != null) {
            if(prev == null){
                newHead = current.next;
                prev = current;
                current.next = newHead.next;
                newHead.next = current;
            }
            else {
                prev.next = current.next;
                current.next = current.next.next;
                prev.next.next = current;
                prev = current;
            }
            current = current.next;
        }
        return newHead;
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
        int[] data = {1, 2, 3, 4};

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
        solution.print(solution.swapPairs(head));
    }
}
```