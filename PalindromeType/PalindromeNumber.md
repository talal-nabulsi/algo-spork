
# Palindrome Number

Easy, idea is to reverse the number and check for equality


```java
     public boolean isPalindrome(int x) {
        int num = x;
        int n = 0;
        
        if (x < 0) return false;
        
        while (x != 0) {
            // Build number backwards, get last and mult by 10
            int last = x % 10;
            n = n * 10 + last;
            x /= 10;
        }
        
        if (n == num) return true;
        return false; 
    }
```