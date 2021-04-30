很慢：

```c++
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode head;
        ListNode* current = &head;

        if (lists.size() == 0)
            return head.next;

        else if (lists.size() == 1) {
            return lists[0];
        }

        while (true) {
            ListNode* node = get_next_node(lists);
            if (node == nullptr)
                break;

            current->next = node;
            current = node;
        }

        return head.next;
    }

    ListNode* get_next_node(vector<ListNode*> &lists) {
        int index = 0;
        for (int i=1; i < lists.size();i++) {
            if (lists[i] == nullptr)
                continue;
            if (lists[index] == nullptr || lists[index]->val > lists[i]->val)
                index = i;
        }

        if (lists[index] == nullptr)
            return nullptr;

        ListNode* pre = lists[index];
        lists[index] = lists[index]->next;

        return pre;
    }
};
```

# 优先队列

```c++
#include<iostream>
#include<vector>
#include<queue>

using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* next) : val(x), next(next) {}
};

struct cmp {
    bool operator()(ListNode*a, ListNode *b) const {
        return a->val > b->val;
    }
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, cmp> q;

        ListNode dummy;
        ListNode* current = &dummy;

        for (ListNode* node : lists) {
            while (node != nullptr) {
                q.push(new ListNode(node->val));
                node = node->next;
            }
        }

        while (!q.empty()) {
            current->next = q.top();
            current = current->next;
            q.pop();
        }

        return dummy.next;
    }
};


int main() {
    ListNode l1(-1);
    l1.next = new ListNode(-1);
    l1.next->next = new ListNode(-1);

    ListNode l2(-2);
    l2.next = new ListNode(-2);
    l2.next->next = new ListNode(-1);

    ListNode l3(2);
    l3.next = new ListNode(6);

    ListNode* p = nullptr;

    vector<ListNode*> vec = { &l1, &l2 };

    Solution solution;
    ListNode* res = solution.mergeKLists(vec);

    while (res != nullptr) {
        cout << res->val;
        res = res->next;
    }
}
```

# 归并

```c++
#include<iostream>
#include<vector>

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        return partition(lists, 0, lists.size()-1);
    }

    ListNode* partition(vector<ListNode*>& lists, int s, int e) {
        if (s == e)
            return lists[s];

        else if (s < e) {
            int q = (s + e) / 2;
            ListNode* l1 = partition(lists, s, q);
            ListNode* l2 = partition(lists, q + 1, e);
            return merge(l1, l2);
        }
        else {
            return nullptr;
        }
    }

    ListNode* merge(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr)
            return l2;
        else if (l2 == nullptr)
            return l1;
        else if (l1->val < l2->val) {
            l1->next = merge(l1->next, l2);
            return l1;
        }
        else {
            l2->next = merge(l1, l2->next);
            return l2;
        }
    }
};


int main() {
    ListNode l1(-1);
    l1.next = new ListNode(-1);
    l1.next->next = new ListNode(-1);

    ListNode l2(-2);
    l2.next = new ListNode(-2);
    l2.next->next = new ListNode(-1);

    ListNode l3(2);
    l3.next = new ListNode(6);

    ListNode* p = nullptr;

    vector<ListNode*> vec = { &l1, &l2 };

    Solution solution;
    ListNode* res = solution.mergeKLists(vec);

    while (res != nullptr) {
        cout << res->val;
        res = res->next;
    }
}
```

