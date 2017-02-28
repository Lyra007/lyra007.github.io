---
layout: exercise
title:  344. Reverse String
category: leetcode
tags: [Leetcode, Easy]
date: 2017-02-28 00:00:00 -0000
---

[Leetcode 344.Reverse String](https://leetcode.com/problems/reverse-string/)


Write a function that takes a string as input and returns the string reversed.

### *Example:*
Given s = "hello", return "olleh". 

### *Accepted Solution:*
{% highlight c++ linenos %}

class Solution {
public:
    string reverseString(string s) {
        int j=s.size();
        int i=0;
        
        while(i<j){
        swap(s[i],s[j-1]);
        i++;
        j--;
        }
        
        return s;
    }
};

{% endhighlight %}

### *Discuss:*
I have a [Memory Limit Exceeded](https://leetcode.com/submissions/detail/94811788/) error for original answer. The reason may be creating a varible that is exceeding memory.