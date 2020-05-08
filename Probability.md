

# LEETCODE 498 Diagonal Traverse


 ```java
/**
 * The rand7() API is already defined in the parent class SolBase.
 * public int rand7();
 * @return a random integer in the range 1 to 7
 */
˚
```java
// Rejection sampling
// Use two rand7s to get an index 1 to 49
// Reject all greater than 40
// Convert 40 to number between 1 to 10
class Solution extends SolBase {
    public int rand10() {
        int row, col, idx;
        do {
            row = rand7();
            col = rand7();
            idx = col + (row - 1) * 7;
        } while (idx > 40);
        return 1 + (idx - 1) % 10;
    }
}
```