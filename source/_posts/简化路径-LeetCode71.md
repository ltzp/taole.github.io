---
title: 简化路径-LeetCode71
date: 2019-10-04 14:16:27
tags: ["LeetCode", "栈", "拆分字符串"]
---
以 Unix 风格给出一个文件的绝对路径，你需要简化它。或者换句话说，将其转换为规范路径。
在 Unix 风格的文件系统中，一个点（.）表示当前目录本身；此外，两个点 （..） 表示将目录切换到上一级（指向父目录）；两者都可以是复杂相对路径的组成部分。更多信息请参阅：Linux / Unix中的绝对路径 vs 相对路径
请注意，返回的规范路径必须始终以斜杠 / 开头，并且两个目录名之间必须只有一个斜杠 /。最后一个目录名（如果存在）不能以 / 结尾。此外，规范路径必须是表示绝对路径的最短字符串。
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/simplify-path
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
解题思路:1.先进行字符串拆分，按照‘/’拆分。2.拆分之后遍历vector,如果“..”出栈,正常路径名则入栈。3.再入一个新stack,并且输出
<!--more-->
```
class Solution {
public:
    string simplifyPath(string path) {
        istringstream iss(path);
		vector<string> splitResult;
		stack<string> result;
		stack<string> outResult;
		string temp;
		string myBack;
		while (getline(iss, temp, '/'))
		{
			splitResult.push_back(temp);
		}
		for (int i = 0; i < splitResult.size(); i++)
		{
			string curr = splitResult[i];
			if (".." == curr) {
				if (!result.empty()) {
					result.pop();
				}
			}
			else if ("." ==curr )
			{
				continue;
			}
			else if ("" == curr)
			{
				continue;
			}
			else
			{
				result.push(curr);
			}
		}
		while (!result.empty())
		{
			string singlePath = result.top();
			outResult.push(singlePath);
			result.pop();
		}
		if (outResult.empty()) {
			myBack = "/";
		}
		else
		{
			while (!outResult.empty())
			{
				myBack = myBack + "/" + outResult.top();
				outResult.pop();
			}
		}
		return myBack;
    }
};
```
运行图：
![](run.png)