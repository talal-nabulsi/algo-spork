

> Straight forward algorithm

1. First on preorder list is the root
2. Find the root in the inorder array, call it `i`
3. You can use that to figure out the size

```java

   public TreeNode buildTree(int[] preorder, int[] inorder) {
        int preStart = 0;
        int preEnd = preorder.length - 1;
        
        int inStart = 0;
        int inEnd = inorder.length - 1;
        
        return build(preorder, inorder, preStart, preEnd, inStart, inEnd);     
    }
    
    public TreeNode build(int[] preorder, int[] inorder, int preStart, int preEnd, int inStart, int inEnd) {
            // You can test it out, it will indeed terminate, don't even need the other inStart/inEnd case
            if (preStart > preEnd) return null;
            
            int val = preorder[preStart];
            TreeNode curr = new TreeNode(val);
            
            // Minor optimization, you can use hashmap to store indices (Havent done here!)
            int i = inStart;
            for (; i <= inEnd; i++) 
                if (inorder[i] == val) 
                    break;
            
            // size of left side
            int size = i - inStart;
            
            curr.left = build(preorder, inorder, preStart + 1, preStart + size, inStart, i - 1);
            curr.right = build(preorder, inorder, preStart + size + 1, preEnd, i + 1, inEnd);
        
            return curr; 
    }
```


# Varation: Inorder/Postorder

```java
     public TreeNode buildTree(int[] inorder, int[] postorder) {
        return build( 0, inorder.length - 1, inorder, 0, postorder.length - 1, postorder );
    }
    
    private TreeNode build( int inStart, int inEnd, int[] inorder, int postStart, int postEnd, int[] postorder ) {
        if ( inStart > inEnd || postStart > postEnd )   return null;
        
        int rootVal = postorder[postEnd];
        TreeNode root = new TreeNode(rootVal);
        // search root in in-order
        int inRootIndex = 0;
        for ( int i = 0; i < inorder.length; i++ ) {
            if ( inorder[i] == rootVal ) {
                inRootIndex = i;
                break;
            }
        }

        int leftLen = inRootIndex - inStart;
        root.left = build( inStart, inRootIndex - 1, inorder, postStart, postStart + leftLen - 1, postorder );
        root.right = build( inRootIndex + 1, inEnd, inorder, postStart + leftLen, postEnd - 1, postorder );
        return root;
    }
```
