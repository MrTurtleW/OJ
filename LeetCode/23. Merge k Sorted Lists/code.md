```java

 class ListNode {
     int val;
     ListNode next;
     ListNode() {}
     ListNode(int val) { this.val = val; }
     ListNode(int val, ListNode next) { this.val = val; this.next = next; }

     public String toString() {
         return "" + val;
     }
 }
 class Solution {
    private ListNode[] lists;
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode sentinel = new ListNode(0);
        ListNode current = sentinel, next = null;
        this.lists = lists;

        while ((next=getNext()) != null) {
            current.next = next;
            current = next;
        }

        return sentinel.next;

    }

    private ListNode getNext() {
        ListNode smallest = null;

        int index = 0;
        for (; index < lists.length; index++) {
            if (lists[index] != null ) {
                smallest = lists[index];
                break;
            }
        }

        if (smallest == null)
            return null;
        for (int i = 0; i < lists.length; i++) {
            if (lists[i] != null && smallest.val > lists[i].val) {
                smallest = lists[i];
                index = i;
            }
        }
        lists[index] = lists[index].next;
        return smallest;
    }

     public static void main(String[] args) {
         Solution solution = new Solution();
         ListNode l1 = new ListNode(1);
         l1.next = new ListNode(4);
         l1.next.next = new ListNode(5);

         ListNode l2 = new ListNode(1);
         l2.next = new ListNode(3);
         l2.next.next = new ListNode(4);

         ListNode l3 = new ListNode(2);
         l3.next = new ListNode(6);

         ListNode res = solution.mergeKLists(new ListNode[]{l1,l2,l3});

         while (res != null) {
             System.out.println(res.val);
             res = res.next;
         }
     }
}
```


下面这个快一点，引申出归并

```java
 class Solution {
    private ListNode[] lists;
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0)
            return null;
        ListNode dummy = lists[0];

        for (int i=1; i < lists.length; i++)
            dummy = mergeTwoSortedLists(dummy, lists[i]);

        return dummy;
    }

    private ListNode mergeTwoSortedLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        while (l1 != null || l2 != null) {
            if (l1 == null) {
                current.next = l2;
                l2 = l2.next;
            }

            else if (l2 == null) {
                current.next = l1;
                l1 = l1.next;
            }

            else if (l1.val < l2.val){
                current.next = l1;
                l1 = l1.next;
            }
            else {
                current.next = l2;
                l2 = l2.next;
            }

            current = current.next;
        }
        return dummy.next;
    }
}
```