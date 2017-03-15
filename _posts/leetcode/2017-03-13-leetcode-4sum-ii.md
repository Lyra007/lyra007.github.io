---
layout: exercise
title:  454. 4Sum II 
category: leetcode
tags: [Leetcode, Medium]
date: 2017-03-13 00:00:00 -0000
---

[Leetcode 454. 4Sum II ](https://leetcode.com/problems/4sum-ii/)

### *Description:*
Given four lists A, B, C, D of integer values, compute how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.



### *Example:*

Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0


### *Accepted Solution:*

{% highlight c++ linenos %}

class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        map<int, int> sumFirst;
        int times=0;
        for(int i=0; i<A.size();i++){
         for(int j=0; j<B.size(); j++){
             int num=A[i]+B[j];
             if (sumFirst.find(num)!=sumFirst.end()) 
                {
                sumFirst[num]++;
                }else{
                    sumFirst[num]=1;

                }
        }
    }
    
    for(int i=0; i<C.size(); i++){
        for(int j=0; j<D.size(); j++){
            int num=C[i]+D[j];
            if(sumFirst.find(-num)!=sumFirst.end()){
                times=times+sumFirst[-num];
            }
        }
        
    }
        return times;
    
    
    }
};


{% endhighlight %}

### *Some thoughts :*

Baic idea is to 
'''
"Take the arrays A and B, and compute all the possible sums of two elements. Put the sum in the Hash map, and increase the hash map value if more than 1 pair sums to the same value.

Compute all the possible sums of the arrays C and D. If the hash map contains the opposite value of the current sum, increase the count of four elements sum to 0 by the counter in the map."
'''
cite from leetcode.