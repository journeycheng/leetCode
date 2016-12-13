## 反转链表

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
public static ListNode reverse(ListNode head){
    if(head == null || head.next == null){
        return head;
    }
    Stack<ListNode> tmp = new Stack<ListNode>();
    while(head != null){
        tmp.push(head);
        head = head.next;
    }
    head = tmp.pop();
    tail = head;
    while(!tmp.empty()){
        tail.next = tmp.pop();
        tail = tail.next;
    }
    tail.next = null;
    
    return head;
}
```
