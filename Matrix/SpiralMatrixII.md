# Spiral Matrix II

> Pretty much identical to spiral matrix I but reverse order

```java

    // Almost identical to spiral matrix I
    public int[][] generateMatrix(int n) {
        int up = 0,  down = n - 1;
        int left = 0, right = n - 1;
        int num = 1;
        int[][] matrix = new int[n][n];
          
        // Dont run into dup problem because matrix is n x n    
        while (num <= n * n) {
            // Right -->
            for (int j = left; j <= right && num <= n * n; j++)
                matrix[up][j] = num++;
            
            // Down |
            for (int i = up + 1; i <= down - 1 && num <= n * n; i++)
                matrix[i][right] = num++;
                
            // <-- left
            for (int j = right; j >= left && num <= n * n; j--)
                matrix[down][j] = num++;
                  
            // Up ^
            for (int i = down - 1; i >= up + 1 && num <= n * n; i--) 
                matrix[i][left] = num++;
                
            left++; right--; up++; down--; 
        }
        return matrix;
    }




```