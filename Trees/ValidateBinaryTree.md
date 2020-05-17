# Validate Binary Tree


```java

     public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        TreeNode pre = null;
        
        while (root != null || !s.isEmpty()) {
 
            while (root != null) {
                s.push(root);
                root = root.left;
            }
            
            root = s.pop();
            
            if (pre != null && root.val <= pre.val) return false;
            pre = root;

            root = root.right;   
        }
        
        return true;  
    }
```