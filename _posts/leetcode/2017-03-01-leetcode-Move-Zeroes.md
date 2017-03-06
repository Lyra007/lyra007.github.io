---
layout: exercise
title:  283. Move Zeroes 
category: leetcode
tags: [Leetcode, Easy]
date: 2017-03-01 00:00:00 -0000
---

[Leetcode 283.Move Zeroes ](https://leetcode.com/problems/move-zeroes/)

### *Description:*
 
 Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.


### *Example:*
For example, given <mark>nums = [0, 1, 0, 3, 12]</mark>, after calling your function, nums should be <mark>[1, 3, 12, 0, 0]</mark>. 


### *Note:*
* You must do this in-place without making a copy of the array.
* Minimize the total number of operations.


### *Accepted Solution:*

{% highlight c++ linenos %}

class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int size=nums.size();
        int count=0;
        for(int i=0; i<size; i++){
            if(nums[i]==0) count++;
        }
        
        if(count!=size){
            for(int i=0; i<size;i++)
            {
                int diff=size-count;
                if(i<diff){
                int j=i;
                while((nums[i]==0)&&(j<size)){
                    j++;
                    nums[i]=nums[j];
                    nums[j]=0;
                }
                }else{
                    nums[i]=0;
                }
                
            }
        }
    }
};

{% endhighlight %}

### *Someone's Talented Solution:*
{% highlight c++ linenos %}
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = 0;
        // move all the nonzero elements advance
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0) {
                nums[j++] = nums[i];
            }
        }
        for (;j < nums.size(); j++) {
            nums[j] = 0;
        }
    }
};
{% endhighlight %}

### *Discuss Area:*
The error I kept occuring is [RunTime Error](https://leetcode.com/problems/move-zeroes/?tab=Submission). The reason is infinite loop. 
Also, my answer is 29ms vs other's is 16ms.
