 
Not too hard of a problem, I solved this one first time on my own.
Just use two pointers


 ```java
 
    public int[][] intervalIntersection(int[][] A, int[][] B) {
        int i = 0, j = 0;
        
        List<int[]> intervals = new ArrayList<>();
        
        while (i < A.length && j < B.length) {
            
            // Calculate and add intersect
            if (intersect(A[i], B[j]) != null) intervals.add(intersect(A[i], B[j]));
            
            // Increment the one that ends first
            if (A[i][1] < B[j][1]) i++; 
            else j++;  
        }
        
        return intervals.toArray(new int[0][0]);      
    }
    
    public int[] intersect(int[] a, int[] b) {
        int[] intersect = new int[] { Math.max(a[0], b[0]), Math.min(a[1], b[1]) };
        return intersect[0] > intersect[1] ? null : intersect;
    }
```