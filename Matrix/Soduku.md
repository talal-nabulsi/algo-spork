# Valid soduku

Use % for horizontal traversal. Because % increments by 1 for each j : 0%3 = 0 , 1%3 = 1, 2%3 = 2, and resets back. So this covers horizontal traversal for each block by 3 steps.

Use / for vertical traversal. Because / increments by 1 after every 3 j: 0/3 = 0; 1/3 = 0; 2/3 =0; 3/3 = 1.

```java
    public boolean isValidSudoku(char[][] board) {
        
        // i == ith box
        for (int i = 0; i < 9; i++) {
            Set<Character> horizontal = new HashSet<>();
            Set<Character> vertical = new HashSet<>();
            Set<Character> square = new HashSet<>();
            
            // Position in Big square(why you mult by 3)
            int r = 3 * (i/3); //0, 3, or 6
            int c = 3 * (i%3); //0, 3, or 6
            
            // j == jth cell within a box
            for (int j = 0; j < 9; j++) {
                if (board[i][j] != '.' && !horizontal.add(board[i][j])) return false;
                if (board[j][i] != '.' && !vertical.add(board[j][i])) return false;
                
                // Pos in mini squre
                int row = r + j/3;
                int col = c + j%3;
                
                if (board[row][col] != '.' && !square.add(board[row][col])) return false;
            }  
        }
        
        return true;
    }
                
    public boolean isValid(char c, Set<Character> set) {
        return c >= '0' && c <= '9' && !set.add(c);
    }
```java


# Solve Sodoku

Brute force backtracking: Just try to fill every empty square if it's valid

```java

 public void solveSudoku(char[][] board) {
        if(board == null || board.length == 0)
            return;
        solve(board);
    }
    
    public boolean solve(char[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
              if (board[i][j] == '.')  {
                for (char c = '1'; c <= '9'; c++) {
                    if (valid(board, i, j, c)) {
                        board[i][j] = c;
                        if (solve(board)) return true;
                        board[i][j] = '.';
                    }
                }
                return false;
              }
            }
        }      
        return true;  
    }
    
    public boolean valid(char[][] board, int row, int col, char c) {
        // Check if c isn't already taken in box, row, or col
        for (int i = 0; i < 9; i++) { 
            if (board[row][i] == c) return false;
            if (board[i][col] == c) return false;
            int x = 3 * (row/3) + i/3;
            int y = 3 * (col/3) + i % 3;
            if (board[x][y] == c) return false;     
        }
        
        return true;   
    }
```