   
 # Spiral Matrix I   


```java    
    //Annoying problem but you have to know this one
    //Best two solutions I've seen. Actualy prefer the size one slightly more, easier to remember
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new LinkedList<>(); 
        if (matrix == null || matrix.length == 0) return res;
        int n = matrix.length, m = matrix[0].length;
        int up = 0,  down = n - 1;
        int left = 0, right = m - 1;
        while (res.size() < n * m) {
            
            // Right -->
            for (int j = left; j <= right && res.size() < n * m; j++)
                res.add(matrix[up][j]);
            
            // Down |
            for (int i = up + 1; i <= down - 1 && res.size() < n * m; i++)
                res.add(matrix[i][right]);
                
            // <-- left
            for (int j = right; j >= left && res.size() < n * m; j--)
                res.add(matrix[down][j]);
                  
            // Up ^
            for (int i = down - 1; i >= up + 1 && res.size() < n * m; i--) 
                res.add(matrix[i][left]);
                
            left++; right--; up++; down--; 
        }
        return res;
    }
    
    
    //For the last two you just gotta make sure you don't duplicate the same row or column
    //The first two don't need that check because its already in the while loop
    // You could also use directions so it enters the while loop condition every travseral
   public List<Integer> spiralOrder2(int[][] matrix) {
        
        List<Integer> res = new ArrayList<Integer>();
        
        if (matrix.length == 0) return res;
        
        
        int rowBegin = 0;
        int rowEnd = matrix.length-1;
        int colBegin = 0;
        int colEnd = matrix[0].length - 1;
        
        while (rowBegin <= rowEnd && colBegin <= colEnd) {
            // Traverse Right
            for (int j = colBegin; j <= colEnd; j ++) res.add(matrix[rowBegin][j]);
            rowBegin++;
            
            // Traverse Down
            for (int i = rowBegin; i <= rowEnd; i++) res.add(matrix[i][colEnd]);
            colEnd--;
            
            // Check we're still in boundaries at this point, think if a 1d array!
            if (rowBegin <= rowEnd) 
                // Traverse Left
                for (int j = colEnd; j >= colBegin; j --) res.add(matrix[rowEnd][j]);
            rowEnd--;
            
            if (colBegin <= colEnd) 
                // Traverse Up
                for (int j = rowEnd; j >= rowBegin; j --) res.add(matrix[j][colBegin]);
            colBegin ++;
        }
        
        return res;
    }
    
```java