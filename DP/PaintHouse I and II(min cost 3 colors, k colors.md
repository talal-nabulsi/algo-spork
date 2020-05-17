# Paint House I

```java

    if(costs.length==0) return 0;
    int lastR = costs[0][0];
    int lastG = costs[0][1];
    int lastB = costs[0][2];
    for(int i=1; i<costs.length; i++){
        int curR = Math.min(lastG,lastB)+costs[i][0];
        int curG = Math.min(lastR,lastB)+costs[i][1];
        int curB = Math.min(lastR,lastG)+costs[i][2];
        lastR = curR;
        lastG = curG;
        lastB = curB;
    }
    return Math.min(Math.min(lastR,lastG),lastB);

```


Another solution Using input array

```java


public int minCost(int[][] costs) {
    if(costs==null||costs.length==0){
        return 0;
    }
    for(int i=1; i<costs.length; i++){
        costs[i][0] += Math.min(costs[i-1][1],costs[i-1][2]);
        costs[i][1] += Math.min(costs[i-1][0],costs[i-1][2]);
        costs[i][2] += Math.min(costs[i-1][1],costs[i-1][0]);
    }
    int n = costs.length-1;
    return Math.min(Math.min(costs[n][0], costs[n][1]), costs[n][2]);
}

```




# Paint House II


## Recursive Implementation (Iterative is by far optimal so check that)

```java

class Solution {

    private int n;
    private int k;
    private int[][] costs;
    private Map<String, Integer> memo;

    public int minCostII(int[][] costs) {
        if (costs.length == 0) return 0;
        this.k = costs[0].length;
        this.n = costs.length;
        this.costs = costs;
        this.memo = new HashMap<>();
        int minCost = Integer.MAX_VALUE;
        for (int color = 0; color < k; color++) {
            minCost = Math.min(minCost, memoSolve(0, color));
        }
        return minCost;
    }

    private int memoSolve(int houseNumber, int color) {

        // Base case: There are no more houses after this one.
        if (houseNumber == n - 1) {
            return costs[houseNumber][color];
        }

        // Memoization lookup case: Have we already solved this subproblem?
        if (memo.containsKey(getKey(houseNumber, color))) {
            return memo.get(getKey(houseNumber, color));
        }

        // Recursive case: Determine the minimum cost for the remainder.
        int minRemainingCost = Integer.MAX_VALUE;
        for (int nextColor = 0; nextColor < k; nextColor++) {
            if (color == nextColor) continue;
            int currentRemainingCost = memoSolve(houseNumber + 1, nextColor);
            minRemainingCost = Math.min(currentRemainingCost, minRemainingCost);
        }
        int totalCost = costs[houseNumber][color] + minRemainingCost;
        memo.put(getKey(houseNumber, color), totalCost);
        return totalCost;
    }

    // Convert a house number and color into a simple string key for the memo.
    private String getKey(int n, int color) {
        return String.valueOf(n) + " " + String.valueOf(color);
    }
}
```


> Key Trick for each row you only have to know the two previous minimums

> Cause if one color is the same you just use the other min color, you dont need k other mins from the previous row.

```java

  // Note: This is an optimized version code wise
  // Algo isnt' that hard been might be difficult to rmeember details 
  public int minCostII(int[][] costs) {
        // Actually a pretty easy problem!
        // You only have to find the two smallest from previous row just in case the smallest is same color!
        // start with mins = 0;
        int min1 = 0, min2 = 0, mIndex = -1;

        // Iterate through houses
        for (int i = 0; i < costs.length; i++) {
            
            int m1 = Integer.MAX_VALUE, m2 = Integer.MAX_VALUE, currMinIdx = -1;

            for (int k = 0; k < costs[0].length; k++) {
                
                int cost = costs[i][k] + (k != mIndex ? min1 : min2);

                if (cost < m1)  {
                    // cost < m1 < m2
                    m2 = m1; m1 = cost; 
                    currMinIdx = k; 
                } else if (cost < m2) {
                    // m1 < cost < m2
                    m2 = cost;
                }   
            }

            // m1 and m2 are the curr mins!
            min1 = m1; min2 = m2; mIndex = idx1;
        }
      
        return min1;
    }
```