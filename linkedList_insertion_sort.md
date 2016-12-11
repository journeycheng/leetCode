## 题目描述
Sort a linked list using insertion sort.

## 方法一：

基于数组的插入排序方法，链表结构不变，交换链表节点的值
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }


        ListNode current = head.next;
        while(current != null){
            ListNode soldier = head;
            while(soldier != current && soldier.val <= current.val){
                soldier = soldier.next;
            }
            int tmp = current.val;
            int tmp1 = soldier.val;
            while(soldier != current){
                tmp1 = soldier.val;
                soldier.val = tmp;
                tmp = tmp1;
                soldier = soldier.next;
            }
            soldier.val = tmp;
            
            current = current.next;

        }
        return head;
    }
}
```

- 将整个链表分为已排好序和未排好序的两部分
- current是未排好序部分的起始点
- soldier节点在已排好序的部分从头节点开始遍历，找到需要和current节点交换值的节点，并将该节点的值依次赋给下一个节点。
- 链表只能从头节点开始，和数组的插入排序遍历方向相反
- 所有测试用例的运行时间：503ms; 占用内存：3638k

## 方法二：
改变链表结构，将节点直接插入到合适的位置。
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode insertionSortList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode current = head.next;
        ListNode tmp = current;
        
        head.next = null;
        ListNode soldier = head;
        
        while(current != null){
            
            soldier = head;
            
            if (current.val <= head.val){
                tmp = tmp.next;
                current.next = head;
                head = current;
                
            }else{
                
                while(soldier!= null && soldier.next != null && soldier.val < current.val && soldier.next.val < current.val){
                    soldier = soldier.next;
                }
                if(soldier != null && soldier.next != null){
                    tmp = tmp.next;
                    current.next = soldier.next;
                	soldier.next = current;
                }else if(soldier != null && soldier.next == null){
                    tmp = tmp.next;
                    current.next = null;
                    soldier.next = current;
                }
            }
            
            current = tmp;    
        }
        return head;
    }
}
```
- 将原始链表分成已排好序和未排好序的不相连的两条链表
- 和前面的方法相比，优点：不需要每次都遍历整个链表，没有数据的交换
- 运行时间：432ms; 占用内存：3638k
