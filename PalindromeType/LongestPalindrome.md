# Longest Palindrome (LEETCODE #5 very common)

> Cant do better than n^2 so easiest is to just check every center (remember to check both odd and even palindromes)

> Theres also a DP solution


## Expanding around center soution (best, O(n^2))

```java
    // check every center point
    public String longestPalindrome2(String s) {
        String longest = String.valueOf(s.charAt(0));
        
        for (int i = 1; i < s.length(); i++) {
            String curr = findLongest(s, i - 1, i + 1);
            String curr2 = findLongest(s, i - 1, i);

            if (curr.length() > longest.length()) longest = curr;
            if (curr2.length() > longest.length()) longest = curr2;
            
        }
        
        
        return longest;  
    }
    
    
    public String findLongest(String s, int left, int right) {  
        while (left >= 0 && right <= s.length() - 1 && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        
        return s.substring(left + 1, right);
        
    } 
```


## DP Solution O(n^2)

> Easy DP of the length type, 

> if (s.charAt(i) == s.charAt(j))
    dp[i][j] = dp[i + 1][j -1]

> Key Trick: No need to build len = 2 and len = 1 in separate loops just combine them (see commented out code)

```java
    
     //DP Method
     public String longestPalindrome(String s) {
                  
         int n = s.length();
         int maxLen = 0;
         int index = 0;
         
         boolean[][] dp = new boolean[n][n];
         
         
// for (int i = 0; i < n; i++) 
//     dp[i][i] = true;
         
         
// commenting out to consolidate in other loop, leaving for reference for future tika
//          // Checking for palindromes of size 2 and building dp
//          for (int i = 0; i < n - 1; i++) {
             
//              if (s.charAt(i) == s.charAt(i + 1)) {
//                  dp[i][i+1] = true;
//                  maxLen = 2;
//                  index = i;
//              }
//          }
         
         
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


# Even more optimized, no need for length thing, just triangle DP

> IMPORTANT, its cleaner but can't be used for longest palindromic subsequence


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

