# Leetcode 678 Valid Parenthesis String


```java

    // Pretty tricky problem but makes sense once you get it
    // Trick is: we don't have to worry about asteriks overlapping, a right paren will be able to take over the role of an asterik
    public boolean checkValidString(String s) {
        int leftWildcard = 0, left = 0;
        
        for (int i = 0; i < s.length(); i++) {  
            // Handle rights 
            if (s.charAt(i) == ')') {
                leftWildcard--;
                if (leftWildcard < 0) return false;
            } else {
                leftWildcard++;
            }
            
            // Handle left parenthesis, just make sure its zero at the end
            if (s.charAt(i) == '(') 
                left++;
            else 
                left = Math.max(0, --left);         
        }
        
        return left == 0;
    }
```