# I



```java

public class Solution {
    public int search(int[] nums, int target) {
        
        int n = nums.length;
        int start = 0;
        int end = n - 1;
        
        while (start <= end) {
            
            int mid = start + (end - start)/2;
            
            if (nums[mid] == target) return mid;
            
            // left side is sorted
            if (nums[start] <= nums[mid]) {
                
                // if target is on sorted side
                if (target < nums[mid] && target >= nums[start]) 
                    end = mid - 1;
                else 
                    start = mid + 1;
                
            // right side is sorted   
            } else if (nums[mid] <= nums[end]) {

                // If target is in sorted side
                if (target > nums[mid] && target <= nums[end]) 
                    start = mid + 1;
                else 
                    end = mid -1; 
            }  
        }
        
        return - 1;

    }
}

```

# II

> Same thing but with dupes. Pretty easy, there is just one case where we run into a roadblock and thats when **nums[left] == nums[mid] == nums[right]**
In that case we should just **left++ and right++**


> Two ways to do this both identical in function. First method a bit more clean where we preemptively check left == mid == right

```java
    bool search(vector<int>& nums, int target) {
        int left = 0, right =  nums.size()-1, mid;
        
        while(left<=right)
        {
            mid = (left + right) >> 1;
            if(nums[mid] == target) return true;

            // the only difference from the first one, trickly case, just updat left and right
            if( (nums[left] == nums[mid]) && (nums[right] == nums[mid]) ) {++left; --right;}

            else if(nums[left] <= nums[mid])
            {
                if( (nums[left]<=target) && (nums[mid] > target) ) right = mid-1;
                else left = mid + 1; 
            }
            else
            {
                if((nums[mid] < target) &&  (nums[right] >= target) ) left = mid+1;
                else right = mid-1;
            }
        }
        return false;
    }
```



```java

    public boolean search(int[] nums, int target) {
        
        int n = nums.length;
        int start = 0;
        int end = n - 1;
        
        while (start <= end) {
            
            int mid = start + (end - start)/2;
            if (nums[mid] == target) return true;
            
            //If we know for sure left side is sorted or right side is unsorted
            if (nums[start] < nums[mid] || nums[mid] > nums[end] ) {
                
                if (target < nums[mid] && target >= nums[start]) 
                    end = mid - 1;
                else 
                    start = mid + 1;
                
            //If we know for sure right side is sorted or left side is unsorted
            } else if (nums[mid] <  nums[end] || nums[mid] < nums[start]) {
    
                if (target > nums[mid] && target <= nums[end]) 
                    start = mid + 1;
                else 
                    end = mid -1;
                
            //If we get here, that means nums[start] == nums[mid] == nums[end], then shifting out
            //any of the two sides won't change the result but can help remove duplicate from
            //consideration, here we just use end-- but left++ works too
            } else {
                start++;
                end--;
            }  
    }
        return false;
    }
```