
# Find All Anagrams of a String

> Classic Sliding Window problem of the count type

> Easier to understand if you use two maps.. see second solution

> Although this isn't too bad, just remember map[c - 'a'] will only every be zero or positive if it was in p 
> Just visualize a number line

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
                //if we find the window's size equals to p, then we have to move i (narrow the window) to find the new match window
                //++ to reset the hash because we kicked out the left
                //only increase the count if the character is in p
                //the map[c - 'a'] >= 0 indicate it was original in the hash, cuz it won't go below 0
                //If it's less than zero we already have too much of it, so we're getting rid of a letter we don't need)
                if(map[c - 'a']++ >= 0) count++;  
                // Note map[c - 'a'] will only every be zero or positive if it was in p 
                i++;
            }        
        }
        return result; 
    }
```

> The easier to understand version with two hashmaps
> To make the switch, 

1. change -- to ++,
2. change all > to <, <= or >=
3. change pMap to 0

```java

    // Classic sliding window + count problem
    public List<Integer> findAnagrams(String s, String p) {
        int i = 0, j = 0;
        int[] pMap = new int[26];
        int[] sMap = new int[26];
        List<Integer> result = new ArrayList<>();
        
        // Count map represents amount of each in pattern
        for (char c : p.toCharArray()) 
            pMap[c - 'a']++;
        
        // Init count to num characters in P
        int count = p.length();
  
        while (j < s.length()) {
            char c = s.charAt(j++);
            
            // Adding a new letter, if we need more of this letter, decrement count
            if (sMap[c - 'a']++ < pMap[c - 'a']) count--;
            
            if (count == 0) result.add(i);
            
            c = s.charAt(i);
            
            if (j - i == p.length()) {
                //if we find the window's size equals to p, then we have to move i (narrow the window) to find the new match window
                //++ to reset the hash because we kicked out the left
                //only increase the count if the character is in p
                //the map[c - 'a'] >= 0 indicate it was original in the hash, cuz it won't go below 0
                //If it's less than zero we already have too much of it, so we're getting rid of a letter we don't need)
                if(sMap[c - 'a']-- <= pMap[c - 'a']) count++;  
                // Note map[c - 'a'] will only every be zero or positive if it was in p 
                i++;
            }        
        }
        return result; 
    }

```