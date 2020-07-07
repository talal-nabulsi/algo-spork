

Linked List recursive problem

Top solution from the discussion


```java

public Node flatten(Node head) {
        Node p = head; 
        // Traverse the list
        while (p != null) {
            if (p.child != null) {
                Node right = p.next; 
                
                //Process child
                p.next = flatten(p.child);
                p.next.prev = p;
                p.child = null; 
                         
                while (p.next != null)
                    p = p.next;
                
                //Reconnect next 
                if (right != null) { 
                    p.next = right;
                    p.next.prev = p; 
                }
            }
            p = p.next;
        }
        return head; 
    }
```


Leetcode article solution. It makes sense but is a bit convultued. I reccomend the first soluiton


```java

  public Node flatten(Node head) {
    if (head == null) return head;
    // pseudo head to ensure the `prev` pointer is never none
    Node pseudoHead = new Node(0, null, head, null);

    flattenDFS(pseudoHead, head);

    // detach the pseudo head from the real head
    pseudoHead.next.prev = null;
    return pseudoHead.next;
  }
  /* return the tail of the flatten list */
  public Node flattenDFS(Node prev, Node curr) {
    if (curr == null) return prev;
    curr.prev = prev;
    prev.next = curr;

    // the curr.next would be tempered in the recursive function
    Node tempNext = curr.next;

    Node tail = flattenDFS(curr, curr.child);
    curr.child = null;

    return flattenDFS(tail, tempNext);
  }
``