
# Valid Palindrome II (easy but slightly tricky)

```java
    public boolean validPalindrome(String s) {
        int l = 0, r = s.length() -1;
        
        while (l < r) {
            if (s.charAt(l) != s.charAt(r)) return isPalindrome(s, l + 1, r) || isPalindrome(s, l, r -1);
            l++; r--;
        }
 
     return true;
    }
    
    public boolean isPalindrome(String s, int l, int r) {
        while (l < r) if (s.charAt(l++) != s.charAt(r--)) return false;
        return true;  
    }
```


