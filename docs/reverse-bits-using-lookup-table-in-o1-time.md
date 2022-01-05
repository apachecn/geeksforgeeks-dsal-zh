# 在 0(1)时间内使用查找表反转位

> 原文:[https://www . geesforgeks . org/reverse-bits-use-lookup-table-in-O1-time/](https://www.geeksforgeeks.org/reverse-bits-using-lookup-table-in-o1-time/)

给定一个无符号整数，反转它的所有位，并返回具有反转位的数字。

示例:

```
Input : n = 1
Output : 2147483648  
On a machine with size of unsigned
bit as 32\. Reverse of 0....001 is
100....0.

Input : n = 2147483648
Output : 1       

```

在[之前的帖子](https://www.geeksforgeeks.org/write-an-efficient-c-program-to-reverse-bits-of-a-number/)中，我们看到了两个在 O(n) & O(logn)时间内解决这个问题的方法。这里我们使用查找表在 O(1)时间内解决这个问题。使用查找表很难一次性反转所有 32 位(假设这是 int 的大小)(“因为创建大小为 2 <sup>32</sup> -1】的查找表是不可行的”)。因此，我们将 32 位分成 8 位块(大小为 2<sup>8</sup>-1“0-255”的查找表)。

**查找表**
在查找表中，我们将存储范围内(0-255)的每个数字的倒数

LookupTable[0] = 0 |二进制 00000000 Reverse 000000
lookup table[1]= 128 |二进制 00000001 Reverse 10000000
lookup table[2]= 64 |二进制 000000010 Reverse 010000000
lookup table[3]= 192 |二进制 00000000011 Reverse 110000000000

**我们举一个查找表如何工作的例子。**
让数字= 12456
用二进制表示= 000000000000000001100000101000

```
Split it into 8 bits chunks  :  00000000 | 00000000 | 00110000 | 10101000
         in decimal          :     0          0          48       168
reverse each chunks using lookup table :
Lookuptable[ 0 ] = 0  | in binary 00000000
Lookuptable[48 ] = 12 | in binary 00001100
Lookuptable[168] = 21 | in binary 00010101

Now Binary :  
00000000 | 00000000 | 00001100 | 00010101

Binary chunks after rearrangement : 
00010101 | 00001100 | 00000000 | 00000000   

Reverse of 12456 is 353107968  

```

```
// CPP program to reverse bits using lookup table.
#include<bits/stdc++.h>
using namespace std;

// Generate a lookup table for 32bit operating system 
// using macro 
#define R2(n)     n,     n + 2*64,     n + 1*64,     n + 3*64
#define R4(n) R2(n), R2(n + 2*16), R2(n + 1*16), R2(n + 3*16)
#define R6(n) R4(n), R4(n + 2*4 ), R4(n + 1*4 ), R4(n + 3*4 )

// Lookup table that store the reverse of each table
unsigned int lookuptable[256] = { R6(0), R6(2), R6(1), R6(3) };

/* Function to reverse bits of num */
int reverseBits(unsigned int num)
{
    int reverse_num = 0;

     // Reverse and then rearrange 

                   // first chunk of 8 bits from right
     reverse_num = lookuptable[ num & 0xff ]<<24 | 

                   // second chunk of 8 bits from  right 
                   lookuptable[ (num >> 8) & 0xff ]<<16 | 

                   lookuptable[ (num >> 16 )& 0xff ]<< 8 |
                   lookuptable[ (num >>24 ) & 0xff ] ;

    return reverse_num;
}

//driver program to test above function 
int main()
{
    int x = 12456; 
    printf("%u", reverseBits(x));    
    return 0;
} 
```

输出:

```
353107968

```

时间复杂度:0(1)