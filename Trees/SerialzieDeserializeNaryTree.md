```java

class Codec {

    // Encodes a tree to a single string.
    public String serialize(Node root) {
        if (root == null)return ",";

        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }
    
    public void serialize(Node root, StringBuilder sb) {
        sb.append(root.val);
        sb.append(',');
        sb.append(root.children.size());
        sb.append(',');
        
        for (Node child : root.children) 
            serialize(child, sb);
    }

    // Decodes your encoded data to tree.
    public Node deserialize(String data) {
        Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserialize(q);
    }
    
    public Node deserialize(Queue<String> q) {
        if (q.isEmpty()) return null;
        
        int val = Integer.valueOf(q.poll());
        int numChildren = Integer.valueOf(q.poll());
        
        Node curr = new Node(val, new ArrayList<>());
        
        for (int i = 0; i < numChildren; i++) 
            curr.children.add(deserialize(q));
        
        return curr;    
    }
    
    
}
```