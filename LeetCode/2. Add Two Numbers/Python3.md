```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def not_equal(self, longer, c):
        result = []
        while True:
            tmp = longer.val + c
            if tmp >= 10:
                c = 1
                result.append(tmp-10)
            else:
                c = 0
                result.append(tmp)
            if longer.next is None:
                if c == 1:
                    result.append(1)
                return result
            else:
                longer = longer.next

    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        
        result = []
        c = 0
        while True:
            tmp = l1.val + l2.val + c
            if tmp >= 10:
                c = 1
                result.append(tmp-10)
            else:
                c=0
                result.append(tmp)

            if l1.next is None and l2.next is not None:
                result.extend(self.not_equal(l2.next, c))
                return result
            elif l1.next is not None and l2.next is None:
                result.extend(self.not_equal(l1.next, c))
                return result
            elif l1.next is None and l2.next is None:
                if c == 1:
                    result.append(1)
                return result
            else:
                l1 = l1.next
                l2 = l2.next
```


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        
        carry = 0
        root = n = ListNode(0)
        while l1 or l2 or carry:
            v1 = v2 = 0
            if l1:
                v1 = l1.val
                l1 = l1.next
            if l2:
                v2 = l2.val
                l2 = l2.next
            carry, val = divmod(v1+v2+carry, 10)
            n.next = ListNode(val)
            n = n.next
        return root.next
```