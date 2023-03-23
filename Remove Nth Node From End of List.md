#Problem 
#LinkedLIst

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        current: ListNode = head
        length: int = 0

        while current is not None:
            length += 1
            current = current.next

        # Reset current
        current = head
        if length == 1:
            head = None
        elif length == n:
            return head.next
        else:
            for loc in range(length-n-1):
                current = current.next

            current.next = current.next.next
                
        return head
```   

