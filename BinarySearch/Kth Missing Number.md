```java


// GREAT BINARY SEARCH PROBLEM

// KEY: Find the largest element that has missing(idx) < k
// SO IT MUST BE IN THE INTERVAL OF THAT INDEX and the next ELEMENT
// Then add k - missing(idx) to find the missing number (this is easy)

class Solution {
  // Return how many numbers are missing until nums[idx]
  int missing(int idx, int[] nums) {
    return nums[idx] - nums[0] - idx;
  }

  public int missingElement(int[] nums, int k) {
    int n = nums.length;
    
    // EDGE CASE here if k is larger than end of the array
    if (k > missing(n - 1, nums))
      return nums[n - 1] + k - missing(n - 1, nums);
      

    int left = 0, right = n - 1, pivot, ans = -1;

    while (left <= right) {
        
      pivot = left + (right - left) / 2;
        
      if (missing(pivot, nums) < k) {
          ans = pivot;
          left = pivot + 1;
      }  else {
          right = pivot - 1;
      }
    }

    // kth missing number is greater than nums[idx - 1]
    // and less than nums[idx]
    return nums[ans] + k - missing(left - 1, nums);
  }
}

```