
# Paint Fence

> Fancy Equation
> Easy when you understand and a great question forsure
        
> Explanation
numWays(i) = numWaysDiff(i) + numWaysSame(i)
        
> Number of ways diff to last
numWaysDiff(i) is easy: numWays(i - 1) * k - 1
        
> Number of ways same as last
(TRICKY PART, ensures you don't have 3 adjacent)
numWaysSame(i) = numWaysDiff(i - 1) = numWays(i - 2) * k -1
           
> NOW ADD THEM TOGETHER 
numWays(i - 1) * (k - 1) + numWays(i - 2) * (k -1)
And simiplify that, easy enough


```java

    public int numWays(int n, int k) {
    
        
        if (n == 0) return 0;
        if (n == 1) return k;
        if (n == 2) return k*k;
        
        int pre2 = k;
        int pre1 = k * k;
        int curr = 0;
        
        for (int i = 3; i <= n; i++) {
            curr = (pre2 + pre1) * (k - 1);
            pre2 = pre1;
            pre1 = curr;
        }        
        return curr;  
    }

```