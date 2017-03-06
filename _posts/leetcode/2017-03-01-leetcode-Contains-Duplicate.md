---
layout: exercise
title:   217. Contains Duplicate 
category: leetcode
tags: [Leetcode, Easy]
date: 2017-03-01 00:00:00 -0000
---

[Leetcode  217.Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

### *Description:*

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct. 


### *Accepted Solution:*

{% highlight c++ linenos %}

class Solution {

public:
    bool containsDuplicate(vector<int>& nums) {
        if (nums.size()<=1) return false;
        sort(nums.begin(), nums.end());
        for(int i=0; i<nums.size()-1; i++){
            if(nums[i]==nums[i+1]) return true;
        }
    return false;
        
    }
};

{% endhighlight %}

### *Some Thoughts:*
Sort could be used directly in c++ to sort vector. The syntax is <mark> sort(first,last)</mark>


