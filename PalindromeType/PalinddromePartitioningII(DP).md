
# Palindrome Partitioning II (min cut so all are palindromes)

> Key Optimization: Build DP paindrome as you go
> In interview might be clearer to do it separately for the sake of clarity ( build DP matrix first and then do the min cuts)



```java
// Live and breathe this solution
// Palindrome Partitioning #2, LC 132, Min cuts
// Similar to Word Break
class Solution {
   public int minCut(String s) {
        
    int n = s.length();
    int[] cut = new int[n];
    boolean[][] pal = new boolean[n][n];
    
    // You build dp palindrome as you go
    for(int i = 0; i < n; i++) {
        int min = i;
        for(int j = 0; j <= i; j++) {
            if(s.charAt(j) == s.charAt(i) && (i - j  <=  2 || pal[j + 1][i - 1])) {
                pal[j][i] = true;  
                min = j == 0 ? 0 : Math.min(min, cut[j - 1] + 1);
            }
        }
        
        cut[i] = min;
    }
    return cut[n - 1];
    }
}
```   