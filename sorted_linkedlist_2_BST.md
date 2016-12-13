## 将有序链表转换为二叉搜索树（Binary Search Tree）

思路:找到链表的中间节点赋给根节点，对左右子树使用递归；中间节点选择后一个，比如0，1，2，3选择2

```java
public class ListNode{
    int val;
    ListNode next;
    ListNode(int x){
        val = x;
        next = null;
    }
}
```

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
public TreeNode sortedListToBST(ListNode head){
    if (head == null){
        return null;
    }
    if (head.next == null){
        return new TreeNode(head.val);
    }
    // mid和end的开始节点相同
    ListNode mid = head;
    ListNode end = head;
    ListNode premid = null;
    
    while(end != null && end.next != null){
        premid = mid;
        mid = mid.next;
        end = end.next.next;
    }
    
    premid.next = null;
    TreeNode root = new TreeNode(mid.val);
    root.left = sortedListToBST(head);
    root.right = sortedListToBST(mid.next);
    
    return root;
}
```
