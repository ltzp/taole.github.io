---
title: 下一个更大的元素I-LeetCode496
date: 2019-10-04 15:00:24
tags: ["LeetCode", "栈"]
---
题目链接:https://leetcode-cn.com/problems/next-greater-element-i/
解题思路:1.将nums2进行遍历, 找出在它后面比他大的第一个数放入Map。
        2.特殊情况
          1.nums1为空的时候，直接返回空
          2.nums2的最后一个值永远是-1
        3.循环nums1数组，在对应的Map里面得到Value
<!--more-->
```
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
		stack<int> S;
		map<int, int> myMap;
		vector<int> allResult;
		if (nums1.size() == 0) {
			return allResult;
		}
		for (int i = 0; i < nums2.size(); i++)
		{
			for (int j = i+1; j < nums2.size(); j++)
			{
				if (nums2[j] > nums2[i]) {
					myMap[nums2[i]] = nums2[j];
					break;
				}
				else
				{
					myMap[nums2[i]] = -1;
				}
			}
		}
		myMap[nums2[nums2.size() - 1]] = -1;
		for (int i = 0; i < nums1.size(); i++)
		{
			map<int, int>::iterator obj = myMap.find(nums1[i]);
			allResult.push_back(obj->second);
		}
		return allResult;
	}
};
```
运行图：
![](run.png)