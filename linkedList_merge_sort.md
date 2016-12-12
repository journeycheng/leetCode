## 链表的归并排序


题目描述

Sort a linked list in O(n log n) time using constant space complexity.


解题思路：
- 快慢指针，找出中间的节点；将原链表一分为二
- 归并排序两条有序链表
- 复杂度分析
```
          T(n)         拆分n/2,归并n/2,一共是 n/2 + n/2 =n
        /      \
    T(n/2)     T(n/2)  n/2 * 2 = n
    /   \       /  \
 T(n/4)  T(n/4) ...    n/4 * 4 = n
 
 总共是logn层，故复杂度是O(nlogn)。
 ```
 
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
 public class Solution{
    public ListNode sortList(ListNode head){
        if(head == null || head.next == null){
            return head;
        }
        ListNode head_2 = getMidNode(head).next;
        ListNode tail_1 = head;
        while(tail_1 != head_2){
            tail_1 = tail_1.next;
        }
        tail_1.next = null;
        
        ListNode head1 = sortList(head);
        ListNode head2 = sortList(head_2);
        
        head = mergesort(head1, head2);
        return head;
    }
    // 利用快慢指针，找出中间节点
    public ListNode getMidNode(ListNode head){
        if (head == null || head.next == null){
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    // 合并两个有序链表
    public ListNode mergesort(ListNode head1, ListNode head2){
        if(head1 == null){
            return head2;
        }else if(head2 == null){
            return head1;
        }
        
        ListNode head;
        
        if(head1.val > head2.val){
            head = head2;
            head2 = head2.next;
        }else{
            head = head1;
            head1 = head1.next;
        }
        
        ListNode tail = head;
        
        while(head1 != null && head2 != null){
            if(head1.val > head2.val){
                tail.next = head2;
                tail = tail.next;
                head2 = head2.next;
            }else{
                tail.next = head1;
                tail = tail.next;
                head1 = head1.next;
            }
        }
        while(head1 != null){
            tail.next = head1;
            tail = tail.next;
            head1 = head1.next;
        }
        while(head2 != null){
            tail.next = head2;
            tail = tail.next;
            head2 = head2.next;
        }
        
        return head;
    }
 }
