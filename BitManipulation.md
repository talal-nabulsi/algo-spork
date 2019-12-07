
# Bit Manipulation

* & (bitwise and)

* | (bitwise or)

* ~ (bitwise compliment)

* \<< (left shift)

* \>> (right shift)

* \>>> (zero fill right shift)

## Common bit operations

### Get Bit
```java
public int getBit(int num, int position) {
   return (num >>> position) & 1;
}
```

### Set Bit
```java
public int setBit(int num, int position) {
   return (1 << position) & num;
}
```
