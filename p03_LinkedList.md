#### 0002 Add Two Numbers

```
给定两个链表，将链表中的值相加后逆转，
如果存在相加进位的情况，则向链表下一位 + 1

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```



1. 相加过程中同步构建链表

   * C++

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    * 
    * 直接构建一个新的 List
    * Time O(n)
    * Space O(n)
    */
   
   class Solution {
   public:
       ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
           ListNode* p1 = l1;
           ListNode* p2 = l2;
           ListNode* dummyHead = new ListNode(-1);
           ListNode* cur = dummyHead;
           int carried = 0;
           
           while( p1 != NULL || p2 != NULL || carried != 0) {
               int n1 = p1 != NULL ? p1->val : 0;
               int n2 = p2 != NULL ? p2->val : 0;
               p1 = p1 != NULL ? p1->next : NULL;
               p2 = p2 != NULL ? p2->next : NULL;
               int n3 = (n1 + n2 + carried) % 10;
               carried = (n1 + n2 + carried) / 10;
               cur->next = new ListNode(n3);
               cur = cur->next;
           }
           
           ListNode* ret = dummyHead->next;
           delete dummyHead;
           return ret;
       }
   };
   ```

   

