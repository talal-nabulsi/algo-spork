

# Remove nth node from end of list

Easy problem. Just advance fast pointer n steps.
Then advance both slow and fast pointers until fast.next == null

```java

   public ListNode removeNthFromEnd(ListNode head, int n) {
        
        ListNode fast = head;
        ListNode slow = head;
        
        while (n > 0) {
            fast = fast.next;
            n--;
        }
        
        if (fast == null) return head.next;
        
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        
        slow.next = slow.next.next;
        return head; 
    }
```