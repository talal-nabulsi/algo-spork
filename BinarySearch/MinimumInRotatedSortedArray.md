

# Minimum in Rotated Sorted Array



## Both solutions are good, almost identical, first one is my solution I came up with after hours, but I think it's easy to remember

Annoying problem but has helped me fully understand binary search and the variations


```java

    // This problem is quite annoying with all the binary search index edge cases

    // This is my amazing solution I came up with myself after MUCH DELIBERATION
    // Features: Mid check
    // Normal searching
    public int findMin(int[] nums) {
        
        int low = 0, high = nums.length - 1;
        
        while (low <= high) {
            int mid = (low + high)/2;

            // Check  mid and mid + 1 or mid - 1 to see if we can terminate binary search
            if (mid > 0 && nums[mid] < nums[mid - 1]) 
                return nums[mid];
            if (mid < nums.length - 1 && nums[mid + 1] < nums[mid]) 
                return nums[mid + 1];
        
            if (nums[mid] > nums[high]) // right unsorted, def not mid
                low = mid + 1;
            else if (nums[low] > nums[mid]) // left unsorted, 
                high = mid - 1;
            else return nums[low]; // Both parts of array are sorted (or its size 1), nums[low] is answer (DONT FORGET THIS CASE)  
        }
        
        return -1;    
    }

```




# shorter solution, not as clear, but gives some insight

```java

    
    // Tip to understand left < right. This means that one element will be left in the array at the end // Makes sense for this problem because theres no such thing as an invalid answer where we return -1

    // This is my solution I came up with myself after MUCH DELIBERATION
    // I got the high = mid edge case wrong, this is becuase the lowest could be mid stil
    // like if low and mid are right next to each other: example [3,1,2]
    public int findMin(int[] nums) {
        
        int low = 0, high = nums.length - 1;
        
        while (low < high) {
            int mid = (low + high)/2;
            
            if (nums[mid] > nums[high]) // right unsorted, def not mid
                low = mid + 1;
            else if (nums[low] > nums[mid]) // left unsorted, could be mid (so dont do mid - 1)
                high = mid;
            else return nums[low]; // Both parts of array are sorted, nums[low] is answer!    
        }
        
        return nums[low];
        
    }
```




