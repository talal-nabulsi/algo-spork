

# Count of Subarrays with K Different/Distinct subarrays

Sliding window variation, a bit tricky but easy once you get it.

Since you're trying to find the count, ie ALL SUBARRAYS, not the max or min subarray

Idea is to just shorten the window as long as it doesn't affect k, and count the prefixes


```java


    // Trickier sliding window problem
    // Almost the same as k distinct characters, but now you have to keep track of the prefixes... since you need the count 
    // not the shortest or longest subarray
    // ie. if array is 12123 make sure to count 1212 AND 212
    // See Leetcode discussion for good explanation but the idea is pretty easy
    
    public int subarraysWithKDistinct(int[] nums, int k) {
        int i = 0, j = 0, count = 0, prefix = 0;
        Map<Integer, Integer> map = new HashMap<>();
        
        
        while (j < nums.length) {
            // Incremement j
            map.put(nums[j], map.getOrDefault(nums[j], 0) + 1);
            
            // Move start of window if size is too big, and reset prefixes
            // Does not need to be while because we've already moved the window in the next loop to make sure no dups of the num at i
            if (map.size() > k) {
                map.put(nums[i], map.get(nums[i]) - 1);
                map.remove(nums[i]);
                i++;
                prefix = 0;
            }
            
            // Here is the main trick for this problem: just move i forward if we have more than 1 of the number at 1
            // And count the prefixes because all the prefixes will also be valid subarrays
            while (map.get(nums[i]) > 1) {
                map.put(nums[i], map.get(nums[i]) - 1);
                i++;
                prefix++;
            }
            
            // Valid subarray, add it and all of it's prefixes (All of its prefixes have the same amount of distinct integrs)
            if (map.size() == k) count += prefix + 1;

            j++;
        }   
        return count;   
    }
```