---
layout: exercise
title:   141. Linked List Cycle 
category: leetcode
tags: [Leetcode, Easy, Linked List]
date: 2017-03-02 00:00:00 -0000
---

[Leetcode  141.Linked List Cycle ](https://leetcode.com/problems/linked-list-cycle/)

### *Description:*
 Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space? 

### *Accepted Solution:*

{% highlight c++ linenos %}

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
     ListNode *slow;
     ListNode *fast;
     if(head!=NULL){
         slow=head;
         fast=head;
     }else{ return false;}
     while(fast->next!=NULL && fast->next->next!=NULL ){
         slow=slow->next;
         fast=fast->next->next;
        if(slow==fast) return true;

     }
    return false;
        
    }
};

{% endhighlight %}

### *Some thoughts:*

The idea behind this question is the [Floyd Cycle Detection Algorithm](https://zh.wikipedia.org/wiki/Floyd%E5%88%A4%E5%9C%88%E7%AE%97%E6%B3%95). The basic concept is "The idea is to have two references to the list and move them at different speeds. Move one forward by 1 node and the other by 2 nodes. If the linked list has a loop they will definitely meet."