---
layout: post
title: 常用算法
categories: [计算机]
description: 
keywords: 算法
---

算法

#### Q1 

> You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.You may assume the two numbers do not contain any leading zero, except the number 0 itself.**Input:** (2 -> 4 -> 3) + (5 -> 6 -> 4)
> **Output:** 7 -> 0 -> 8

```c++
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
    
 
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
       
        ListNode *listhead = NULL;
        ListNode *list = NULL;
        
        int lastNum = 0;
        while (l1!=NULL || l2!=NULL || lastNum>0){
            
            int value1 = (l1!=NULL)?(l1->val):0;
            int value2 = (l2!=NULL)?(l2->val):0;
            
            int totalNum = value1+value2+lastNum;
            int num = (totalNum)%10;
            lastNum = (totalNum)/10;
            
            ListNode *tmpNode = new ListNode(num);
           
            if(list == NULL){
                listhead = tmpNode;
                list = listhead;
            }
            else{
                list->next = tmpNode;
                list = list->next;
            }
            
            if (l1!=NULL) l1=l1->next;
            if (l2!=NULL) l2=l2->next;
        }
    
        return listhead;
    }
};
```

