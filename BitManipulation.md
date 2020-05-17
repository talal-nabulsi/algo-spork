
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

### Turn off Rightmost SET bit

```java

int clearRightMostSetBit(int n) {
   return n & (n - 1);
}

```

# Leetcode 476. Number Complement

Find complement of number.
Ex: 5 =101 -> 010

Basically the idea is you want to get a mask of all 1s (11111)

```java
   public int findComplement(int num) {
        return num ^ ((Integer.highestOneBit(num) << 1) - 1);
   }
```

```java
    public int findComplement(int num) {
        int solution = 0;
        int pointer = 1;
        int lsb = 0;
        
        while (num != 0) {
            lsb = num & 1;
            if (lsb == 0) 
                solution = setBit(solution, pointer)
            pointer <<= 1;
            num >>>= 1;   
        }
        return solution;     
    }
```
