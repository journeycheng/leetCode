题目描述：

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:

Given the below binary tree andsum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

return true, as there exist a root-to-leaf path5->4->11->2which sum is 22.

```java
public class TreeNode{
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x){
        val = x;
        left = null;
        right = null;
    }
}
```


```java
public boolean hasPathSum(TreeNode root, int sum){
    if(root == null){
        return false;
    }
    if(root.left == null && root.right == null){
        if(root.val == sum){
            return true;
        }
    }
    
    sum -= root.val;
    if(hasPathSum(root.left, sum) || hasPathSum(root.right, sum)){
        return true;
    }
    
    return false;
}
```
