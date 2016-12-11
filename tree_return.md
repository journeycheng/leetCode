## 二叉树的遍历返回

二叉树结构体
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

- 前序
```java
import java.util.*

ArrayList<Integer> result = new ArrayList<Integer>();

public ArrayList<Integer> orderTree(TreeNode root, String searchWay){
    if(searchWay == "preOrder"){
        preorder(node);
    }else if(searchWay == "inOrder"){
        inorder(node);
    }else if(searchWay == "postOrder"){
        postorder(node);
    }

    return result;
}

// 前序
public void preorder(TreeNode root){
    if(root == null){
        return;
    }
    result.add(root.val);
    preorder(root.left);
    preorder(root.right);
}

// 中序
public void inorder(TreeNode root){
    if(root == null){
        return ;
    }
    inorder(root.left);
    result.add(root.val);
    inorder(root.right);
}

// 后序
public void postorder(TreeNode root){
    if(root == null){
        return;
    }
    postorder(root.left);
    postorder(root.right);
    result.add(root.val);
}
```
