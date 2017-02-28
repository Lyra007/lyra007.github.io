---
layout: exercise
title: 104. Maximum Depth of Binary Tree 
category: leetcode
tags: [Leetcode, Easy]
date: 2017-02-28 00:00:00 -0000
---

[Leetcode 104.Maximum Depth of Binary Tree ](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

### *Description:*

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.


### *Accepted Solution:*

{% highlight c++ linenos %}

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int max_depth=0;
        if(root== NULL){
            return 0;
        }else{
        int a=1+maxDepth(root->left);
        int b=1+maxDepth(root->right);
        max_depth=max(a,b);
        }
        return max_depth;
        
    }
};


{% endhighlight %}

### *Some thoughts:*
The original code I wrote was wrong with error message (Runtime Error) saying 
```
member access within null pointer of type 'struct TreeNode'
```
. The reason of this is because  I used
```
TreeNode* move_left=root->left;
```
at the beginning of code. Poniter 'root' could be null in this situation. Thus, the error message will occur in this situation. 

Also, to check if a pointer is null or not. The word 'null' should be upcase which is 
```
NULL 
```
in c++.