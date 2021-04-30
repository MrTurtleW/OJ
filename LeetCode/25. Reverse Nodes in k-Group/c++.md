```c++
#include<iostream>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (head == nullptr) {
            return head;
        }

        if (k == 1){
            return head;
        }

        ListNode sentinel;

        sentinel.next = head;

        int i = 0;
        ListNode *start = &sentinel;
        while (head != nullptr || i == k) {
            if (i < k) {
                i++;
                head = head->next;
            }
            else {
                start = reverseGroup(start, k);
                head = start->next;
                i = 0;
            }
        }
        return sentinel.next;
    }

    ListNode* reverseGroup(ListNode* head, int k) {
        ListNode *prev = head->next;
        ListNode *current = head->next->next;
        for (int i = 1; i < k ; i++) {
            prev->next = current->next;
            current->next = head->next;
            head->next = current;
            current = prev->next;
        }
        return prev;
    }
};


int main() {
    Solution solution;
    ListNode root(1);
    root.next = new ListNode(2);
    root.next->next = new ListNode(3);
    root.next->next->next = new ListNode(4);

    ListNode *result = solution.reverseKGroup(&root, 4);

    while (result != nullptr) {
        cout << result->val << endl;
        result = result->next;
    }
}
```

