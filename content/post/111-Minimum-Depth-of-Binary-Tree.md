+++
title = "111. Minimum Depth of Binary Tree"
date = "2020-08-21T17:21:10+08:00"
toc = true
tags = ["LeetCode", "learning"]
categories = ["LeetCode", "递归", "深度优先搜索", "广度优先搜索"]
description = ""
+++


Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.

<!--more-->

```c++
//深度优先搜索
class Solution1 {
public:
   int minDepth(TreeNode *root) {
      if (root == nullptr) {
         return 0;
      }

      if (root->left == nullptr && root->right == nullptr) {
         return 1;
      }

      int min_depth = INT_MAX;
      if (root->left != nullptr) {
         min_depth = min(minDepth(root->left), min_depth);
      }
      if (root->right != nullptr) {
         min_depth = min(minDepth(root->right), min_depth);
      }

      return min_depth + 1;
   }
};
```





```C++
//广度优先搜索
class Solution2 {
public:
   int minDepth(TreeNode *root) {
      if (root == nullptr) {
         return 0;
      }

      queue<pair<TreeNode *, int> > que;
      que.emplace(root, 1);
      while (!que.empty()) {
         TreeNode *node = que.front().first;
         int depth = que.front().second;
         que.pop();
         if (node->left == nullptr && node->right == nullptr) {
            return depth;
         }
         if (node->left != nullptr) {
            que.emplace(node->left, depth + 1);
         }
         if (node->right != nullptr) {
            que.emplace(node->right, depth + 1);
         }
      }

      return 0;
   }
};
```

