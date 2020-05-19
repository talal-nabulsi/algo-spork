
# Lowest Common Ancestor (non BST)

```java

      // Not a BST, so we must search both sides
      public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        
        if (root == null) return null;
        if (root == p || root == q) return root;
    
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left != null && right != null) 
            return root;
          
        return left != null ? left : right;
    }
```


# BST makes it even simpler

> If nodes are in different subtrees then that node is the LCA


```java

   public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        else if(root.val < p.val && root.val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        else
            return root;
    }
```