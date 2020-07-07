
Pretty Easy Hard


```java

    public int longestConsecutive(int[] nums) {
        
        if (nums.length == 0) return 0;
        
        Set<Integer> set = new HashSet<>();
        
        for (int num : nums) {
            set.add(num);
        }
        
        int count = 1;
        
        for (int num : set) {
            
            if (set.contains(num - 1)) 
                continue;
          
            int curr = 1;
            
            while (set.contains(num + 1)) {
                curr++;
                num++;
                count  = Math.max(count, curr);
                
            }
            
        }
        
        return count; 
    }

```java

