



```java

    // Classic sliding window + count problem
    public List<Integer> findAnagrams(String s, String p) {
        int i = 0, j = 0;
        int[] map = new int[26];
        List<Integer> result = new ArrayList<>();
        
        // Count map represents amount of each in pattern
        for (char c : p.toCharArray()) 
            map[c - 'a']++;
        
        // Init count to num characters in P
        int count = p.length();
  
        while (j < s.length()) {
            char c = s.charAt(j++);
            
            // Adding a new letter, if we need more of this letter, decrement count
            // If its zero or below, we already have too much of this letter, so don't decrement count;
            if (map[c - 'a']-- > 0) count--;
            
            if (count == 0) result.add(i);
            
            c = s.charAt(i);
            
            if (j - i == p.length()) {
                // When big string doesn't have enough of that letter, or is at equilibriam
                // And you're losing that letter, so increment count
                // (If it's less than zero we already have too much of it, so we're getting rid of a letter we don't need)
                if(map[c - 'a']++ >= 0) count++;
                i++;
            }        
        }
        return result; 
    }
    
    public charIndex

```


