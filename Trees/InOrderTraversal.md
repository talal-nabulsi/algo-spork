
# Inorder Iterative travsal

```java

     public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        
        while (root != null || !s.isEmpty()) {
            while (root != null) {
                s.push(root);
                root = root.left;
            }
            
            // Process
            root = s.pop();    

            // Go RIght        
            root = root.right; 
        }
        
        return true;
        
        
    }
```