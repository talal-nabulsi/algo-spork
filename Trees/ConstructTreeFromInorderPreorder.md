

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