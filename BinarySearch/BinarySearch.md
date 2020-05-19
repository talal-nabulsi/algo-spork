# Binary Search

Easy, just don't forget it!

```java
    public int binarySearch(int target, int[] array) {
        int low = 0;
        int high = array.length - 1;
        int res = -1;
        
        // Remember <=
        while (low <= high) {
            int mid = (high - low)/2 + low;
            
            if (target < nums[mid]) {
                high = mid - 1; // remember the +/-
            } else if (target > nums[mid]k) {
                low = mid + 1; 
            } else {
                // found it
                return mid;
            }
        }
        
        return firstBadVersion;      
    }
```



> Classic Example of the keep going left if you find an answer method

```java
    public int firstBadVersion(int n) {
        int low = 1;
        int high = n;
        int firstBadVersion = -1;
        
        while (low <= high) {
            int mid = (high - low)/2 + low;
            if (isBadVersion(mid)) {
                firstBadVersion = mid; 
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        
        return firstBadVersion;      
    }

```

# Some tips

Personally I perfer `(low <= high)` and `high = mid - 1`  and `low = mid + 1` 
For this to work you must always check if mid is the answer every loop. So you make sure you can elimate mid before moving on. Exiting the while loop means we didn't find an answer.

Sometimes people use `low < high` or `low + 1 < high`. This is useful when you want to exit the loop with one or two elements left. I've never personally had to use this case because I prefer to terminate in the middle.

