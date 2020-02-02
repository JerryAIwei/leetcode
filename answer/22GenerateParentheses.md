Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4


source:LeetCode https://leetcode-cn.com/problems/merge-two-sorted-lists/
***

Loop, pay attention to empty list

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL) return l2;
        else if (l2==NULL) return l1;
        else{
            ListNode* lSmall = l1->val<l2->val?l1:l2;
            ListNode* lLarge = l1->val>=l2->val?l1:l2;
            ListNode* result = lSmall;
            ListNode* tempS = NULL;
            ListNode* tempL = NULL;
            while(lSmall!=NULL){
                if(lSmall->next==NULL||lSmall->next->val>=lLarge->val){
                    tempS = lSmall->next;
                    lSmall->next = lLarge;
                    if(tempS == NULL) return result;
                    else{
                        while(lLarge!=NULL){
                            if(lLarge->next==NULL||tempS->val<lLarge->next->val){
                                tempL = lLarge->next;
                                lLarge->next = tempS;
                                if(tempL == NULL) return result;
                                else{
                                    lSmall = tempS;
                                    lLarge = tempL;
                                    break;
                                }
                            }
                            else{
                                lLarge = lLarge->next;
                            }
                        }
                    }
                }
                else{
                    lSmall = lSmall->next;
                }
            }
            return result;
        }
    }
};
```
Recursion
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL) return l2;
        else if (l2==NULL) return l1;
        else{
            if(l1->val<l2->val) {
                l1->next = mergeTwoLists(l1->next,l2);
                return l1;
            }
            else {
                l2->next = mergeTwoLists(l2->next,l1);
                return l2;
            }
        }
    }
};

```