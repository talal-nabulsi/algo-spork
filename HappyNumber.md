
> Keep doing operation until you get 1 or run into a repeating number

```java

    public boolean isHappy(int n) {
        return isHappy(n, new HashSet<>());   
    }
    
    public boolean isHappy(int n, Set<Integer> set) {
        if (n == 1) return true;
        if (set.contains(n)) return false;
        set.add(n);
        int res = 0;
        
        while (n != 0) {
            res += (n%10) * (n%10);
            n /= 10;
        }
        return isHappy(res, set);    
    }

```