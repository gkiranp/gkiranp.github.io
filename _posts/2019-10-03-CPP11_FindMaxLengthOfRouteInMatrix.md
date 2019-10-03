---
layout: post
excerpt_separator: <!--more-->
title: "C++11 - Find Maximum length of a route in a Matrix"
date: 2019-10-03
tags: C++11 programming algorithms
---

__Question:__
Given a rectangular path in the form of Binary Matrix. Find the length of longest possible route 
from source points to destination points.<!--more-->
Rules:
- In a binary matrix, you can move 1 adjacent position only if its value is non-zero (that is 1).
- There shall not be any cycles in the output path

*Input:*
A binary matrix 'Mat' of size 'MxN', where (M > 0 and M <= 1000) and (N > 0 and N <= 1000).
Given, starting points (x1, y1) and end points (x2, y2), where (x1,y1 > 0 and x2,y2 > 0) and (x1,x2 < M and y1,y2 < N)

*Output:*
Print "Longest Path = max-distance".

Example input:
int M = 10;
int N = 10;
int Mat[M][N] = 
{
	{ 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
	{ 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
	{ 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
	{ 0, 0, 0, 0, 1, 0, 0, 1, 0, 0 },
	{ 1, 0, 0, 0, 1, 1, 1, 1, 1, 1 },
	{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 0 },
	{ 1, 0, 0, 0, 1, 0, 0, 1, 0, 1 },
	{ 1, 0, 1, 1, 1, 1, 0, 0, 1, 1 },
	{ 1, 1, 0, 0, 1, 0, 0, 0, 0, 1 },
	{ 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 }
};

(x1,y1) = (0,0)
(x2,y2) = (5,7)

Output:
Longest Path = 22

__Solution:__

The solution is to use Backtracking. We start from given source cell and explore all four paths possible by recursively checking 
whether they lead to destination path or not. We need to keep track of current distance of the cell from the source. We update 
the values of longest path when we reach the destination.
If the path doesn't lead to destination or we have explored all possible routes from current cell, then we will backtrack. 
To make sure that path doesn't contain any cycle, we keep track of cells involved in current path in matrix and before exploring 
any cell we shall ignore it if it is already covered in current path.

Here is C++11 based solution for the same:

```
#include <iostream>
#include <vector>
using namespace std;

// declare a structure to store points
class Pos_t 
{
public:
    int x;
    int y;
    Pos_t(int i, int j): x(i), y(j) {;} //ctr
};

// define M and N
const int M = 10;
const int N = 10;

//Define MxN Matrix
std::vector<std::vector<int>>Mat {  { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                                    { 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
		                            { 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
		                            { 0, 0, 0, 0, 1, 0, 0, 1, 0, 0 },
		                            { 1, 0, 0, 0, 1, 1, 1, 1, 1, 1 },
		                            { 1, 1, 1, 1, 1, 1, 1, 1, 1, 0 },
		                            { 1, 0, 0, 0, 1, 0, 0, 1, 0, 1 },
		                            { 1, 0, 1, 1, 1, 1, 0, 0, 1, 1 },
		                            { 1, 1, 0, 0, 1, 0, 0, 0, 0, 1 },
		                            { 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 }    };

//Declaring another Matrix of MxN to keep track of Visited cells
std::vector<std::vector<int>>Visited;

// check if it is possible to reach to position (x, y) from 
// current position. The function returns false if the cell
// has value 0 or it is already visited.
auto is_reachable = [&Mat, &Visited](Pos_t &&p) {
    bool ret = (Mat[p.x][p.y] == 0 || Visited[p.x][p.y])? false: true; return ret;
};

// check validity of position
auto is_valid_position = [&M, &N](Pos_t &&p) {
    bool ret = (p.x < M && p.y < N && p.x >= 0 && p.y >= 0) ? true: false; return ret;
};

// Find Longest Possible Route in a Matrix mat from source cell (0, 0) to
// destination cell (x, y)
// max_dist is passed by reference and stores length of longest path from 
// source to destination found so far dist maintains length of path from 
// source cell to current cell (i, j)
void find_max_distance(Pos_t &&src, Pos_t dst, int& max_dist, int dist)
{
	// if destination is found, update max_dist
	if (src.x == dst.x && src.y == dst.y) 
	{
		max_dist = max(dist, max_dist);
		return;
	}
	
	// set (i, j) cell as visited
	Visited[src.x][src.y] = 1;
	
	// go to bottom cell
	if (is_valid_position(Pos_t(src.x+1, src.y)) && is_reachable(Pos_t(src.x+1, src.y))) {
	    find_max_distance(Pos_t(src.x+1, src.y), dst, max_dist, dist + 1);
	}

	// go to right cell			
	if (is_valid_position(Pos_t(src.x, src.y+1)) && is_reachable(Pos_t(src.x, src.y+1))) {
		find_max_distance(Pos_t(src.x, src.y+1), dst, max_dist, dist + 1);
	}
	
	// go to top cell
	if (is_valid_position(Pos_t(src.x-1, src.y)) && is_reachable(Pos_t(src.x-1, src.y))) {
		find_max_distance(Pos_t(src.x-1, src.y), dst, max_dist, dist + 1);
	}
	
	// go to left cell
	if (is_valid_position(Pos_t(src.x, src.y-1)) && is_reachable(Pos_t(src.x, src.y-1))) {
		find_max_distance(Pos_t(src.x, src.y-1), dst, max_dist, dist + 1);
	}
	
	// Backtrack - Remove src points from visited matrix
	Visited[src.x][src.y] = 0;
}

// Usage
int main()
{
	//Resize our Visited Matrix to custom length, 
	//let default value be 0
	Visited.resize(M, vector<int> (N, 0));
	
	int max_dist = 0;

	// (0,0) are the source cell and (5, 7) are the destination cell coordinates
	Pos_t dst(5,7);
	find_max_distance( Pos_t(0,0), dst, max_dist, 0);

	cout << "Longest Path = " << max_dist;

	return 0;
}
```
