


```java

 public List<String> findStrobogrammatic(int n) {  
        return recurse(n, n);     
}

    public List<String> recurse(int n, int k) {
        
        List<String> result = new ArrayList<>();
        
        if (n == 0) {
            result.add("");
            return result;
        }
        
        if (n == 1) {
            result.add("0");
            result.add("1");
            result.add("8");
            return result;
        }
        
        List<String> list = recurse(n - 2, k);
        
        for (String s: list) {   
            if (n != k) { result.add("0" + s + "0"); }
            
            result.add("1" + s + "1");
            result.add("8" + s + "8");
            result.add("6" + s + "9");
            result.add("9" + s + "6");   
        }
        
        return result;       
    }
```