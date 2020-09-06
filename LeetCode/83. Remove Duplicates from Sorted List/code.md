```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if head is None:
            return None

        new_head = head
        current = new_head

        head = head.next

        while head:
            if current.val != head.val:
                current.next = head
                current = current.next

            head = head.next
            
        current.next = None

        return new_head
```

