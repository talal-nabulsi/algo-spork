
Another one of those binary search problems that don't seem like binary search


```java

    // Binary Search for weight capacity
    public int shipWithinDays(int[] weights, int D) {
        int min = 0; int max = 0;

        int capacity = Integer.MAX_VALUE;
        for (int w : weights) {
            max += w;
            min = Math.max(min, w);
        }
        
        while (min <= max) {
            int mid = min + (max - min)/2;
            if (possible(weights, D, mid)) {
                capacity = mid;
                max = mid - 1;
            } else {
                min = mid + 1;
            }
        }
        
        return capacity;
    }
    
    public boolean possible(int[] weights, int D, int capacity) {
        int days = 1;
        int total = 0;
        int i = 0;
        while (i < weights.length) {            
            if (total + weights[i] <= capacity) 
                total += weights[i++];
            else {
                days++;
                total = 0;
            }
        }
        
        return days <= D;
    }
```