
# Shuffle Array (Fisher Yates Algorithm)

```java
    public int[] shuffle() {
        for (int i = 0; i < array.length; i++) 
            swap(i, randRange(i, array.length));
        
        return array;
    }
```