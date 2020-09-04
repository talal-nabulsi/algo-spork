
```

    // BINARY SEARCH MATH SOLUTION
    public int arrangeCoins(int n) {
        
        long low = 0, high = n;
        long k, coins, res = -1;
        
        while (low <= high) {
            k = low + (high - low)/2;
            coins = k * (k + 1)/2;
            
            if (coins <= n) {
                res = k;
                low = k + 1;
            } else {
                high = k - 1;
            }
        }
        
        return (int) res;  
    }
```