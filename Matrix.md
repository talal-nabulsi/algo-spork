# Matrix tips


# LEETCODE 498 Diagonal Traverse
    
```java
    // Super easy, just check (i + j  % 2 == 0), and handle edge cases accordingly
     public int[] findDiagonalOrder(int[][] matrix) {
                
        if (matrix.length == 0) return new int[0];
        
        int i = 0, j = 0;
        int m = matrix.length,  n = matrix[0].length;
        int[] result = new int[m * n];
        
        for (int index = 0; index < result.length; index++) {
            
            result[index] = matrix[i][j];
            
            if ((i + j) % 2 == 0) { // moving up
                if (j == n - 1) {
                    i++;
                } else if (i == 0) {
                    j++;
                } else {
                    i--;
                    j++;
                }   
            } else { // moving down
                if      (i == m - 1) { j++; }
                else if (j == 0)     { i++; }
                else            { i++; j--; }
                
            }
        }   
        return result; 
    }
```


# Sodoku