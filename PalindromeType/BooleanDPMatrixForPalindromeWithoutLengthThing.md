
I've explained this in LongestPalindrome.md page, but just adding here for reference


# Even more optimized, no need for length thing, just triangle DP

> IMPORTANT, its cleaner but can't be used for longest palindromic subsequence
> So you should def still know length thing


```java

    // Extra: DP Palindrome Preprocessing, cool trick, we don't even need the length thing, just simple triangle Matrix DP 
    public boolean[][] createPalindromeDPMatrix(String s) {
        boolean[][] dp = new boolean[s.length()][s.length()];
        // IMPORTANT: remember this iteration style
        for(int i = 0; i < s.length(); i++) {
            for(int j = 0; j <= i; j++) {
                if(s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j+1][i-1])) 
                    dp[j][i] = true;
                
            }
        }
        return dp;
    }
```
