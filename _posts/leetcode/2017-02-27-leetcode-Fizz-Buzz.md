---
layout: exercise
title:  412. Fizz Buzz
category: leetcode
tags: [Leetcode, Easy]
date: 2017-02-27 00:00:00 -0000
---

[Leetcode 412.Fizz Buzz](https://leetcode.com/problems/fizz-buzz/)

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

### *Example:*
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]

### *Accepted Solution:*

{% highlight c++ linenos %}
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        int count=0;
        vector<string> res;
        while(count!=n){
            count=count+1;
            if(count%15==0){
                res.push_back("FizzBuzz");
            }else if(count%3==0){
            res.push_back("Fizz");
        }else if(count%5==0){
            res.push_back("Buzz");
        }else{
            res.push_back(to_string(count));
        }
        }
        return res;
    }
};
{% endhighlight %}
