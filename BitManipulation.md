
# Bit Manipulation

## Bit Operators

* & (bitwise and)

* | (bitwise or)

* ~ (bitwise compliment)

* \<< (left shift)

* \>> (right shift)

* \>>> (zero fill right shift)

## Common bit operations

### Get Bit
```java
public int getBit(int num, int i) {
   return (num >>> i) & 1;
}

boolean getBit(int num, int i) {
   return ((num & (1 << i)) != 0)
}
```

### Set Bit
```java
public int setBit(int num, int i) {
   return (1 << i) | num;
}

```
