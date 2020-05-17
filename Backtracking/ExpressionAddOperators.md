# Expression Add Operators, Leetcode 282

```java

       public List<String> addOperators(String num, int target) {
        
        List<String> result = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        backtrack("", num, target, 0, result, 0L, 0L);
        return result;
        
    }
    
    // Easy to understand once you see solution, but decently hard question
    public void backtrack(String path, String num, int target, int start, List<String> result, long eval, long multed) {
        
        if (start == num.length()) {
            if (target == eval)  
                result.add(path);
            return;
        }
        
        for (int i = start; i < num.length(); i++) {
            
            long curr = Long.parseLong(num.substring(start, i + 1));
            
            // Start is 0 so you cant make any digits! So break for all the rest
            if (num.charAt(start) == '0' && i != start) break;
        
            // If we're at the 0 index you're just getting one number so no need for operators - cant put a + or 0 or *
            // The path is just starting
            if (start == 0) {
                backtrack(path + curr, num, target, i + 1, result, curr, curr);
            } else {
                backtrack(path + '+' + curr, num, target, i + 1, result, eval + curr, curr);
                backtrack(path + '-' + curr, num, target, i + 1, result, eval - curr, -curr);
                // Multed represents current mulitpication chain
                backtrack(path + '*' + curr, num, target, i + 1, result, eval - multed + multed * curr, multed * curr);
            }
             
        }

    }
```