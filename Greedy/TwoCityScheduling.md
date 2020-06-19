
Good greedy problem
Tricky but easy to understand

```


    // GREEDY
    // Basically you can track all the costs as an oppurtunity cost
    // One way to look at it: Send everyone to city A, and and then calculate the difference in cost gained by switching to B for each
    // The ones with the biggest "refunds" are the ones 
    public int twoCitySchedCost(int[][] costs) {
        int N = costs.length/2;
        int[] refund = new int[N * 2];
        int minCost = 0, index = 0;
        
        // Add up cost of sending to A
        for(int[] cost : costs)
            minCost += cost[0]; 
        
        
        // Calculate "refund" gained by switching to B (cost(B) - cost(A))
        for(int[] cost : costs)
            refund[index++] = cost[1] - cost[0]; // generate refund 
        
        Arrays.sort(refund);
        
        // Switch first N cities to B and recalculate 
        for(int i = 0; i < N; i++)
            minCost += refund[i]; // note that refund could be negative or positive
        
        return minCost;
    }
```