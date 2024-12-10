---
title: 有序链表合并-LeetCode21-23
date: 2019-10-01 18:33:09
tags: ["LeetCode", "链表", "分治算法"]
---
两个有序链表合并的思路有两种1.利用递归的思路 2.创建一个空的链表,并且用一个指针指向这个空链表。
多个链表合并利用分治算法的思想:将原问题划分成n个规模较小，并且结构与原问题相似的子问题，递归地解决这些子问题，然后再合并其结果，就得到原问题的解。
利用分治算法的前提条件:
1.原问题与分解成的小问题具有相同的模式；
2.原问题分解成的子问题可以独立求解，子问题之间没有相关性，这一点是分治算法跟动态规划的明显区别；
3.具有分解终止条件，也就是说，当问题足够小时，可以直接求解；
4.可以将子问题合并成原问题，而这个合并操作的复杂度不能太高，否则就起不到减小算法总体复杂度的效果了。
<!--more-->
```
1.递归
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == NULL){
            return l2;
        }
        else if (l2 == NULL){
            return l1;
        } else {
            if(l1->val <= l2->val){
                l1->next = mergeTwoLists(l1->next, l2);
                return l1;
            }else{
                l2->next = mergeTwoLists(l1, l2->next);
                return l2;
            }
        }
    }
```
```
#2.空链表 + 指针
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode temp_head(0);
        ListNode *pre = &temp_head;
        while (l1 && l2)
        {
            if(l1->val < l2->val){
                pre->next = l1;
                l1 = l1->next;
            }else
            {
                pre->next = l2;
                l2 = l2->next;
            }
            pre = pre->next;
        }
        if (l1){
            pre->next = l1;
        }
        if (l2){
            pre->next = l2;
        }
        return temp_head.next;        
    }
```
```
#3.合并多个有序链表-分治算法
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0){
            return NULL;
        }
        if(lists.size() == 1){
            return lists[0];
        }
        if(lists.size() == 2){
            return mergeTwoLists(lists[0], lists[1]);
        }
        vector<ListNode*> subList1;
        vector<ListNode*> subList2;
        int mid = lists.size()/2;
        for (int i = 0; i < mid; i++){
            subList1.push_back(lists[i]);
        }
        for(int i = mid; i < lists.size(); i++){
            subList2.push_back(lists[i]);
        }
        ListNode *l1 = mergeKLists(subList1);
        ListNode *l2 = mergeKLists(subList2);
        return mergeTwoLists(l1, l2);
    }
```
