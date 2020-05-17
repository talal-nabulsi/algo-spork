
> Same as other leetcode, LongestPalindromicSubsequence

> s.length() - longestPalindromicSubsequence.length();

```java

  
    // My idea was correct just find longestPalindromicSubsequence and find diff in size
    public int minInsertions(String s) {
        return s.length() - longestPalindromeSubseq(s);
    }
    
    // Same as other leetcode
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
```