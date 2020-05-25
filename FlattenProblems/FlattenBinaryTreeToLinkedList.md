```java

    public void flatten(TreeNode root) {
        flattenDFS(root);
    }
    
    
    public TreeNode flattenDFS(TreeNode root) {
        if (root == null) return null;
        TreeNode curr = root;
        
        TreeNode left = flattenDFS(curr.left);
        TreeNode right = flattenDFS(curr.right);
        
        curr.right = left;
        while (curr.right != null) 
            curr = curr.right;     
        
        
        curr.right = right;
        root.left = null;
        
        return root;   
    } 

```