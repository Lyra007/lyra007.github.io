---
layout: exercise
title:  237. Delete Node in a Linked List 
category: leetcode
tags: [Leetcode, Easy, unsolved, linked list]
date: 2017-03-01 00:00:00 -0000
---

[Leetcode 237.Delete Node in a Linked List ](https://leetcode.com/problems/delete-node-in-a-linked-list/)

### *Description:*

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.


### *Example:*

Supposed the linked list is <mark> 1 -> 2 -> 3 -> 4</mark> and you are given the third node with value 3, the linked list should become <mark> 1 -> 2 -> 4 </mark> after calling your function. 



### *Other's Accepted Solution:*

#### Note:
We can't really delete the node, but we can kinda achieve the same effect by instead removing the next node after copying its data into the node that we were asked to delete.

##### Solution One:
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
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
              
    }
};

{% endhighlight %}



##### Solution Two:
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
void deleteNode(ListNode* node) {
    auto next = node->next;
    *node = *next;
    delete next;
}
};

{% endhighlight %}

### *Discuss Area:*
I have problem on how to refer to the varibles in the struct the other day. However, it seems that it is similar to point to a int as well as a pointer. For the example above, the val can be refered to using <mark>node->val</mark>, which is similar as refering next pointer using <mark>node->next</mark>.