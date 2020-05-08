# Dynamnic Programming

## Palindrome type problems



### Longest Palindromic Subsequence

> Type: Dynamic Programming

> Subtype: string length

```java
    public int longestPalindromeSubseq(String s) {
        int dp[][] = new int[s.length()][s.length()];

        // Length 1 strings initialized to 1
        for(int i=0; i < s.length(); i++)
            dp[i][i] = 1;
        
        // Start with string length 2 strings
        for(int l = 2; l <= s.length(); l++){
            for(int i = 0; i < s.length()-l + 1; i++){
                int j = i + l - 1;
                if(l == 2 && s.charAt(i) == s.charAt(j)){
                    dp[i][j] = 2;
                }else if(s.charAt(i) == s.charAt(j)){
                    dp[i][j] = dp[i + 1][j-1] + 2;
                }else{
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][s.length()-1];
    }

```
