## 二叉树的根节点到叶子节点的最少层数

- 题目描述

Given a binary tree, find its minimum depth.The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


```java
public class TreeNode{
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x){
        val = x;
    }
}
```


```java
public class Solution{
    public int run(TreeNode root){
        if(root == null){
            return 0;
        }else if(root.left == null && root.right == null){
            return 1;
        }else if(root.left == null && root.right != null){
            return 1 + run(root.right);
        }else if(root.left != null && root.right == null){
            return 1 + run(root.left);
        }else{
            int left_depth = 0;
            int right_depth = 0;
            left_depth = run(root.left);
            left_depth = run(root.right);
            
            if(left_depth > right_depth){
                return 1 + right_depth;
            }else{
                return 1 + left_depth;
            }
        }
    }
}
```
