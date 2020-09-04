
# Shuffle Array (Fisher Yates Algorithm)

```java
    public int[] shuffle() {
        for (int i = 0; i < array.length; i++) 
            swap(i, randRange(i, array.length));
        
        return array;
    }
```

# Bitwise Swap trick

```cplusplus
    *x = *x ^ *y;
    *y = *x ^ *y;
    *x = *x ^ *y;
```

```java
   public void swap2(char[] s, int a, int b) {
        s[a] ^= s[b];
        s[b] ^= s[a];
        s[a] ^= s[b];
    }
```