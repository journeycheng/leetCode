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
- 所有测试用例的运行时间：437ms; 占用内存：3638k

## 方法二：
改变链表结构，将节点直接插入到合适的位置。
