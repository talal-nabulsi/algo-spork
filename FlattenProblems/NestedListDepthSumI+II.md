
# Nested List Depth Sum


```java

    public int depthSum(List<NestedInteger> nestedList) {
        return depthSum(nestedList, 1); 
    }
    
    public int depthSum(List<NestedInteger> nestedList, int level) {
        int sum = 0;
        
        for (NestedInteger nested : nestedList) {
            if (nested.isInteger()) 
                sum += nested.getInteger() * level;
            else 
                sum += depthSum(nested.getList(), level + 1); 
        }
        
        return sum;  
    }
```

II: Literally the same as I but inverted so get the height first

```java


    public int depthSumInverse(List<NestedInteger> nestedList) {
        if(nestedList == null || nestedList.size() == 0) return 0;
        int height = height(nestedList);
        return dfs(nestedList, height);
    }
    
    public int dfs(List<NestedInteger> nestedList, int level) {
        int sum = 0;
        for(NestedInteger n : nestedList) {
            if (n.isInteger()) sum += level * n.getInteger();
            else sum += dfs(n.getList(), level - 1);
        }
        return sum;
    }
    
    
     private int height(List<NestedInteger> l) {
        if(l.size() == 0) return 0;
        int max = 0;
        for(NestedInteger n : l) {
            if(n.isInteger()) max = Math.max(max, 1);
            else max = Math.max(max, height(n.getList()) + 1);
        }
         
        return max;
    }


```