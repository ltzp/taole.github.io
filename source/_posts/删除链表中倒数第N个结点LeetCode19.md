---
title: 删除链表中倒数第N个结点LeetCode19
date: 2019-10-01 20:17:09
tags: ["LeetCode", "链表"]
---
    删除链表中倒数第N个结点思路:1.倒数第N个也就是顺序第length-1个结点后面的一个结点删除2.length 和 N 相等时,则是删除头结点,直接返回head->next就行
<!--more-->
```
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
 };
 
int get_length(ListNode* head){
    int num = 0;
    while (head)
    {
        num ++;
        head = head->next;
    }
    return num;
}

class Solution {
public:
	ListNode* removeNthFromEnd(ListNode* head, int n) {
		int length = get_length(head);
		int delete_num = length - n - 1;
		if (length == n) {
			return head->next;
		}
		ListNode *temp = head;
		while (temp)
		{
			if (delete_num == 0) {
				temp->next = temp->next->next;
				break;
			}
			temp = temp->next;
			delete_num--;

		}
		return head;
	}
};
```
![](/images/runLeetCode19.png)
