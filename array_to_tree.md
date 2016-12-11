## 利用数组构建二叉树

```java
public class BinaryTree{
    int val;
    BinaryTree left;
    BinaryTree right;
    BinaryTree(int x){
        val = x;
        left = null;
        right = null;
    }
}
```

- ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构
- 对于随机访问get和set，ArrayList优于LinkedList，因为ArrayList是随机定位的，而LinkedList要移动指针一步步移动到节点处。可以参考数组和链表。

```java
public void createBinaryTree(int[] array){
    nodeList = new LinkedList<BinaryTree>();
    for (int nodeIndex = 0; nodeIndex < array.length; nodeIndex ++){
        nodeList.add(new Node(array[nodeIndex]));
    }
    
    for(int parentIndex = 0; parentIndex < array.length/2 - 1)
}
