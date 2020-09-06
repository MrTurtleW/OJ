```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        last = sys.maxsize

        new_head = ListNode(0)
        current = new_head

        while head:
            if (not head.next and head.val != last) or (head.next and head.val != head.next.val and head.val != last):
                current.next = ListNode(head.val)
                current = current.next

            last = head.val
            head = head.next

        return new_head.next
```

