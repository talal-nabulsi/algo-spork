
# Random Pick With Weights

```java

// Extremeley easy problem, see solution for more info but heres a summary:
// Basically use preSum array and binary search of the keep searching varation
// 1. Get prefix sum array of weights
// 2. Generate random index from sum of all weights
// 3. Search for smallest index that is less than the random
class Solution {

    Random random;
    int[] wSums;
    
    public Solution(int[] w) {
        this.random = new Random();
        for(int i=1; i<w.length; ++i)
            w[i] += w[i-1];
        
        this.wSums = w;
    }
    
    public int pickIndex() {
        int len = wSums.length;
        int idx = random.nextInt(wSums[len-1]) + 1; // Random index from sum of all weights combined
        int left = 0, right = len - 1;
        int ans = 0;
        // search position 
        while(left <= right){
            int mid = left + (right-left)/2;
            if(wSums[mid] == idx)
                return mid;
            else if (idx > wSums[mid])
                left = mid + 1;
            else {
               // If less, set ans and keep searching left
               ans = mid;
               right = mid - 1;
            }
        }
        return ans;
    }
}
```