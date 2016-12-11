## 二叉树的遍历打印


定义BinaryTree结构体

```java
public class BinaryTree{
    int val;
    BinaryTree left;
    BinaryTree right;
    BinaryTree(int x){
        val = x;
    }
}
```


- 先序遍历打印
```java
public class void preOrder(BinaryTree root){
    if (root == null){
        return;
    }
    System.out.println(root.val);
    preOrder(root.left);
    preOrder(root.right);
}
```

- 中序遍历
```java
public class void inOrder(BinaryTree root){
    if(root == null){
        return;
    }
    inOrder(root.left);
    System.out.println(root.val);
    inOrder(root.right);
}
```

- 后序遍历
```java
public class void postOrder(BinaryTree root){
    if(root == null){
        return;
    }
    postOrder(root.left);
    postOrder(root.right);
    System.out.println(root.val);
}
```
