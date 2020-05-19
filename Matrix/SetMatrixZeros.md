
# Set Matrix Zeros

> Again, easy but very tricky parts

> Use first row and first col to store info about zeros

> JUST REMEMBER first row and first col occupy same place

> So you gotta use booleans for those and do them AT THE END

> Or it'll mess everything up

```java
    // Again, easy but very tricky parts
    // Use first row and first col to store info about zeros
    // JUST REMEMBER first row and first col occupy same place
    // So you gotta use booleans for those and do them AT THE END
    // Or it'll mess everything up
    
    public void setZeroes(int[][] matrix) {
        boolean firstRow = false;
        boolean firstCol = false;
        
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {  
                if (matrix[i][j] == 0) {
                    if (i == 0) firstRow = true;
                    if (j == 0) firstCol = true;
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }       
            }
        }
        
       // Iterate thorugh matrix excluding fist row and col
       for (int i = 1; i < matrix.length; i++) 
            for (int j = 1; j < matrix[0].length; j++) 
                if (matrix[0][j] == 0 || matrix[i][0] == 0) 
                    matrix[i][j] = 0;
              
        
        // Set at THE END or it'll mess everything up
        if (firstRow) setRowZero(0, matrix);
        if (firstCol) setColZero(0, matrix);  
    }
    
    
    public void setRowZero(int i, int[][] matrix) {
        for (int j = 0; j < matrix[0].length; j++)
            matrix[i][j] = 0;   
    }
    
    public void setColZero(int j, int[][] matrix) {
        for (int i = 0; i < matrix.length; i++)
            matrix[i][j] = 0; 
    }
```