
BINARY SEARCH, easy but tricky cause it doesn't look like binary search


```java
    // Doesn't look like it, but EASY binary search
   public int minDays(int[] A, int m, int k) {
        int n = A.length, left = 1, right = (int)1e9;
        if (m * k > n) return -1;
       
        while (left < right) {
            int mid = (left + right) / 2;
            int bouq = countBouq(A, mid, k);
            
            if (bouq < m) 
                left = mid + 1;
            else 
                right = mid; 
        }
       
        return left;
    }
    
    // Helper func to calculate number of bouquets for each trial
    public int countBouq(int[]A, int days, int k) {
        int flow = 0, bouq = 0;
        for (int j = 0; j < A.length; ++j) {
            if (A[j] > days) {
                flow = 0;
            } else if (++flow >= k) {
                bouq++;
                flow = 0;
            } 
        }
        return bouq;
    }
```