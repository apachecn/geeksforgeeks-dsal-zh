# 交换给定数量的位

> 原文:[https://www.geeksforgeeks.org/swap-bits-in-a-given-number/](https://www.geeksforgeeks.org/swap-bits-in-a-given-number/)

给定数字 x 和 x 的二进制表示中的两个位置(从右侧)，编写一个函数，在给定的两个位置交换 n 位并返回结果。还假设两组位不重叠。

**方法 1**
设 p1 和 p2 为给定的两个位置。

**例 1**

```
Input:
x = 47 (00101111)
p1 = 1 (Start from the second bit from the right side)
p2 = 5 (Start from the 6th bit from the right side)
n = 3 (No of bits to be swapped)
Output:
227 (11100011)
The 3 bits starting from the second bit (from the right side) are 
swapped with 3 bits starting from 6th position (from the right side)
```

**例 2**

```
Input:
x = 28 (11100)
p1 = 0 (Start from first bit from right side)
p2 = 3 (Start from 4th bit from right side)
n = 2 (No of bits to be swapped)
Output:
7 (00111)
The 2 bits starting from 0th position (from right side) are
swapped with 2 bits starting from 4th position (from right side)
```

**解决方案**
我们需要交换两组比特。异或门的使用方式与[交换 2 个数字](http://en.wikipedia.org/wiki/XOR_swap_algorithm)的方式类似。下面是算法。

```
1) Move all bits of the first set to the rightmost side
   set1 =  (x >> p1) & ((1U << n) - 1)
Here the expression *(1U << n) - 1* gives a number that 
contains last n bits set and other bits as 0\. We do & 
with this expression so that bits other than the last 
n bits become 0.
2) Move all bits of second set to rightmost side
   set2 =  (x >> p2) & ((1U << n) - 1)
3) XOR the two sets of bits
   xor = (set1 ^ set2) 
4) Put the xor bits back to their original positions. 
   xor = (xor << p1) | (xor << p2)
5) Finally, XOR the xor with original number so 
   that the two sets are swapped.
   result = x ^ xor
```

**实施:**

## C++

```
// C++ Program to swap bits
// in a given number
#include <bits/stdc++.h>
using namespace std;

int swapBits(unsigned int x, unsigned int p1,
             unsigned int p2, unsigned int n)
{
    /* Move all bits of first set to rightmost side */
    unsigned int set1 = (x >> p1) & ((1U << n) - 1);

    /* Move all bits of second set to rightmost side */
    unsigned int set2 = (x >> p2) & ((1U << n) - 1);

    /* Xor the two sets */
    unsigned int Xor = (set1 ^ set2);

    /* Put the Xor bits back to their original positions */
    Xor = (Xor << p1) | (Xor << p2);

    /* Xor the 'Xor' with the original number so that the
    two sets are swapped */
    unsigned int result = x ^ Xor;

    return result;
}

/* Driver code*/
int main()
{
    int res = swapBits(28, 0, 3, 2);
    cout << "Result = " << res;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C Program to swap bits
// in a given number
#include <stdio.h>

int swapBits(unsigned int x, unsigned int p1, unsigned int p2, unsigned int n)
{
    /* Move all bits of first set to rightmost side */
    unsigned int set1 = (x >> p1) & ((1U << n) - 1);

    /* Move all bits of second set to rightmost side */
    unsigned int set2 = (x >> p2) & ((1U << n) - 1);

    /* XOR the two sets */
    unsigned int xor = (set1 ^ set2);

    /* Put the xor bits back to their original positions */
    xor = (xor << p1) | (xor << p2);

    /* XOR the 'xor' with the original number so that the
       two sets are swapped */
    unsigned int result = x ^ xor;

    return result;
}

/* Driver program to test above function*/
int main()
{
    int res = swapBits(28, 0, 3, 2);
    printf("\nResult = %d ", res);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to swap bits
// in a given number

class GFG {

    static int swapBits(int x, int p1, int p2, int n)
    {
        // Move all bits of first set
        // to rightmost side
        int set1 = (x >> p1) & ((1 << n) - 1);

        // Move all bits of second set
        // to rightmost side
        int set2 = (x >> p2) & ((1 << n) - 1);

        // XOR the two sets
        int xor = (set1 ^ set2);

        // Put the xor bits back to
        // their original positions
        xor = (xor << p1) | (xor << p2);

        // XOR the 'xor' with the original number
        // so that the  two sets are swapped
        int result = x ^ xor;

        return result;
    }

    // Driver program
    public static void main(String[] args)
    {
        int res = swapBits(28, 0, 3, 2);
        System.out.println("Result = " + res);
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python program to
# swap bits in a given number

def swapBits(x, p1, p2, n):

    # Move all bits of first
    # set to rightmost side
    set1 =  (x >> p1) & ((1<< n) - 1)

    # Moce all bits of second
    # set to rightmost side
    set2 =  (x >> p2) & ((1 << n) - 1)

    # XOR the two sets
    xor = (set1 ^ set2)

    # Put the xor bits back
    # to their original positions
    xor = (xor << p1) | (xor << p2)

      # XOR the 'xor' with the
      # original number so that the
      # two sets are swapped
    result = x ^ xor

    return result

# Driver code

res = swapBits(28, 0, 3, 2)
print("Result =", res)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to swap bits
// in a given number
using System;

class GFG {

    static int swapBits(int x, int p1, int p2, int n)
    {
        // Move all bits of first
        // set to rightmost side
        int set1 = (x >> p1) & ((1 << n) - 1);

        // Move all bits of second set
        // set to rightmost side
        int set2 = (x >> p2) & ((1 << n) - 1);

        // XOR the two sets
        int xor = (set1 ^ set2);

        // Put the xor bits back to
        // their original positions
        xor = (xor << p1) | (xor << p2);

        // XOR the 'xor' with the original number
        // so that the two sets are swapped
        int result = x ^ xor;

        return result;
    }

    // Driver program
    public static void Main()
    {
        int res = swapBits(28, 0, 3, 2);
        Console.WriteLine("Result = " + res);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to swap bits
// in a given number

// function returns
// the swapped bits
function swapBits($x, $p1, $p2, $n)
{

    // Move all bits of first
    // set to rightmost side
    $set1 = ($x >> $p1) &
            ((1 << $n) - 1);

    // Move all bits of second
    // set to rightmost side
    $set2 = ($x >> $p2) &
            ((1 << $n) - 1);

    // XOR the two sets
    $xor = ($set1 ^ $set2);

    // Put the xor bits back to
    // their original positions
    $xor = ($xor << $p1) |
           ($xor << $p2);

    // XOR the 'xor' with the
    // original number so that
    // the two sets are swapped
    $result = $x ^ $xor;

    return $result;
}

    // Driver Code
    $res = swapBits(28, 0, 3, 2);
    echo "\nResult = ", $res;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to swap bits
// in a given number

    function  swapBits(x, p1, p2, n)
    {
        // Move all bits of first set
        // to rightmost side
        let set1 = (x >> p1) & ((1 << n) - 1);

        // Move all bits of second set
        // to rightmost side
        let set2 = (x >> p2) & ((1 << n) - 1);

        // XOR the two sets
        let xor = (set1 ^ set2);

        // Put the xor bits back to
        // their original positions
        xor = (xor << p1) | (xor << p2);

        // XOR the 'xor' with the original number
        // so that the  two sets are swapped
        let result = x ^ xor;

        return result;
    }

// Driver Code

    let res = swapBits(28, 0, 3, 2);
    document.write("Result = " + res);

</script>
```

**输出:**

```
 Result = 7
```

下面是相同逻辑的一个简短实现

## C

```
int swapBits(unsigned int x, unsigned int p1, unsigned int p2, unsigned int n)
{
    /* xor contains xor of two sets */
    unsigned int xor = ((x >> p1) ^ (x >> p2)) & ((1U << n) - 1);

    /* To swap two sets, we need to again XOR the xor with original sets */
    return x ^ ( (xor << p1) | (xor << p2));
}
```

**方法 2–**
该解决方案侧重于使用与门计算要交换的位的值。然后，我们可以根据是否要交换这些位来设置/取消设置这些位。对于要交换的位数(n)–

*   计算移位 1 =将 p1 位置的位设置为 1 后的值
*   计算移位 2 =将 p2 位置的位设置为 1 后的值
*   值 1 =检查位置 p1 的数字是否设置的数字。
*   值 2 =检查位置 p2 的数字是否设置的数字。
*   如果值 1 和值 2 不同，我们就必须交换位。

**示例:**

```
[28 0 3 2] num=28 (11100) p1=0 p2=3 n=2
   Given = 11100
   Required output = 00111 i.e. (00)1(11) msb 2 bits replaced with lsb 2 bits

n=2
  p1=0,  p2=3
  shift1= 1,  shift2= 1000
  value1= 0,  value2= 1000
 After swap
  num= 10101

n=3
  p1=1,  p2=4
  shift1= 10,  shift2= 10000
  value1= 0,  value2= 10000
 After swap
  num= 00111
```

**实施**

## C++

```
#include <iostream>
using namespace std;

int swapBits(unsigned int num, unsigned int p1,
             unsigned int p2, unsigned int n)
{
    int shift1, shift2, value1, value2;
    while (n--) {
        // Setting bit at p1 position to 1
        shift1 = 1 << p1;
        // Setting bit at p2 position to 1
        shift2 = 1 << p2;

        // value1 and value2 will have 0 if num
        // at the respective positions - p1 and p2 is 0.
        value1 = ((num & shift1));
        value2 = ((num & shift2));

        // check if value1 and value2 are different
        // i.e. at one position bit is set and other it is not
        if ((!value1 && value2) || (!value2 && value1)) {
            // if bit at p1 position is set
            if (value1) {
                // unset bit at p1 position
                num = num & (~shift1);
                // set bit at p2 position
                num = num | shift2;
            }
            // if bit at p2 position is set
            else {
                // set bit at p2 position
                num = num & (~shift2);
                // unset bit at p2 position
                num = num | shift1;
            }
        }
        p1++;
        p2++;
    }
    // return final result
    return num;
}

/* Driver code*/
int main()
{
    int res = swapBits(28, 0, 3, 2);
    cout << "Result = " << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
    static int swapBits(int num, int p1, int p2, int n)
    {
        int shift1, shift2, value1, value2;
        while (n-- > 0)
        {

            // Setting bit at p1 position to 1
            shift1 = 1 << p1;

            // Setting bit at p2 position to 1
            shift2 = 1 << p2;

            // value1 and value2 will have 0 if num
            // at the respective positions - p1 and p2 is 0.
            value1 = ((num & shift1));
            value2 = ((num & shift2));

            // check if value1 and value2 are different
            // i.e. at one position bit is set and other it is not
            if ((value1 == 0 && value2 != 0) ||
                (value2 == 0 && value1 != 0))
            {

                // if bit at p1 position is set
                if (value1 != 0)
                {

                    // unset bit at p1 position
                    num = num & (~shift1);

                    // set bit at p2 position
                    num = num | shift2;
                }

                // if bit at p2 position is set
                else
                {

                    // set bit at p2 position
                    num = num & (~shift2);

                    // unset bit at p2 position
                    num = num | shift1;
                }
            }
            p1++;
            p2++;
        }

        // return final result
        return num;
    }

  // Driver code
  public static void main(String[] args)
  {
    int res = swapBits(28, 0, 3, 2);
    System.out.println("Result = " + res);
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
def swapBits(num, p1, p2, n):
    shift1 = 0
    shift2 = 0
    value1 = 0
    value2 = 0

    while(n > 0):

        # Setting bit at p1 position to 1
        shift1 = 1 << p1

        # Setting bit at p2 position to 1
        shift2 = 1 << p2

        # value1 and value2 will have 0 if num
        # at the respective positions - p1 and p2 is 0.
        value1 = ((num & shift1))
        value2 = ((num & shift2))

        # check if value1 and value2 are different
        # i.e. at one position bit is set and other it is not
        if((value1 == 0 and value2 != 0) or (value2 == 0 and value1 != 0)):

            # if bit at p1 position is set
            if(value1 != 0):

                # unset bit at p1 position
                num = num & (~shift1)

                # set bit at p2 position
                num = num | shift2

            # if bit at p2 position is set
            else:

                # set bit at p2 position
                num = num & (~shift2)

                # unset bit at p2 position
                num = num | shift1
        p1 += 1
        p2 += 1
        n -= 1

    # return final result
    return num

# Driver code
res = swapBits(28, 0, 3, 2)
print("Result =", res)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
using System;
class GFG
{

  static int swapBits(int num, int p1,
                      int p2, int n)
  {
    int shift1, shift2, value1, value2;
    while (n-- > 0)
    {

      // Setting bit at p1 position to 1
      shift1 = 1 << p1;

      // Setting bit at p2 position to 1
      shift2 = 1 << p2;

      // value1 and value2 will have 0 if num
      // at the respective positions - p1 and p2 is 0.
      value1 = ((num & shift1));
      value2 = ((num & shift2));

      // check if value1 and value2 are different
      // i.e. at one position bit is set and other it is not
      if ((value1 == 0 && value2 != 0) || (value2 == 0 && value1 != 0))
      {

        // if bit at p1 position is set
        if (value1 != 0)
        {

          // unset bit at p1 position
          num = num & (~shift1);

          // set bit at p2 position
          num = num | shift2;
        }

        // if bit at p2 position is set
        else
        {

          // set bit at p2 position
          num = num & (~shift2);

          // unset bit at p2 position
          num = num | shift1;
        }
      }
      p1++;
      p2++;
    }

    // return final result
    return num;
  }

  // Driver code
  static void Main()
  {
    int res = swapBits(28, 0, 3, 2);
    Console.WriteLine("Result = " + res);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

function swapBits(num, p1, p2, n)
{
    let shift1, shift2, value1, value2;

    while (n-- > 0)
    {

        // Setting bit at p1 position to 1
        shift1 = 1 << p1;

        // Setting bit at p2 position to 1
        shift2 = 1 << p2;

        // value1 and value2 will have 0 if num
        // at the respective positions - p1 and p2 is 0.
        value1 = ((num & shift1));
        value2 = ((num & shift2));

        // Check if value1 and value2 are different
        // i.e. at one position bit is set and
        // other it is not
        if ((value1 == 0 && value2 != 0) ||
            (value2 == 0 && value1 != 0))
        {

            // If bit at p1 position is set
            if (value1 != 0)
            {

                // Unset bit at p1 position
                num = num & (~shift1);

                // Set bit at p2 position
                num = num | shift2;
            }

            // If bit at p2 position is set
            else
            {

                // Set bit at p2 position
                num = num & (~shift2);

                // Unset bit at p2 position
                num = num | shift1;
            }
        }
        p1++;
        p2++;
    }

    // Return final result
    return num;
}

// Driver code
let res = swapBits(28, 0, 3, 2);

document.write("Result = " + res);

// This code is contributed by suresh07

</script>
```

**输出:**

```
 Result = 7
```

**参考文献:**[](http://graphics.stanford.edu/~seander/bithacks.html#SwappingBitsXOR)
[用 XOR 交换个别位](http://graphics.stanford.edu/~seander/bithacks.html#SwappingBitsXOR)
如果发现有不正确的地方，或者想分享更多关于上面讨论的话题的信息，请写评论。