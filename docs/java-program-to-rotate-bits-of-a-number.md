# 旋转数字位的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序旋转位数/](https://www.geeksforgeeks.org/java-program-to-rotate-bits-of-a-number/)

比特旋转:旋转(或循环移位)是一种类似移位的操作，只是一端脱落的比特放回另一端。
左旋转时，左端脱落的比特放回右端。
右旋转时，右端脱落的钻头放回左端。

示例:
让 n 用 8 位存储。n = 11100101 向左旋转 3，则 n = 00101111(左移 3 位，前 3 位放回最后)。如果使用 16 位或 32 位存储 n，那么 n (000…11100101)的左旋转变为 00..00 **11100101** 000。
如果使用 8 位存储 n，n = 11100101 向右旋转 3，则 n = 10111100(右移 3，最后 3 位放回第一位)。如果使用 16 位或 32 位存储 n，那么 n (000…11100101)向右旋转 3 就变成了 **101** 000..00 **11100** 。

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

    System.out.print("
Right Rotation of " + n +
                             " by " + d + " is ");
    System.out.print(rightRotate(n, d));
}
}

// This code is contributed by Anant Agarwal.
```

**输出:**

```
Left Rotation of 16 by 2 is 64
Right Rotation of 16 by 2 is 4
```

**16 位数字:**

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

Output:

```
Left Rotation of 28 by 2 is 112
Right Rotation of 28 by 2 is 7
```

**时间复杂度** : O(1)

**空间复杂度** : O(1)

更多详情请参考[旋转数字位](https://www.geeksforgeeks.org/rotate-bits-of-an-integer/)整篇文章！