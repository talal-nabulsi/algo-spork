

# Inorder Sucessor in BST 

Pretty trivial problem, seecomments

```java

     public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        
        // This part is just an optimization, not that necessary, and only possible when you are given the node
        if (p.right != null) {
            TreeNode sucessor = findMin(p.right);
            return sucessor;
        }
        
        TreeNode successor = null;
        
         // Just iterate until you find the node
         // If you go left then mark that parent as the successor
         // Opposite for PREDECESSOR!!
        while (root != p) {
            if (p.val < root.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        } 
        return successor;
          
    }
    
    public TreeNode findMin(TreeNode root) {
        while (root.left != null) 
            root = root.left;
        return root;    
    }
```