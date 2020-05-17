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