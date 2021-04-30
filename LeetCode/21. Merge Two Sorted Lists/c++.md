```c++
class Solution{
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode sentinel;
        ListNode* current = &sentinel;

        while (l1 != nullptr && l2 != nullptr) {
            if (l1 == nullptr) {
                current->next = l2;
                current = current->next;
                l2 = l2->next;
            }
            else if (l2 == nullptr) {
                current->next = l1;
                current = current->next;
                l1 = l1->next;
            }
            else if (l1->val <= l2->val) {
                current->next = l1;
                current = current->next;
                l1 = l1->next;
            }
            else {
                current->next = l2;
                current = current->next;
                l2 = l2->next;
            }
        }

        if (l1 != nullptr)
            current->next = l1;
        else if (l2 != nullptr)
            current->next = l2;

        return sentinel.next;
    }
};
```

