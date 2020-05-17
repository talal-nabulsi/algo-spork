# Max Sliding Window, Leetcode 239

> Very easy hard problem
> Solution is to use a Deque/LinkedList and just remove all indexes that map to a value with a value less than the current

```java

    public int[] maxSlidingWindow(int[] nums, int k) {
        
        if (nums.length == 0) return new int[]{};
        
        LinkedList<Integer> q = new LinkedList<>();
        int[] res = new int[nums.length - k + 1];
        
        for (int i = 0; i < nums.length; i++) {
            
            while (!q.isEmpty() && q.peekFirst() == i - k) 
                q.poll();
            
            while (!q.isEmpty() && nums[q.peekLast()] < nums[i]) 
                q.removeLast();
            
            q.offer(i);
            
            if (i + 1 >= k) res[i - k + 1] = nums[q.peekFirst()];  
        } 
        return res;    
    }
```