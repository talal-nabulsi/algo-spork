

 # Coin Change 1

Easy, just remember, coins is the inner loop 

> Objective: min number of coins to get to amount

> Remember to set all in the dp array to max value


```java

    // Live and Breathe, remember the gotchas
    public int coinChange(int[] coins, int amount) {
        // Easy but there are a few gotchas here
        // DP array is the amount + 1
        int[] dp = new int[amount + 1];
    
        for (int i = 1; i < dp.length; i++) 
            dp[i] = Integer.MAX_VALUE; // can also use amount + 1 instead of max value
      
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0) {
                    int diff = i - coin;
                    if (dp[diff] == -1) continue;   
                    dp[i] = Math.min(dp[i], 1 + dp[diff]);
                }
             }
            
            // If we can't find any way set it to -1
            // We can also just keep at max value if we want
            if (dp[i] == Integer.MAX_VALUE) dp[i] = -1;   
        }   
        
        return dp[amount];
    }

```

# Coin Change II


> Objective: Find number of ways to get to amount

> WARNING: TRICKY : use coins in outer loop to prevent duplicates

// Coins must be outer loop otherwise you will duplicate it

Explanation: Imagine you have coins 2 and 5 and amount is 7

// When amount is 2 and the coin value is 5, it would be counted as 1 way.

// When amount is 5 and the coin value is 2, the number of ways become 2.

// 

> DP[i][amount] = num ways without + num ways with

> DP[i][amount] = dp[i - 1][amount] + dp[i][amount - coin]

> Dp[i][amount] = top cell + cell in SAME row at colunm [amount - coin]

> IMPORTANT: you can use 1D DP in the forwards direction because you NEED only the cell directly above and the  value from the SAME row calculate the answer (so you aren't at risk of overwriting values you need in the future)

> This is different from subset sum, where you have to go backwards since you need elements from previus row and don't want to overwrite them!

```java
    
    // It's a classic 0/1 knapsack problem but with weight == value and a twist (WE CAN REUSE ITEMS)
    // Instead of dp[i - 1][j] + dp[i - 1][j - coin] its dp[i - 1][j] + dp[i][j - coin] (same row)
    // Because we can REUSE Items for the second check(including item) we dont go (i - 1) we just check the same row
    // You should definitely memorize this one, its a good trick
    // Because we can reuse items we don't have to go to previous row, and we can do it 1D
    
    // Similar to Combination Sum IV excpet for the fact this one doesn't allow combinations of the same sequence

    
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        
        // Coins must be outer loop otherwise you will duplicate it
        // When amount is 2 and the coin value is 5, it would be counted as 1 way.
        // When amount is 5 and the coin value is 2, the number of ways become 2.
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++)
                dp[i] += dp[i-coin];  
        }
        return dp[amount];
    }


```


