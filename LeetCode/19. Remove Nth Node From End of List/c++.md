```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode sentinel;
        sentinel.next = head;
        ListNode* pre = &sentinel, * current = head;
        int i = 0;
        while (current != nullptr) {
            if (i >= n)
                pre = pre->next;
            current = current->next;
            i++;
        }

        if (pre->next != nullptr)
            pre->next = pre->next->next;

        return sentinel.next;
    }
};
```

