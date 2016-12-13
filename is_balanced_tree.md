## 判断是否是平衡二叉树

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
public boolean isBalanced(TreeNode root){
    if(root == null){
        return true;
    }
    int depth_left = getDepth(root.left);
    int depth_right = getDepth(root.right);
    if(Math.abs(depth_left,depth_right) <= 1){
        if(isBalanced(root.left) && isBalanced(root.right)){
            return true;
        }
    }
    return false;
}

public int getDepth(TreeNode root){
    if(root == null){
        return 0;
    }
    int depth_left = getDepth(root.left);
    int depth_right = getDepth(root.right);
    return depth_left > depth_right ? depth_left+1 : depth_right + 1;
}
```
