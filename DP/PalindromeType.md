
# Leetcode 409: Longest Palindrome (EASY)

```java

   public int longestPalindrome(String s) {
        Map<Character, Integer> map = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char curr = s.charAt(i);
            map.put(curr, map.getOrDefault(curr,0) + 1);
        }
        
        int total = 0;
        int odd = 0;
        
        for (int count : map.values()) {
            if (count % 2 == 0) {
                total += count;
            } else {
                total += count -1; // dont forget this in case its an odd greater than one
                odd = 1;
            }  
        } 
        return total + odd; 
    }
```