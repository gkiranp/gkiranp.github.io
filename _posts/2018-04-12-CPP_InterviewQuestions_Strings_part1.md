---
layout: post
excerpt_separator: <!--more-->
title: "C and C++ Programming Questions . Strings . Part 1"
date: 2018-04-12
tags: C C++ programming strings
---

Following are list of common programming questions with respect to `Strings` and its manupulations. I insist you read the question and come back with your own program solution before you read answer. <!--more-->

Q: Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.
The input string does not contain leading or trailing spaces and the words are always separated by a single space.
For example,
Given s = "the sky is blue",
return "blue is sky the".
Could you do it in-place without allocating extra space?

Solution:
```
void reverse(char[] s, int i, int j)
{
    while(i < j)
	{
        char temp = s[i];
        s[i] = s[j];
        s[j] = temp;
        i++;
        j--;
    }
}

void reverseWords(char[] s, const int length)
{
    int i = 0;
    for(int j=0; j < length; j++)
	{
        if(s[j]==' ')
		{
            reverse(s, i, j-1);        
            i = j++;
        }
    }
    reverse(s, i, (length-1));
    reverse(s, 0, (length-1));
}

```
---

Q: Rotate an array of n elements to the right by k steps.
For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4]. 
How many different ways do you know to solve this problem?

Solution 1: Intermediate Array | Space is O(n) and time is O(n).
```
void rotate(int[] nums, const int length, int k) 
{
    if(k > length) 
	{
		k = k % length;
	}
	int *result = new int[length];
 
    for(int i=0; i < k; i++)
	{
        result[i] = nums[length - k+i];
    }

    int j=0;
    for(int i = k; i < length; i++)
	{
        result[i] = nums[j];
        j++;
    }

    (void)memcpy(nums, result, length);
	delete [] result;
}
```

Solution 2: Bubble Rotate | Time is O(n*k)
```
void rotate(int[] arr, const int length, const int order)
{
	if (arr != NULL || order > 0)
	{
	    for (int i = 0; i < order; i++) 
		{
			for (int j = length - 1; j > 0; j--) 
			{
				int temp = arr[j];
				arr[j] = arr[j - 1];
				arr[j - 1] = temp;
			}
		}
	}	
}
```

Solution 3: Reversal | Space O(1) and Time O(n)
```
void reverse(int[] arr, int left, int right)
{
	while((left < right) && (arr != NULL))
	{
		int temp = arr[left];
		arr[left] = arr[right];
		arr[right] = temp;
		left++;
		right--;
	}	
}

void rotate(int[] arr, const int length, int order) 
{	
	if (arr != NULL || length > 0 || order > 0) 
	{
		if(order > length)
		{
			order = order % length;
		}
	
		//length of first part
		int a = length - order;
		reverse(arr, 0, a-1);
		reverse(arr, a, length-1);
		reverse(arr, 0, length-1);
	} 
}
```

---

Q: Given two strings s and t, determine if they are isomorphic. 
Two strings are isomorphic if the characters in s can be replaced to get t.
For example,"egg" and "add" are isomorphic, "foo" and "bar" are not.

Solution: | Time complexity is O(n*n)
```
bool isIsomorphic(std::string s, std::string t)
{
    if(s.empty() || t.empty())
	{
		return false;
	}
 
    if(s.length() != t.length())
	{
		return false;
	}

	std::map<char,char> mymap;

    for(int i=0; i < s.length(); i++)
	{
        char c1 = s.at(i);
        char c2 = t.at(i);
 
        if(mymap.find(c1) != mymap.end())
		{
            if(mymap.at(c1) != c2)// if not consistant with previous ones //C++11 and above
			{
				return false;
			}
        }
		else
		{
            if(mymap.find(c2) != mymap.end()) //if c2 is already being mapped. Time complexity O(n) here
			{
				return false;
			}
			//Here is your map filling activity
            mymap[c1] = c2;
        }
    }
 
    return true;
}
```

---

Q: Find the kth largest element in an unsorted array. 
Note that it is the kth largest element in the sorted order, not the kth distinct element.
You may assume k is always valid, 1 ≤ k ≤ array's length
For example, given [3,2,1,5,6,4] and k = 2, return 5.

Solution 1: Power of C++ Algorithms | Time is O(nlog(n))
```
#include <algorithm>
int findKthLargest(int[] nums, const int length, int k) 
{
    sort(nums, (nums+length));
    return (nums[length - k]);
}
```

Solution 2: Quick Sort | Average case time is O(n), worst case time is O(n^2)

``` 
void swap(int[] nums, int n1, int n2) 
{
	int tmp = nums[n1];
	nums[n1] = nums[n2];
	nums[n2] = tmp;
}

int getKth(int k, int[] nums, int start, int end) 
{ 
	int pivot = nums[end];
	int left = start;
	int right = end;
 
	while (true) 
	{
 
		while (nums[left] < pivot && left < right) 
		{
			left++;
		}
 
		while (nums[right] >= pivot && right > left) 
		{
			right--;
		}

		if (left == right) 
		{
			break;
		} 

		swap(nums, left, right);
	}

	swap(nums, left, end);
 
	if (k == left + 1) 
	{
		return pivot;
	} 
	else if (k < left + 1) 
	{
		return getKth(k, nums, start, left - 1);
	}
	else 
	{
		return getKth(k, nums, left + 1, end);
	}
}

int findKthLargest(int[] nums, const int length, int k) 
{
	if (k < 1 || nums == NULL) 
	{
		return 0;
	}

	return getKth(length - k +1, nums, 0, length - 1);
}
```
