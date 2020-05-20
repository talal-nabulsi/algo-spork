# Serialize and Deserialize Binary Tree


```java

public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }
    
    public void serialize(TreeNode node, StringBuilder sb) {
        if (node == null)  {
            sb.append("X,");
        } else {
            sb.append(node.val + ",");
            serialize(node.left, sb);
            serialize(node.right, sb);
        }    
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] nodeList = data.split(",");
        return deserialize(nodeList, new int[1]);
    }
    
    // Can also use a queue instead of index array of size 1
    public TreeNode deserialize(String[] nodeList, int[] index) {
        String s = nodeList[index[0]++];
        if (s.equals("X")) return null;
        TreeNode node = new TreeNode(Integer.valueOf(s));
        node.left = deserialize(nodeList, index);
        node.right = deserialize(nodeList, index);
        return node;  
    }
}

```


# Serialize and Deserialize Binary Search Tree (no need for null delimiter)


```java

public class Codec {
    // Serialize BINARY SEARCH TREE (BST)
    // SAME AS SERIALIZE BINARY TREE BUT YOU CAN USE UPPER/LOWER to avoid storing null delimiters
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }
    
    public void serialize(TreeNode root, StringBuilder sb) {
        if (root == null) return;
        sb.append(root.val).append(",");
        serialize(root.left, sb);
        serialize(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.isEmpty()) return null;
        Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserialize(q, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
    
    public TreeNode deserialize(Queue<String> q, int lower, int upper) {
        if (q.isEmpty()) return null;
        String s = q.peek();
        int val = Integer.parseInt(s);
        if (val < lower || val > upper) return null;
        
        q.poll();
        TreeNode root = new TreeNode(val);
        root.left = deserialize(q, lower, val);
        root.right = deserialize(q, val, upper);
        return root;
    }
}

```