## 合并有序链表

递归
```java
public static ListNode merge(ListNode head1, ListNode head2){
    if(head1 == null){
        return head2;
    }else if(head2 == null){
        return head1;
    }
    
    ListNode mergehead;
    if(head1.val < head2.val){
        mergehead = head1;
        mergehead.next = merge(head1.next, head2);
    }else{
        mergehead = head2;
        mergehead.next = merge(head1, head2.next);
    }
    
    return mergehead;
}
```

非递归
```java
public static ListNode merge(ListNode head1, ListNode head2){
    if(head1 == null){
        return head2;
    }else if(head2 == null){
        return head1;
    }
    
    ListNode mergehead;
    if(head1.val < head2.val){
        mergehead = head1;
        head1 = head1.next;
    }else{
        mergehead = head2;
        head2 = head2.next;
    }
    
    while(head1 != null && head2 != null){
        if(head1.val < head2.val){
            mergehead.next = head1;
            mergehead = mergehead.next;
            head1 = head1.next;
        }else{
            mergehead.next = head2;
            mergehead = mergehead.next;
            head2 = head2.next;
        }
    }
    while(hea1 != null){
        mergehead.next = head1;
        mergehead = mergehead.next;
        head1 = head1.next;
    }
    while(hea2 != null){
        mergehead.next = head2;
        mergehead = mergehead.next;
        head2 = head1.next;
    }
    
    return mergehead;
}
```
