# Best time to buy and sell stock I

Trivial, one transaction

```java

    public int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int profit = 0;
        
        for (int price : prices) {
            min = Math.min(price, min);
            profit = Math.max(profit, price - min);  
        }
        
        return profit;
    }
```


# II

Also trivial, unlimited transactions

```java


    public int maxProfit(int[] prices) {
        int prev = prices[0];
        int profit = 0;
        
        for (int price : prices) {
            if (price > prev) profit += (price - prev);
            prev = price;
        }
        return profit;

```

# III 
HARD now 2 transcations

> leftMax[i] and rightMax[i] two array method
> Most classic solution but O(n) space (there is a more optimized solution!)

```java

  public int maxProfit(int[] prices) {
    int length = prices.length;
    if (length <= 1) return 0;

    int leftMin = prices[0];
    int rightMax = prices[length - 1];

    int[] leftProfits = new int[length];
    // pad the right DP array with an additional zero for convenience.
    int[] rightProfits = new int[length + 1];

    // construct the bidirectional DP array
    for (int l = 1; l < length; ++l) {
      leftProfits[l] = Math.max(leftProfits[l - 1], prices[l] - leftMin);
      leftMin = Math.min(leftMin, prices[l]);

      int r = length - 1 - l;
      rightProfits[r] = Math.max(rightProfits[r + 1], rightMax - prices[r]);
      rightMax = Math.max(rightMax, prices[r]);
    }

    int maxProfit = 0;
    for (int i = 0; i < length; ++i) {
      maxProfit = Math.max(maxProfit, leftProfits[i] + rightProfits[i + 1]);
    }
    return maxProfit;

```

## THE BEST SOLUTION FOR TWO TRANSACTIONS!

```java

  public int maxProfit(int[] prices) {
    int t1Cost = Integer.MAX_VALUE, 
        t2Cost = Integer.MAX_VALUE;
    int t1Profit = 0,
        t2Profit = 0;

    for (int price : prices) {
        // the maximum profit if only one transaction is allowed
        t1Cost = Math.min(t1Cost, price);
        t1Profit = Math.max(t1Profit, price - t1Cost);
        // reinvest the gained profit in the second transaction
        t2Cost = Math.min(t2Cost, price - t1Profit);
        t2Profit = Math.max(t2Profit, price - t2Cost);
    }

    return t2Profit;
  }
```


## K transactions




## Best time to buy and sell stock swith cooldown

> Important TIP: if k >= n/2, then you can make maximum number of transactions.

> Pretty hard problem, but very intuitive once you get it.

> There is a very important opimization that cuts it down from O(k * d * d) to O(k * d) where d is days 



```java
// THE OPTMIZED VERSION USING THE MAX_DIFF
// MAX_DIFF is basically the max starting point from (i - 1) transactions
// Its the (profit at that index) - (price at that day)
// Very Intiutive because you don't have to keep recalculating the starting point

    public int maxProfitLinearSpace(int k, int[] prices) {
        if (k == 0 || prices.length == 0) {
            return 0;
        }

        // Use solution from II because same as unlimited transactions!!!
        if (k >= prices.length) return maxProfitII(prices);
        
        int[] T = new int[prices.length];
        int[] prev = new int[prices.length];

        for (int i = 1; i <= k; i++) {
            int maxDiff = -prices[0];
            for (int j = 1; j < prices.length; j++) {
                T[j] = Math.max(T[j - 1], maxDiff + prices[j]);
                maxDiff = Math.max(maxDiff, prev[j] - prices[j]);
            }
            for (int j = 1; j < prices.length; j++) {
                prev[j] = T[j];
            }
        }
        return T[T.length - 1];
    }

```

```java
// The unoptimized version (O(k * d * d )) where we don't save starting points

    /**
     * This is slow method but easier to understand.
     * Time complexity is O(k * number of days ^ 2)
     * T[i][j] = max(T[i][j-1], max(prices[j] - prices[m] + T[i-1][m])) where m is 0...j-1
     */
    public int maxProfitSlowSolution(int prices[], int K) {
        if (K == 0 || prices.length == 0) {
            return 0;
        }
        int T[][] = new int[K+1][prices.length];

        for (int i = 1; i < T.length; i++) {
            for (int j = 1; j < T[0].length; j++) {
                int maxVal = 0;
                for (int m = 0; m < j; m++) 
                    maxVal = Math.max(maxVal, prices[j] - prices[m] + T[i-1][m]);
                T[i][j] = Math.max(T[i][j-1], maxVal);
            }
        }
        printActualSolution(T, prices);
        return T[K][prices.length - 1];
    }




```