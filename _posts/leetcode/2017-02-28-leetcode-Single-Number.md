---
layout: exercise
title:  136. Single Number
category: leetcode
tags: [Leetcode, Easy]
date: 2017-02-28 00:00:00 -0000
---

[Leetcode 136.Single Number](https://leetcode.com/problems/single-number/)

### *Description:*

Given an array of integers, every element appears twice except for one. Find that single one.

#### *Note:*
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory? 

### *Accepted Solution:*
{% highlight c++ linenos %}

class Solution {
public:
    int singleNumber(vector<int>& nums) {
        map<int, char> mymap;
        map<int, char> ::iterator it;

        int size=nums.size();
        for(int i=0; i<size; i++){
            int a=nums[i];
            it=mymap.find(a);
            if(it!=mymap.end()){
                mymap.erase(it);
            }else{
                mymap[a]='Y';
            }
            
        }
     int b = mymap.begin()->first;
        return b;
    }
};


{% endhighlight %}

### *Someone's talented answer:*
#### Discuss Area:
known that A XOR A = 0 and the XOR operator is commutative, the solution will be very straightforward.

For anyone who didn't understood why this works here is an explanation. This XOR operation works because it's like XORing all the numbers by itself. So if the array is {2,1,4,5,2,4,1} then it will be like we are performing this operation

```
((2^2)^(1^1)^(4^4)^(5)) => (0^0^0^5) => 5.

```
Hence picking the odd one out ( 5 in this case).

#### Sample code soulution:

{% highlight c++ linenos %}

int singleNumber(int A[], int n) {
    int result = 0;
    for (int i = 0; i<n; i++)
    {
		result ^=A[i];
    }
	return result;
}


{% endhighlight %}
