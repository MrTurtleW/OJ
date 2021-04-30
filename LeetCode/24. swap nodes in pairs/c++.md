```c++
#include<iostream>

using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* next) : val(x), next(next) {}
};

class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return head;

        ListNode sentinel;
        
        sentinel.next = head;


        ListNode* pre = &sentinel, * current = head;
        
        while (current != nullptr && current->next != nullptr) {
            pre->next = current->next;
            pre = pre->next;
            current->next = pre->next;
            pre->next = current;
            current = current->next;
            pre = pre->next;
        }

        return sentinel.next;
    }
};


int main() {
    ListNode root(1);

    ListNode* p = nullptr;

    Solution solution;
    ListNode* swapped = solution.swapPairs(&root);
    while (swapped != nullptr) {
        cout << swapped->val << " ";
        swapped = swapped->next;
    }
}
```

