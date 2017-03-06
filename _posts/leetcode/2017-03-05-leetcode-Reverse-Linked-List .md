---
layout: exercise
title:  206. Reverse Linked List 
category: leetcode
tags: [Leetcode, Easy, Linked List]
date: 2017-03-05 00:00:00 -0000
---

[Leetcode 206.Reverse Linked List ](https://leetcode.com/problems/reverse-linked-list/)

### *Description:*

Reverse a singly linked list.



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
    ListNode* reverseList(ListNode* head) {
    if(head==NULL) return head;
    ListNode* tmp=head;
    ListNode* new_head=head;
    ListNode* reverse=NULL;
    
    while(tmp->next!=NULL){
          tmp=tmp->next;
          new_head->next=reverse;
          reverse=new_head;
          new_head=tmp;  
    }
    tmp->next=reverse;
    reverse=tmp;
    return reverse;
    }

};

{% endhighlight %}

### *Some thoughts :*
When I wrote codes, I always met same error message which is <mark>Error: member access within null pointer of type 'struct ListNode'</mark>. This confused me for a while. Finally, the reason comes out which is because of the order of code.

{% highlight c++ %}

    while(tmp->next!=NULL){
          new_head->next=reverse;
          reverse=new_head;
          new_head=tmp; 
        tmp=tmp->next;
    }
{% endhighlight %}

The above code leads to the error, which is because when change the next node of new_head to NULL, then the tmp->next will be NULL as well. This leads to the above error. So when changing the point of the next node of new_head, save it to tmp first to avoid the impact.