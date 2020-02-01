Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.

Note:

Given n will always be valid.


source:LeetCode https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

***

Do it directly, pay attention when the head node should be deleted

time complex: O(n)  

space complex: O(1)

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* p = head;
        int length = 0;
        while(p->next != NULL){
            length++;
            p = p->next;
        }
        p = head;
        ListNode* pLast = NULL;
        for(int i = 0;i<length-n+1;i++){
            pLast = p;
            p = p->next;
        }
        if(p == head)
            head = p->next;
        else{
           pLast->next = p->next;
        }
        delete p;
        return head;
    }
};

```
***
Follow up:

Could you do this in one pass? 

Use two pointer.
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* p = head;
        ListNode* pDelete = NULL;
        for(int i =0;i<n-1;i++){
            p = p->next;
        }
        if(p->next ==NULL){
            pDelete = head;
            head = head->next;
            delete pDelete;
        }
        else{
            p = p->next;
            ListNode* pLast = head;
            while(p->next != NULL){
                p = p->next;
                pLast = pLast->next;
            }
            pDelete = pLast->next;
            pLast->next = pLast->next->next;
            delete pDelete;
        }
        return head;
    }
};
```
