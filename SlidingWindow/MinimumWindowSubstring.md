
# Minimum Window Substring

> Almost same as find anagrams except you gotta shorten the window more

```java

    public String minWindow(String s, String t) {
        int i = 0, j = 0;
        int[] sMap = new int[128];
        int[] tMap = new int[128];
        int min = Integer.MAX_VALUE;
        String res = "";
        
        // Count map represents amount of each in pattern
        for (char c : t.toCharArray()) 
            tMap[c]++;
        
        // Init count to num characters in P
        int count = t.length();
  
        while (j < s.length()) {
            char c = s.charAt(j);
            
            // Adding a new letter, if we need more of this letter, decrement count
            if (sMap[c]++ < tMap[c]) count--;
                        
            while (count == 0) {
                c = s.charAt(i);

                if (j - i + 1 < min) {
                    min = j - i + 1;
                    res = s.substring(i, j + 1);
                }
    
                if(sMap[c]-- <= tMap[c]) count++;  
                i++;
            }
            j++;
        }
        return res; 
    }
```

HashMap Version


```java

    public String minWindow(String s, String t) {
        
        Map<Character, Integer> map = new HashMap<>();
        Map<Character, Integer> target = new HashMap<>();
        int min = Integer.MAX_VALUE;
        String window = "";
        
        for (char c : t.toCharArray()) map.put(c, map.getOrDefault(c, 0) + 1);
        
        int count = 0;
        
        int i = 0;
        int j = 0;
        
        while (j < s.length()) {
            
            char c = s.charAt(j);
            if (map.containsKey(c)) {
                target.put(c, target.getOrDefault(c, 0) + 1);
                if (target.get(c) <= map.get(c)) count++;
            }
            
            while (count == t.length()) {
                
                if (j - i + 1 < min) {
                    min  = j - i + 1;
                    window = s.substring(i, j + 1);
                }
                
                c = s.charAt(i);
                if (map.containsKey(c)) {
                    target.put(c, target.get(c) - 1);
                    if (target.get(c) < map.get(c)) count --;
                }
                
                i++;
                
            }
            
            j++;
            
 
        }
        
        return window;

        
    }
```