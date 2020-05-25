
# 209. Minimum Size Subarray Sum

```java

    public int minSubArrayLen(int s, int[] nums) {  
        int i = 0, j = 0, sum = 0;
        int min = Integer.MAX_VALUE;
        
        while (j < nums.length) { 
            
            sum += nums[j];
                        
            while (sum >= s) {
                min = Math.min(min, j - i + 1);
                sum -= nums[i];
                i++;
            }
            
            j++;
        }
        
        return min == Integer.MAX_VALUE ? 0 : min;     
    }

```


# 862. Shortest Subarray with Sum at Least K

SAME PROBLEM, BUT NOW WITH NEGATIVES (Monotonic Queue problem)