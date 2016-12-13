## 判断链表中是否有环

```java
class ListNode{
    int val;
    ListNode next;
    ListNode(int x){
        val = x;
        next = null;
    }
}
```

快慢指针的思路
```java
public boolean hasCycle(ListNode head){
    if(head == null || head.next == null){
        return false;
    }
    ListNode slow = head;
    ListNode fast = head.next;
    
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast){
            return true;
        }
    }
    
    return false;
}
```
