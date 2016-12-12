## 链表的快排

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
public static ListNode sortList(ListNode head){
    quicksort(head, null);
    return head;
}

public static void quicksort(ListNode head, ListNode tail){
    if(head == tail){
        return;
    }
    ListNode p = partition(head, tail);
    quicksort(head, p);
    quicksort(p.next, tail);
}

// 保证low后面high前面的都比key大
public static ListNode partition(ListNode head, ListNode tail){
    int key = head.val;
    ListNode low = head;
    ListNode high = head.next;
    while(high != tail){
        if(high.val < key){
            low = low.next;
            int tmp = low.val;
            low.val = high.val;
            high.val = tmp;
        }
        high = high.next;
    }
    int tmp = low.val;
    low.val = head.val;
    head.val = tmp;
    
    return low;
}
```
