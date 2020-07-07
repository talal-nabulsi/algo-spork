# Merge Two Sorted Lists

Both iterative and recursive are clean,

```java

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        
        ListNode dummy = new ListNode(0);
        ListNode curr= dummy;

        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                curr.next = l1;
                curr = curr.next;
                l1 = l1.next;
            } else {
                curr.next = l2;
                curr = curr.next;
                l2  = l2.next;
            }
        }
        
        // No need for while loop, just set it equal to rest of list!!
        if (l1 != null) curr.next = l1;
        if (l2 != null) curr.next = l2;
     
        return dummy.next;   
    }

```


# Recursive Implementation

```java

     public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }

```