---
title: "Single_bit_operation"
date: 2023-11-02T18:44:15+08:00
draft: false
---


Golang Single Bit Operation
===

From: 

https://stackoverflow.com/questions/23192262/how-would-you-set-and-clear-a-single-bit-in-go

https://yourbasic.org/golang/bitwise-operator-cheat-sheet/

### Set pos bit

```go
func setBit(n int, pos uint) int {
    n |= (1 << pos)
    return n
}
```

### Clear pos bit

```go
// Clears the bit at pos in n.
func clearBit(n int, pos uint) int {
    mask := ^(1 << pos)
    n &= mask
    return n
}
```



### Check has bit 

```go
func hasBit(n int, pos uint) bool {
    val := n & (1 << pos)
    return (val > 0)
}

```
