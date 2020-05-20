

# Subset Sum

This is Tushar Roy's 2D solution

```java
    public boolean subsetSum(int input[], int total) {

        boolean T[][] = new boolean[input.length + 1][total + 1];
        for (int i = 0; i <= input.length; i++) 
            T[i][0] = true;
    

        for (int i = 1; i <= input.length; i++) 
            for (int j = 1; j <= total; j++) {
                if (j - input[i - 1] >= 0) 
                    T[i][j] = T[i - 1][j] || T[i - 1][j - input[i - 1]];
                else 
                    T[i][j] = T[i-1][j];
            }
        
        return T[input.length][total];
    }

```



# Partition Equal Subset Sum

Identical to subset sum but with half the sum

```java
    // Classic 0/1 Knapsack problem
    public boolean canPartition(int[] nums) {  
        // Exactly like subset sum but with sum/2
        // Beause if you can make sum/2 then you def have the other subset making sum
        // CAN DO IT in 1 DIMENSION - pretty easy but rememember to go backwards
        // Read first discussion solution for Leetcode 416, its great
        int sum = 0;
        for (int num : nums) 
            sum += num;
        
        // If sum is not divisible by two then return false
        if (sum % 2 == 0)  sum /= 2;
        else return false;
        
        
        boolean[] dp = new boolean[sum + 1];
        dp[0] = true;
        
        // Can do 1
        for (int num : nums) 
            for (int j = sum; j >= num; j--) 
                dp[j] = dp[j] || dp[j - num];   
            
        
        
        return dp[sum];  
    }

```