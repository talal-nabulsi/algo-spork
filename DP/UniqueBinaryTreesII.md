

GENERATE ALL TREES

> Pretty weirdish solution
> Supposedly opimizable with more DP for left side but probably dont worry about that

```java


public class Solution {
     public List<TreeNode> generateTrees(int n) {
         
         if (n == 0) return new ArrayList<TreeNode>();
         
     return generateTrees(1,n);
 }

public List<TreeNode> generateTrees(int start,int end){             
    List<TreeNode> trees = new ArrayList<TreeNode>();
    if(start>end){  trees.add(null); return trees;}

    for(int rootValue=start;rootValue<=end;rootValue++){
        List<TreeNode> leftSubTrees=generateTrees(start,rootValue-1);
        List<TreeNode> rightSubTrees=generateTrees(rootValue+1,end);

        for(TreeNode leftSubTree:leftSubTrees){
            for(TreeNode rightSubTree:rightSubTrees){
                TreeNode root=new TreeNode(rootValue);
                root.left=leftSubTree;
                root.right=rightSubTree;
                trees.add(root);
            }
        }
    }
    return trees;
}

```