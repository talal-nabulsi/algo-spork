

# Helper Tip

> Generate random number within range

```java
    Random rand = new Random();

    private int randRange(int min, int max) {
        return rand.nextInt(max - min) + min;
    }
```



# Leetcode Rand 10 from Rand 7

> Technique: Rejection Sampling

 ```java
/**
 * The rand7() API is already defined in the parent class SolBase.
 * public int rand7();
 * @return a random integer in the range 1 to 7
 */
˚
// Rejection sampling
// Use two rand7s to get an index 1 to 49
// Reject all greater than 40
// Convert 40 to number between 1 to 10
    public int rand10() {
        int row, col, idx;
        do {
            row = rand7();
            col = rand7();
            idx = col + (row - 1) * 7;
        } while (idx > 40);
        return 1 + (idx - 1) % 10;
    }

```


# Shuffle an Array (Fisher Yates Algorithm)

```java
    public int[] shuffle() {
        for (int i = 0; i < array.length; i++) 
            swap(i, randRange(i, array.length));
        
        return array;
    }
```

# Reservoir Sampling