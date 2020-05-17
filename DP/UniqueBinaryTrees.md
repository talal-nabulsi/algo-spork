# Unique Binary Search Trees

> Easy dp, idea is that for each size you test out a root

> Multiple the size left of root * size right of root

```java
    // Recursive
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = dp[1] = 1;
        return numTrees(n, dp);
    }
    
    // This is the recursive implementation
    public int numTrees(int n, int[] dp) {
        
        if (dp[n] != 0) return dp[n];

        int count = 0;
        
        for (int i = 1; i <= n; i++) 
            count += numTrees(i - 1, dp) * numTrees(n - i, dp);
        
        dp[n] = count;
        return count;  
    }

```



```java

// DP Method
 public int numTrees(int n) {
    int [] dp = new int[n+1];
    dp[0]= 1;
    dp[1] = 1;
    for(int level = 2; level <=n; level++)
        for(int root = 1; root<=level; root++)
            dp[level] += dp[level-root]*dp[root-1];
    return dp[n];
}


```