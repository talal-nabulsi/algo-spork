


```java
//TRICKY INDEX HASHMAP SUM PROBLEM
class Solution {
    // Key here is to realize that we can convert the array to just 1s and 0s if a day is greater than 8
    // Then find the longest subarray with a sum of > 0
    
     public int longestWPI(int[] hours) {
        if (hours.length == 0) return 0;
        int maxLen = 0;
        Map<Integer, Integer> map = new HashMap();  // key is possible sum in hours array, value is index where that sum appears for the first time
        int sum = 0;  // sum at index i indicates the sum of hours[0:i] after transformation
		
        for (int i = 0; i < hours.length; i++) {
            sum += hours[i] > 8 ? 1 : -1;  // transform each hour to 1 or -1
            
            if (!map.containsKey(sum)) {
                map.put(sum, i);  // record index where the sum appears for the FIRST time to get max possible array
            
			
            if (sum > 0)  // in hours[0:i], more 1s than -1s
                maxLen = i + 1;                     
            else if (map.containsKey(sum - 1)) {  
                // get the index j where sum of hours[0:j] is sum - 1, so that sum of hours[j+1:i] is 1
                // We can do this because the array only has zeros and 1s so every possible value will be in the sum
                maxLen = Math.max(maxLen, i - map.get(sum - 1));
                     
        }
        
        return maxLen;
    }
}
```