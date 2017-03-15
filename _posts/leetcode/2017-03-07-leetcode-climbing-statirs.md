---
layout: exercise
title:  070. Climbing Stairs 
category: leetcode
tags: [Leetcode, Easy, dp]
date: 2017-03-07 00:00:00 -0000
---

[ Leetcode 70. Climbing Stairs ](https://leetcode.com/problems/climbing-stairs/)

### *Description:*

You are climbing a stair case. It takes n steps to reach to the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


### *Node:*
Given n will be a positive integer. 


### *Accepted Solution:*

{% highlight c++ linenos %}
class Solution {
int table[32767];
bool solve[32767];
public:
    int find(int n){
      table[0]=0;
      table[1]=1;
      table[2]=2;
      solve[0]=true;
      solve[1]=true;
      solve[2]=true;
      
      if(solve[n]) return table[n];
      
      table[n]=find(n-1)+find(n-2);
      solve[n]=true;
        
        return table[n];
    }
    int climbStairs(int n) {
        int res=find(n);
        return res;
    }
};

{% endhighlight %}

