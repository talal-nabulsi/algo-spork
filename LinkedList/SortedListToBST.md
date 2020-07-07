

```java

    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        // Remember to handle the 1 case!
        if (head.next == null) return new TreeNode(head.val);
        ListNode middle = findMiddle(head);
        TreeNode node = new TreeNode(middle.val);
        node.left = sortedListToBST(head);
        node.right = sortedListToBST(middle.next);
        return node;
    }
    
    
    public ListNode findMiddle(ListNode head) {
        // Pre slow is to cut the list into two
        ListNode slow = head;
        ListNode fast = head;
        ListNode preSlow= new ListNode(0);
        preSlow.next = slow;
        
        while (fast != null && fast.next != null) {
            preSlow = preSlow.next;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        preSlow.next = null; // cut list into two parts
        return slow;   
    }
```

