
# Longest Palindromic Subsequence


> Important Pattern, DP of length type

```java

    public int longestPalindromeSubseq(String s) {
        int dp[][] = new int[s.length()][s.length()];

        for(int i=0; i < s.length(); i++)
            dp[i][i] = 1;
        
        // Start with length 2
        for(int l = 2; l <= s.length(); l++){
            for(int i = 0; i < s.length()-l + 1; i++){
                int j = i + l - 1;
                if(l == 2 && s.charAt(i) == s.charAt(j)){
                    dp[i][j] = 2;
                }else if(s.charAt(i) == s.charAt(j)){
                    dp[i][j] = dp[i + 1][j-1] + 2;
                }else{
                    // just take longest from shorter
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][s.length()-1];
    }

````


## FOR REFERENCE HERE IS Longest Palindrome (not subsequence)

```java

```java
    
     //DP Method
     public String longestPalindrome(String s) {
                  
         int n = s.length();
         int maxLen = 0;
         int index = 0;
         
         boolean[][] dp = new boolean[n][n];
         
         
         for (int len = 1; len <= n; len++) {
             for (int i = 0; i <= n - len; i++) {
                 int j = i + len - 1;
                 if (s.charAt(i) == s.charAt(j)) {
                     if (len == 1 || len == 2 || dp[i + 1][j -1]) {
                         dp[i][j] = true;
                         maxLen = len;
                         index = i;
                     }
                 }
             }
         }
         
         return s.substring(index, index + maxLen);
         
    }
``` 
