
# The Index-Hashmap-Sum max subarray paradigm
## Difficulty:easy

This problem usually invovles finding a maximum subarray with some type of subarray

Key Steps to remember:

1. Insert (0, -1) into map at the beginning
2. Only insert first occurrence of sum into map! (Because you want to maximize array sizef)

## Examples

# 325. Maximum Size Subarray Sum Equals k

``` java
      // Max subarray of length k
      // Use pre sum!! Can be done in O(n)
      // Remember only put if absent because we want longest array
      public int maxSubArrayLen(int[] nums, int k) {
        
        int sum = 0;
        Map<Integer, Integer> preSum = new HashMap<>();
        int max = 0;
        
        for (int i = 0; i < nums.length; i++) {
            
            sum += nums[i];
            
            // Can also do map.put(0, -1)
            if (sum == k) {
               max = i + 1;
            } else if (preSum.containsKey(sum - k)) {
               max = Math.max(max, i - preSum.get(sum - k));
            }
                
            preSum.putIfAbsent(sum, i);  
        }
        
        return max;
        
    }
```

# Max Subarray sum less than k
Given an array, find the maximum sum of subarray close to k but not larger than k.

```java

public int getLargestSumCloseToK(int[] arr, int k){
    int sum=0;
    TreeSet<Integer> set = new TreeSet<Integer>();
    int result=Integer.MIN_VALUE;
    set.add(0);
 
    for(int i=0; i<arr.length; i++){
        sum += arr[i];
 
        int ceiling = set.ceiling(sum-k);
        if(ceiling!=null) result = Math.max(result, sum-ceiling);        
        
 
        set.add(sum);
    }
 
    return result;
}


```


# Leetcode 523: Check if subarray that sums up to multiple of K
Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to a multiple of k, that is, sums up to n*k where n is also an integer.


```java

    // Contigious subarray sum
    // Mathhy time problem, LC 523
    // Easy once you know solution, basically keep  track of sum % k
    // If you run into a sum
    public boolean checkSubarraySum(int[] nums, int k) {
        int sum = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1); // Dont forget this!, you can also just check is sum %=k = 0
        ```
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];

            if (k != 0) sum %= k;
            if (map.containsKey(sum)) {
                if (i - map.get(sum) >= 2) return true; // Just Make sure subarray size is greater than or equal to 2
            } else {
                map.put(sum, i);
            }
        }  
        return false;
    }

```


# Leetcode 525 Subarray sums up to multiple of k
Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to a multiple of k, that is, sums up to n*k where n is also an integer.

```java

// Contigious Array, Leetcode 525
// Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.
class Solution {
    // Problem of the Index-Hashmap Type
    // Remember to put in (0, -1) for these types of problems
  public int findMaxLength(int[] nums) {        
        int max = 0;
        int count = 0;
        
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        
        for (int i = 0; i < nums.length; i++) {
            
            count += nums[i] == 1 ? 1 : -1;
            
            if (map.containsKey(count)) {
                max = Math.max(max, i - map.get(count));
            } else { // must be else cause we want the smallest possible index
                map.put(count, i);
            }    
        }
        return max; 
    }
}

```
