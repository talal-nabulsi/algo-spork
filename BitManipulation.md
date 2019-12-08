
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

// OR shift the bit mask 
int getBit(int num, int i) {
   return ((num & (1 << i)) != 0) ? 1 : 0
}
```

### Set Bit
```java
public int setBit(int num, int i) {
   return  num | (1 << i);
}

```

### Clear bit

```java
int clearBit(int num, int i) {
   int mask = ~(1 << i); // 11111101111111
   return num & mask;
}
```

### Clear bits (MSB through i)

```java
int clearBitsMSBthroughI(int num, int i) {
   int mask = (1 << i) - 1; // Subtracting 1 turns 0000010000 into 0000001111
   return num & mask;
}
```

### Toggle Bit (XOR ^)

```java
int toggleBit(int num, int i) {
   int mask = 1 << i;
   return num ^ mask;
}
```

### Turn off Rightmost bit

```java

int clearRightMostBit(int n) {
   return n & (n - 1);
}
