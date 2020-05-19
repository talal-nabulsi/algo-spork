
# Rotate Image

>Transpose is basically flipping all the items across the diagonal!

>Remember Upper Triangle Iteration (for int i = 0) for (int j = i + 1) 

>For clockwise, reverse arrays (top down)
>For counter-clockwise reverse each array (left right)

```java
      public void rotate(int[][] matrix) {
        
        int n = matrix.length;

        // reverse from up to down, just reverse arrays
        // for anti-clockwise reverse left to right
        for (int i = 0; i < matrix.length/2; i++) {
            int[] temp = matrix[i];
            matrix[i] = matrix[n - i - 1];
            matrix[n - i - 1] = temp;
        }
        
        // Transpose (Iterate through Upper Triangle)
        for (int i = 0; i < matrix.length; i++) {
            for (int j = i + 1; j < matrix[0].length; j++) {
                int temp  = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }  
        }    
    }



```