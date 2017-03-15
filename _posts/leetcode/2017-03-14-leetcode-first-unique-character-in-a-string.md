---
layout: exercise
title:   387. First Unique Character in a String 
category: leetcode
tags: [Leetcode, Easy]
date: 2017-03-14 00:00:00 -0000
---

[Leetcode  387. First Unique Character in a String ](https://leetcode.com/problems/first-unique-character-in-a-string/)

### *Description:*
 Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1. 

### *Example:*

s = "leetcode"
return 0.

s = "loveleetcode",
return 2.


### *Accepted Solution:*

{% highlight c++ linenos %}

class Solution {
public:
    int firstUniqChar(string s) {
        map<char, int> nums;
        map<char, int>::iterator it;
        for(int i=0; i<s.size(); i++){
            char letter=s.at(i);
            if(nums.find(letter)!=nums.end()){
                nums[letter]=-1;
            }else{
                nums[letter]=i;
            }
        }
        int min=-1;
        int count=0;
        for(it=nums.begin(); it!=nums.end(); it++){
            if(it->second!=-1){
                if(count==0) min=it->second;
                int ele=it->second;
                if(ele<min) min=ele;
                count++;
            }
        }
        return min;
        
    }
};



{% endhighlight %}

### *Some thoughts :* a much faster one

1. Get the frequency of each character. 
2. Get the first character that has a frequency of one.


{% highlight c++ linenos %}

class Solution {
public:
    int firstUniqChar(string s) {
    int letter[26]={0};
    for(int i=0; i<s.size(); i++){
        int index=s[i]-'a';
        letter[index]++;
    }
    
    
    for(int i=0; i<s.size(); i++){
        if(letter[s[i]-'a']==1) return i;
    }
        return -1;
    }
};


{% endhighlight %}