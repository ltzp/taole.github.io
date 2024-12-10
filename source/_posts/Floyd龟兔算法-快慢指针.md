---
title: Floyd龟兔算法-快慢指针
date: 2019-11-05 21:51:30
tags: ['LeetCode', '链表', '判断是否有环']
---
题目链接:https://leetcode-cn.com/problems/linked-list-cycle-ii/
&emsp;&emsp;https://leetcode-cn.com/problems/find-the-duplicate-number/
快慢指针主要用于判断是否有环的情况
时间复杂度O(n),空间复杂度O(1)
<!--more-->
理解一:
![](a.png)
理解二:
![](b.png)
```
LeetCode287:
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int tortoise = nums[0];
		int hare = nums[0];
		//找到两个跑步者的交点。
		do
		{
			tortoise = nums[tortoise]; //乌龟走一步
			hare = nums[nums[hare]];//兔子走两步
		} while (tortoise != hare);
		//找到循环的“入口”。
		int ptr1 = nums[0];
		int ptr2 = hare;
		while (ptr1!=ptr2)
		{
			ptr1 = nums[ptr1];
			ptr2 = nums[ptr2];
		}
		return ptr1;
    }
};
```
