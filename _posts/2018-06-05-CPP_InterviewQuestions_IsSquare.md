---
layout: post
excerpt_separator: <!--more-->
title: "C and C++ Programming Questions. Is Square?"
date: 2018-06-05
tags: C C++ programming algorithms
---

__Question:__
Given four different points in space. Find these points can form a square or not. <!--more-->
*Input:*
The first line of input contains an integer T denoting the number of test cases.
The first line of each test case contains x1, y1, x2, y2, x3, y3, x4, y4 (four points coordinates).
*Output:*
Print "Yes" (without quotes) if it is square else "No".
*Constraints:*
1 ≤ T ≤ 30
1 ≤ x1, x2, x3, x4, y1, y2, y3, y4 ≤ 100
*Example:*
**Input**
1
20 10 10 20 20 20 10 10
**Output**
Yes

__Solution:__
The solution is to find distance between two points. If distance between p1 to p2 is same as distance between p3 and p4, and distance between p1 and p4 and p2 and p3 are same, then it is square.
```
typedef struct
{
	int8_t x;
	int8_t y;
} Points_t;

int8_t dist(Points_t p, Points_t q)
{
	return ((p.x - q.x) * (p.x - q.x) + (p.y - q.y) * (p.y - q.y));
}

bool is_square(char * ip, int8_t len)
{
	if(ip != NULL && len == 8)
	{
		Points_t p1, p2, p3, p4;
		p1.x = ip[0];
		p1.y = ip[1];
		p2.x = ip[2];
		p2.y = ip[3];
		p3.x = ip[4];
		p3.y = ip[5];
		p4.x = ip[6];
		p4.y = ip[7];

		if( (dist(p1,p2) == dist(p3,p4)) && 
			(dist(p1,p3) == dist(p2,p4)))
		{
			return true;
		}
		else
		{
			return false;
		}
	}
}

//Usage
int main()
{
    char arr[8] = {20, 10, 10, 20, 20, 20, 10, 10};
    char arr2[8] = {10, 10, 10, 20, 20, 20, 10, 10};
    
    cout << "Is Square : " << is_square(arr, 8); 
	cout << "Is Square : " << is_square(arr2, 8); 
    return 0;
}
```
