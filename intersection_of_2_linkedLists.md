## 160. Intersection of Two Linked Lists

- O(n+m) time, O(1) memory
```python
def getIntersectionNode(headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
    if not headA or not headB:
        return None
        
    startA = headA
    startB = headB
    while startA != startB:
        if not startA:
            startA = headB
        else:
            startA = startA.next
            
        if not startB:
            startB = headA
        else:
            startB = startB.next
    return startA
```
