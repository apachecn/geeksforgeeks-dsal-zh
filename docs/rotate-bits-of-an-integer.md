# 旋转一个数字的位

> 原文:[https://www.geeksforgeeks.org/rotate-bits-of-an-integer/](https://www.geeksforgeeks.org/rotate-bits-of-an-integer/)

比特旋转:旋转(或循环移位)是一种类似移位的操作，只是一端脱落的比特放回另一端。
左旋转时，左端脱落的比特放回右端。
右旋转时，右端脱落的钻头放回左端。

示例:
让 n 用 8 位存储。n = 11100101 向左旋转 3，则 n = 00101111(左移 3 位，前 3 位放回最后)。如果使用 16 位或 32 位存储 n，那么 n (000…11100101)的左旋转变为 00..00 **11100101** 000。
如果使用 8 位存储 n，n = 11100101 向右旋转 3，则 n = 10111100(右移 3，最后 3 位放回第一位)。如果使用 16 位或 32 位存储 n，那么 n (000…11100101)向右旋转 3 就变成了 **101** 000..00 **11100** 。

## C++

```
// C++ code to rotate bits
// of number
#include<iostream>

using namespace std;
#define INT_BITS 32
class gfg
{

/*Function to left rotate n by d bits*/
public:
int leftRotate(int n, unsigned int d)
{

    /* In n<<d, last d bits are 0\. To
     put first 3 bits of n at
    last, do bitwise or of n<<d
    with n >>(INT_BITS - d) */
    return (n << d)|(n >> (INT_BITS - d));
}

/*Function to right rotate n by d bits*/
int rightRotate(int n, unsigned int d)
{
    /* In n>>d, first d bits are 0.
    To put last 3 bits of at
    first, do bitwise or of n>>d
    with n <<(INT_BITS - d) */
    return (n >> d)|(n << (INT_BITS - d));
}
};

/* Driver code*/
int main()
{
    gfg g;
    int n = 16;
    int d = 2;
    cout << "Left Rotation of " << n <<
            " by " << d << " is ";
    cout << g.leftRotate(n, d);
    cout << "\nRight Rotation of " << n <<
            " by " << d << " is ";
    cout << g.rightRotate(n, d);
    getchar();
}

// This code is contributed by SoM15242
```

## C

```
#include<stdio.h>
#define INT_BITS 32

/*Function to left rotate n by d bits*/
int leftRotate(int n, unsigned int d)
{
   /* In n<<d, last d bits are 0\. To put first 3 bits of n at
     last, do bitwise or of n<<d with n >>(INT_BITS - d) */
   return (n << d)|(n >> (INT_BITS - d));
}

/*Function to right rotate n by d bits*/
int rightRotate(int n, unsigned int d)
{
   /* In n>>d, first d bits are 0\. To put last 3 bits of at
     first, do bitwise or of n>>d with n <<(INT_BITS - d) */
   return (n >> d)|(n << (INT_BITS - d));
}

/* Driver program to test above functions */
int main()
{
  int n = 16;
  int d = 2;
  printf("Left Rotation of %d by %d is ", n, d);
  printf("%d", leftRotate(n, d));
  printf("\nRight Rotation of %d by %d is ", n, d);
  printf("%d", rightRotate(n, d));
  getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to rotate bits
// of number
class GFG
{
static final int INT_BITS = 32;

/*Function to left rotate n by d bits*/
static int leftRotate(int n, int d) {

    /* In n<<d, last d bits are 0.
       To put first 3 bits of n at
       last, do bitwise or of n<<d with
       n >>(INT_BITS - d) */
    return (n << d) | (n >> (INT_BITS - d));
}

/*Function to right rotate n by d bits*/
static int rightRotate(int n, int d) {

    /* In n>>d, first d bits are 0.
       To put last 3 bits of at
       first, do bitwise or of n>>d
       with n <<(INT_BITS - d) */
    return (n >> d) | (n << (INT_BITS - d));
}

// Driver code
public static void main(String arg[])
{
    int n = 16;
    int d = 2;
    System.out.print("Left Rotation of " + n +
                          " by " + d + " is ");
    System.out.print(leftRotate(n, d));

    System.out.print("\nRight Rotation of " + n +
                             " by " + d + " is ");
    System.out.print(rightRotate(n, d));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 code to
# rotate bits of number

INT_BITS = 32

# Function to left
# rotate n by d bits
def leftRotate(n, d):

    # In n<<d, last d bits are 0.
    # To put first 3 bits of n at
    # last, do bitwise or of n<<d
    # with n >>(INT_BITS - d)
    return (n << d)|(n >> (INT_BITS - d))

# Function to right
# rotate n by d bits
def rightRotate(n, d):

    # In n>>d, first d bits are 0.
    # To put last 3 bits of at
    # first, do bitwise or of n>>d
    # with n <<(INT_BITS - d)
    return (n >> d)|(n << (INT_BITS - d)) & 0xFFFFFFFF

# Driver program to
# test above functions
n = 16
d = 2

print("Left Rotation of",n,"by"
      ,d,"is",end=" ")
print(leftRotate(n, d))

print("Right Rotation of",n,"by"
     ,d,"is",end=" ")
print(rightRotate(n, d))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to rotate
// bits of a number
using System;

class GFG
{
    static int INT_BITS = 32;

    /* Function to left rotate n by d bits*/
    static int leftRotate(int n, int d) {

        /* In n<<d, last d bits are 0.
        To put first 3 bits of n at
        last, do bitwise or of n<<d with
        n >>(INT_BITS - d) */
        return (n << d) | (n >> (INT_BITS - d));
    }

    /*Function to right rotate n by d bits*/
    static int rightRotate(int n, int d) {

        /* In n>>d, first d bits are 0.
        To put last 3 bits of at
        first, do bitwise or of n>>d
        with n <<(INT_BITS - d) */
        return (n >> d) | (n << (INT_BITS - d));
    }

    // Driver code
    public static void Main()
    {
        int n = 16;
        int d = 2;

        Console.Write("Left Rotation of " + n
                      + " by " + d + " is ");
        Console.Write(leftRotate(n, d));

        Console.Write("\nRight Rotation of " + n
                       + " by " + d + " is ");
        Console.Write(rightRotate(n, d));
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// JavaScript code to rotate bits
// of number
let INT_BITS = 32;

/*Function to left rotate n by d bits*/

function leftRotate( n,  d)
{   
    /* In n<<d, last d bits are 0\. To
     put first 3 bits of n at
    last, do bitwise or of n<<d
    with n >>(INT_BITS - d) */
    return (n << d)|(n >> (INT_BITS - d));
}

/*Function to right rotate n by d bits*/
function rightRotate( n, d)
{
    /* In n>>d, first d bits are 0.
    To put last 3 bits of at
    first, do bitwise or of n>>d
    with n <<(INT_BITS - d) */
    return (n >> d)|(n << (INT_BITS - d));
}

/* Driver code*/
let n = 16;
let d = 2;
document.write("Left Rotation of " + n +
            " by " + d + " is ");
document.write(leftRotate(n, d));
document.write("<br>");           
document.write("\nRight Rotation of " + n +
            " by " + d + " is ");
document.write(rightRotate(n, d));

</script>
```

**输出:**

```
Left Rotation of 16 by 2 is 64
Right Rotation of 16 by 2 is 4
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**16 位数字:**

## C++

```
#include <bits/stdc++.h>

using namespace std;

#define SHORT_SIZE 16

// function to rotate the given unsigned short
// in the left direction
unsigned short leftRotate(unsigned short x, short d)
{
    /**
     * By doing x << d, we move the first(right most) d bits
     * to the left most d bits, and at the same time we move
     * the left most d bits to the right side,
     * performing OR operation between the two gives use the
     * required result.
     * */

    return (x << d) | (x >> (SHORT_SIZE - d));
}

// function to rotate the given unsigned short
// in the right direction
unsigned short rightRotate(unsigned short x, short d)
{
    /**
     * By doing x >> d, we move the first(left most) d bits
     * to the right most d bits, and at the same time we move
     * the right most d bits to the right side,
     * performing OR operation between the two gives use the
     * required result.
     * */

    return (x >> d) | (x << (SHORT_SIZE - d));
}

/* Driver program to test above functions */
int main()
{
    // Test case
    unsigned short n = 28;
    short d = 2;

    cout << leftRotate(n, d) << endl;
    cout << rightRotate(n, d) << endl;

    return 0;
}

// This code is contributed by ganesh227
```

## C

```
#include <stdio.h>
#define SHORT_SIZE 16

// function to rotate the given unsigned short
// in the left direction
unsigned short leftRotate(unsigned short x, short d)
{
    /**
     * By doing x << d, we move the first(right most) d bits
     * to the left most d bits, and at the same time we move
     * the left most d bits to the right side,
     * performing OR operation between the two gives use the
     * required result.
     * */

    return (x << d) | (x >> (SHORT_SIZE - d));
}

// function to rotate the given unsigned short
// in the right direction
unsigned short rightRotate(unsigned short x, short d)
{
    /**
     * By doing x >> d, we move the first(left most) d bits
     * to the right most d bits, and at the same time we move
     * the right most d bits to the right side,
     * performing OR operation between the two gives use the
     * required result.
     * */

    return (x >> d) | (x << (SHORT_SIZE - d));
}

/* Driver program to test above functions */
int main()
{
    // Test case
    unsigned short n = 28;
    short d = 2;
    printf("%d\n", leftRotate(n, d));
    printf("%d\n", rightRotate(n, d));

    return 0;
}

// This code is contributed by ganesh227
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static void main (String[] args) {
        int N=28;
          int D=2;
          rotate(N,D);
    }

   static void rotate(int N, int D)
    {
        // your code here
        int t=16;
        int left= ((N<<D) | N>>(t-D)) & 0xFFFF;
        int right=((N>>D) | N<<(t-D)) & 0xFFFF;
        System.out.println(left);
         System.out.println(right);
    }

}
```

## 蟒蛇 3

```
SHORT_SIZE = 16

# function to rotate the given unsigned short
# in the left direction
def leftRotate(x, d):

    return (x << d) | (x >> (SHORT_SIZE - d))

  # function to rotate the given unsigned short
# in the right direction
def rightRotate(x, d):

    return (x >> d) | (x << (SHORT_SIZE - d)) & 0xDDDDDF

# Driver program to test above functions
# Test case
n = 28
d = 2

print("Left Rotation of",n,"by"
      ,d,"is",end=" ")
print(leftRotate(n, d))

print("Right Rotation of",n,"by"
     ,d,"is",end=" ")
print(rightRotate(n, d))

# This code is contributed by shivanisinghss2110
```

## C#

```
/*package whatever //do not write package name here */
using System;
using System.Collections.Generic;
public class GFG {
    public static void Main(String[] args) {
        int N = 28;
          int D = 2;
          rotate(N, D);
    }

  // Driver code
   static void rotate(int N, int D)
    {
        int t = 16;
        int left = ((N<<D) | N>>(t-D)) & 0xFFFF;
        int right = ((N>>D) | N<<(t-D)) & 0xFFFF;
        Console.WriteLine(left);
         Console.WriteLine(right);
    }

}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

function rotate(N,D)
{
    // your code here
        let t = 16;
        let left = ((N<<D) | N>>(t-D)) & 0xFFFF;
        let right = ((N>>D) | N<<(t-D)) & 0xFFFF;
        document.write(left + "<br>");
         document.write(right + "<br>");
}

let N = 28;
let D = 2;
rotate(N, D);

// This code is contributed by avanitrachhadiya2155
</script>
```

```
Left Rotation of 28 by 2 is 112
Right Rotation of 28 by 2 is 7
```

**时间复杂度** : O(1)

**空间复杂度** : O(1)

如果您发现上述程序中有任何 bug 或其他解决相同问题的方法，请写评论。