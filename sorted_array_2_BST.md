## 将有序数组转换为二叉搜索树

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
public TreeNode sortedArrayToBST(int[] num){
    if(num == null || num.length == 0){
        return null;
    }
    
    return sortedarraytobst(num, 0 ,num.length-1);
}

public TreeNode sortedarraytobst(int[] num, int start, int end){
    if(start > end){
        return null;
    }
    if(start == end){
        return new TreeNode(num[start]);
    }
    
    int mid = (start + end)/2;
    if((end - start)%2 == 1){
        mid += 1;
    }
    
    TreeNode root = new TreeNode(num[mid]);
    root.left = sortedarraytobst(num, start, mid-1);
    root.right = sortedarraytobst(num, mid+1, end);
    
    return root;
}
```
