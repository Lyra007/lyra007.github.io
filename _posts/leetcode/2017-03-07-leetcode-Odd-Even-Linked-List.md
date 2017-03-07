---
layout: exercise
title:  328. Odd Even Linked List
category: leetcode
tags: [Leetcode, Medium, Linked List]
date: 2017-03-07 00:00:00 -0000
---

[Leetcode 328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

### *Description:*

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.


### *Example:*

Given <mark>1->2->3->4->5->NULL,</mark>
return <mark>1->3->5->2->4->NULL. </mark>

### *Node:*
The relative order inside both the even and odd groups should remain as it was in the input.
The first node is considered odd, the second node even and so on ... 

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
    ListNode* oddEvenList(ListNode* head) {
        if(head==NULL) return head;
        if(head->next==NULL) return head;
        vector<int> odds;
        vector<int> even;
        int count=0;
        ListNode* tmp=head;
        ListNode* h=head;
        bool odd=true;
        
        while(tmp->next!=NULL){
            if(odd){
                count++;
                odds.push_back(tmp->val);
                tmp=tmp->next;
                odd=false;
            }else{
                even.push_back(tmp->val);
                tmp=tmp->next;
                odd=true;
            }
        }
        if(odd){
            count++;
            odds.push_back(tmp->val);
        }else{
            even.push_back(tmp->val);
        }
        for(int i=0; i<count; i++){
            head->val=odds[i];
            head=head->next;
        }

        int j=0;
        while(head->next!=NULL){
            head->val=even[j];
            j++;
            head=head->next;
        }
        head->val=even[j];
        
        return h;
    }
};


{% endhighlight %}

### *Some thoughts :*
Basically, my idea is to keep the linked list stay where they are and change the val of each node. Another idea to solve this is to seperate the listed list to the even linked list and odd linked list. And join them at the end of program. Below is sample code.

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
    ListNode* oddEvenList(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;
        ListNode* odd=head;
        ListNode* even=head->next;
        ListNode* even_head=even;
        while(even!=NULL && even->next!=NULL){
           odd->next=odd->next->next;
           even->next=even->next->next;
           odd=odd->next;
           even=even->next;
        }
        odd->next=even_head;
        return head;
    }
};
{% endhighlight %}

For understanding of line <mark> while(even!=NULL && even->next!=NULL)</mark>, the best explanation could be there is a invisible null at the end of linked list. For example, linked list 1->2->3 could be regarded as 1->2->3->NULL. The next node of 3 is NULL. Thus, in this case, <mark>even->next=even->next->next</mark> equals NULL. Then <mark>even=even->next</mark> is NULL as well. Thus, condition in while loop put the even!=NULL at first, if even==NULL it will return false directly. 