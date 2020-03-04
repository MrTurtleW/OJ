# C


```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
 
 #include<stdio.h> 
 #include<stdlib.h>
 
struct ListNode {
    int val;
    struct ListNode *next;
};



struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
	int carry = 0;
	struct ListNode *root, *n;
	root = malloc(sizeof(struct ListNode));
    n = root;
	while(l1 != NULL || l2 != NULL || carry != 0){
		int v1=0, v2 = 0;
		if (l1 != NULL){
			v1 = l1->val;
			l1 = l1->next;
		}
		if(l2 != NULL){
			v2= l2->val;
			l2 = l2->next;
		}
		int val = (v1 + v2 + carry) % 10;
		carry = (v1 + v2 + carry) / 10;
		printf("%d, %d\n", carry, val);
		n->next = malloc(sizeof(struct ListNode));
		n->next->val = val;
		// 一定要置空 
		n->next->next = NULL;
		n = n->next;
	}
	return root->next;
}
int main(){
	struct ListNode l1_3 = {3, NULL};
	struct ListNode l1_2 = {4, &l1_3};
	struct ListNode l1 = {2, &l1_2};
	
	
	struct ListNode l2_3 = {4, NULL};
	struct ListNode l2_2 = {6, &l2_3};
	struct ListNode l2 = {5, &l2_2};
	
	struct ListNode *result = addTwoNumbers(&l1, &l2);

	while(result != NULL){
		printf("%d, ", result->val);
		result = result -> next; 
	} 
}
```

# C++

```c++
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int sum=0;
        ListNode *l3=NULL;
        ListNode **node=&l3;
        while(l1!=NULL||l2!=NULL||sum>0)
        {
            if(l1!=NULL)
            {
                sum+=l1->val;
                l1=l1->next;
            }
            if(l2!=NULL)
            {
                sum+=l2->val;
                l2=l2->next;
            }
            (*node)=new ListNode(sum%10);
            sum/=10;
            node=&((*node)->next);
        }        
        return l3;
    }
};
```
# python

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