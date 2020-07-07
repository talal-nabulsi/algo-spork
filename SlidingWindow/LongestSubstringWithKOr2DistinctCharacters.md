# Longest Substring with 2 distinct characters


```java

      public int lengthOfLongestSubstringTwoDistinct(String s) {
        
        Map<Character, Integer> map = new HashMap<>();
        int i = 0, j = 0;
        int max = 0;
        
        while (j < s.length()) {
            char c = s.charAt(j++);
            map.put(c, map.getOrDefault(c, 0) + 1);
            
            while (map.size() > 2) {
                c = s.charAt(i++);
                map.put(c, map.get(c) - 1);
                if (map.get(c) == 0) map.remove(c);
            }
            
            max = Math.max(max, j - i);
        }
        return max;  
    }
```



```java


  // Beautiful solution, designed by me  
  public int lengthOfLongestSubstringKDistinct(String s, int k) {
        
        int i = 0, j = 0, max = 0;
        Map<Character, Integer> map = new HashMap<>();
    
        while (j < s.length()) {
           char c = s.charAt(j);
           map.put(c, map.getOrDefault(c, 0) + 1);
            
            // While greater than k, narrow the window until it's validd
            while (map.size() > k) {
                c = s.charAt(i++);
                map.put(c, map.get(c) - 1);
                if (map.get(c) == 0) map.remove(c);
            }
            max = Math.max(max, j - i + 1);
            j++;
        }
        
        return max;
    }
```