 
```java 
    public List<List<String>> partition(String s) {
        
        List<List<String>> result = new ArrayList<>();
        List<String> tempList = new ArrayList<>();
        backtrack(s, result, tempList, 0);
       
        return result;
    }
    
    // Really easy, just basic backtracking, use DP for mincuts (Palindrome Partitioning 2)
    public void backtrack(String s, List<List<String>> result, List<String> tempList, int start) {
        
      if (start == s.length()) 
          result.add(new ArrayList<>(tempList));
      
      for (int i = start; i < s.length(); i++) {
          if (isPalindrome(s, start, i)) {
              tempList.add(s.substring(start, i + 1));
              backtrack(s, result, tempList, i + 1);
              tempList.remove(tempList.size() - 1);
          }
      }
    }
   
    //HELPER FUNCTION
    public boolean isPalindrome(String s, int left, int right) {   
        while (left < right) {
            if (s.charAt(left++) != s.charAt(right--)) 
                return false;
        }
        return true;     
    }
    
    
    // Extra: DP Palindrome Preprocessing, cool trick, we don't even need the length thing, just simple triangle DP 
    public boolenPalindrome() {
        boolean[][] dp = new boolean[s.length()][s.length()];
        for(int i = 0; i < s.length(); i++) {
            for(int j = 0; j <= i; j++) {
                if(s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j+1][i-1])) 
                    dp[j][i] = true;
            }
        }
    }

```