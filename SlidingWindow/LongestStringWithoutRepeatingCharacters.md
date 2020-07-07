
# Longest String without repeating characters

> Make sure to checkout all the solutions, 1 and 2 are basically the same, 3 uses an index optimization by saving

```java  
    public int lengthOfLongestSubstring1(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        
        while (j < n) {
            
            while (set.contains(s.charAt(j))) 
                set.remove(s.charAt(i++));
                  
            set.add(s.charAt(j++));
            ans = Math.max(ans, j - i);
        } 
    
        return ans;
    }
    
    public int lengthOfLongestSubstring2(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        
        while (j < n) {
            // If not repeating then add it
            if (!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            } else {
                // Else remove i and narrow the window
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
    
    // EVEN MORE OPTIMAL, just keep track of the last index a character appeared at!
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        int[] index = new int[128]; // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            i = Math.max(index[s.charAt(j)], i);
            ans = Math.max(ans, j - i + 1);
            index[s.charAt(j)] = j + 1;
        }
        return ans;
    }
```