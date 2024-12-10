---
title: 棒球比赛-LeetCode682
date: 2019-10-04 14:49:55
tags: ["LeetCode", "栈"]
---
题目链接:https://leetcode-cn.com/problems/baseball-game/
解题思路:循环遍历vector,将每一轮的分值进行计算入stack,(注意:"C"字符是操作将有效分数变为无效)
<!--more-->
```
class Solution {
public:
    int calPoints(vector<string>& ops) {
    	stack<int> s;
		int result = 0;
		for (int i = 0; i < ops.size(); i++)
		{
			if ("C" == ops[i]) {
				s.pop();
			}
			else if ("D" == ops[i]) {
				int pre = s.top();
				int now = 2 * pre;
				s.push(now);
			}
			else if ("+" == ops[i])
			{
				int pre = s.top();
				s.pop();
				int pre_pre = s.top();
				int now = pre + pre_pre;
				s.push(pre);
				s.push(now);
			}
			else
			{
				int value = stoi(ops[i]);
				s.push(value);
			}
		}
		while (!s.empty())
		{
			result = result + s.top();
			s.pop();
		}
		return result;    
    }
};
```
运行图：
![](run.png)