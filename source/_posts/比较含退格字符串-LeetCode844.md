---
title: 比较含退格字符串-LeetCode844
date: 2019-10-04 14:38:46
tags: ["LeetCode","栈"]
---
链接:https://leetcode-cn.com/problems/backspace-string-compare/
思路:1.将字符串依次入栈，如果遇到"#"就进行pop()操作, 进行pop()时候要判断是否stack为空
<!--more-->
```
class Solution {
public:
    bool backspaceCompare(string S, string T) {
     		stack<char> s_first, t_second;
		for (int i = 0; i < S.size(); i++)
		{
			if ('#' == S[i] )
			{
				if (!s_first.empty()) {
					s_first.pop();
				}
				else
				{
					continue;
				}
				
			}
			else
			{
				s_first.push(S[i]);
			}
		}
		for (int i = 0; i < T.size(); i++)
		{
			if ('#' == T[i])
			{
				if (!t_second.empty()) {
					t_second.pop();
				}
				else
				{
					continue;
				}
			}
			else
			{
				t_second.push(T[i]);
			}
		}
		if (s_first.size() != t_second.size())
		{
			return false;
		}
		else if (s_first.size() == 0 && t_second.size()==0)
		{
			return true;
		}
		else
		{
			while (!s_first.empty() && !t_second.empty())
			{
				char s = s_first.top();
				char t = t_second.top();
				if (s != t)
				{
					return false;
				}
				else
				{
					s_first.pop();
					t_second.pop();
				}
			}
		}
		return true;
    }
};
```
运行图：
![](run.png)
