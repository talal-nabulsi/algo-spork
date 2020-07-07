

Easy, put each number in it's index (-1 to handle zero)
Just don't forget dup check to prevent infinite loop.

```java

 public int firstMissingPositive(int[] nums) {
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] <= 0 || nums[i] == i + 1 || nums[i] > nums.length) continue;
            //REMEMBER THIS CHECK
            //CHECK IF THE TWO NUMS ARE THE SAME TO PREVENT INFINITE LOOP (Duplicate number)
            if (nums[nums[i] - 1] != nums[i]) {
                swap(nums, nums[i] - 1, i);
                i--; // decrement i so you process number that was swapped
            }
        }
        
        for (int i = 0; i < nums.length; i++) 
            if (nums[i] != i + 1) 
                return i + 1;
        
        
        return nums.length + 1;   
    }
    
    
    public void swap(int[] nums, int a, int b) {
        nums[a] ^= nums[b];
        nums[b] ^= nums[a];
        nums[a] ^= nums[b];
    }
```