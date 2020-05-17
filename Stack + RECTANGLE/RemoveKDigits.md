# Remove K digits

Easy Stack Problem, pop greedily if numbers arent increasing!!


```java
class Solution {
    // The solution on leetcode is explained amazingly
    // Greedily rom
    public String removeKdigits(String num, int k) {
        
        if (k == num.length()) return "0";
        
        Stack<Character> s = new Stack<>();     
        int i = 0;
        
        while (i < num.length()) {
            char c = num.charAt(i++);
            // Keep popping if numbers arent increasing
            while (k > 0 && !s.isEmpty() && c < s.peek()) {
                s.pop(); 
                k--;
            }
            s.push(c);
        }
        
        
        while (k > 0) {
            s.pop();
            k--;
        }
        
        StringBuilder sb = new StringBuilder();
        
        while (!s.isEmpty()) sb.append(s.pop());
        sb.reverse();
        
        i = 0;
        // Remove leading zeros
        while (sb.length() != 1 && i < sb.length() - 1 && sb.charAt(i) == '0') 
            i++;
        
        
        return sb.substring(i);
            
    }
}
```