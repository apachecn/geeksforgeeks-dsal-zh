# 如何交换给定整数中的两位？

> 原文:[https://www . geesforgeks . org/如何交换给定整数中的两位数/](https://www.geeksforgeeks.org/how-to-swap-two-bits-in-a-given-integer/)

给定整数 n 和其中的两位位置 p1 和 p2，交换给定位置的位。给定的位置来自最低有效位(lsb)。例如，lsb 的位置为 0。
**例:**

```
Input: n = 28, p1 = 0, p2 = 3
Output: 21
28 in binary is 11100\.  If we swap 0'th and 3rd digits, 
we get 10101 which is 21 in decimal.

Input: n = 20, p1 = 2, p2 = 3
Output: 24
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
**方法 1:**
思路是先找到位，然后用[基于异或的交换概念](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)，I..例如，要交换两个数字“x”和“y”，我们要做 x = x ^ y，y = y ^ x 和 x = x ^ y。
下面是上述想法的实现

## C++

```
// C++ program to swap bits in an integer
#include<bits/stdc++.h>
using namespace std;

// This function swaps bit at positions p1 and p2 in an integer n
int swapBits(unsigned int n, unsigned int p1, unsigned int p2)
{
    /* Move p1'th to rightmost side */
    unsigned int bit1 =  (n >> p1) & 1;

    /* Move p2'th to rightmost side */
    unsigned int bit2 =  (n >> p2) & 1;

    /* XOR the two bits */
    unsigned int x = (bit1 ^ bit2);

    /* Put the xor bit back to their original positions */
    x = (x << p1) | (x << p2);

    /* XOR 'x' with the original number so that the
       two sets are swapped */
    unsigned int result = n ^ x;
}

/* Driver program to test above function*/
int main()
{
    int res =  swapBits(28, 0, 3);
    cout<<"Result = "<< res<<" ";
    return 0;
}

// This code is contributed by pratham76.
```

## C

```
// C program to swap bits in an integer
#include<stdio.h>

// This function swaps bit at positions p1 and p2 in an integer n
int swapBits(unsigned int n, unsigned int p1, unsigned int p2)
{
    /* Move p1'th to rightmost side */
    unsigned int bit1 =  (n >> p1) & 1;

    /* Move p2'th to rightmost side */
    unsigned int bit2 =  (n >> p2) & 1;

    /* XOR the two bits */
    unsigned int x = (bit1 ^ bit2);

    /* Put the xor bit back to their original positions */
    x = (x << p1) | (x << p2);

    /* XOR 'x' with the original number so that the
       two sets are swapped */
    unsigned int result = n ^ x;
}

/* Driver program to test above function*/
int main()
{
    int res =  swapBits(28, 0, 3);
    printf("Result = %d ", res);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap bits in an integer
import java.io.*;

class GFG
{

// This function swaps bit at
// positions p1 and p2 in an integer n
static int swapBits( int n, int p1, int p2)
{
    /* Move p1'th to rightmost side */
    int bit1 = (n >> p1) & 1;

    /* Move p2'th to rightmost side */
    int bit2 = (n >> p2) & 1;

    /* XOR the two bits */
    int x = (bit1 ^ bit2);

    /* Put the xor bit back to
    their original positions */
    x = (x << p1) | (x << p2);

    /* XOR 'x' with the original
    number so that the
    two sets are swapped */
    int result = n ^ x;
    return result;
}

    /* Driver code*/
    public static void main (String[] args)
    {
        int res = swapBits(28, 0, 3);
        System.out.println ("Result = " + res);
    }
}

// This code is contributed by ajit..
```

## C#

```
// C# program to swap bits in an integer
using System;
class GFG
{

  // This function swaps bit at
  // positions p1 and p2 in an integer n
  static int swapBits( int n, int p1, int p2)
  {

    /* Move p1'th to rightmost side */
    int bit1 = (n >> p1) & 1;

    /* Move p2'th to rightmost side */
    int bit2 = (n >> p2) & 1;

    /* XOR the two bits */
    int x = (bit1 ^ bit2);

    /* Put the xor bit back to
    their original positions */
    x = (x << p1) | (x << p2);

    /* XOR 'x' with the original
    number so that the
    two sets are swapped */
    int result = n ^ x;
    return result;
  }

  /* Driver code*/
  public static void Main(string[] args)
  {
    int res = swapBits(28, 0, 3);
    Console.Write("Result = " + res);
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// javascript program to swap bits in an integer

// This function swaps bit at
// positions p1 and p2 in an integer n
function swapBits(n , p1 , p2)
{
    /* Move p1'th to rightmost side */
    var bit1 = (n >> p1) & 1;

    /* Move p2'th to rightmost side */
    var bit2 = (n >> p2) & 1;

    /* XOR the two bits */
    var x = (bit1 ^ bit2);

    /* Put the xor bit back to
    their original positions */
    x = (x << p1) | (x << p2);

    /* XOR 'x' with the original
    number so that the
    two sets are swapped */
    var result = n ^ x;
    return result;
}

/* Driver code*/
var res = swapBits(28, 0, 3);
document.write("Result = " + res);

// This code contributed by Princi Singh
</script>
```

## 蟒蛇 3

```
# Python3 program for the above approach

# This function swaps bit at positions p1 and p2 in an integer n
def swapBits(n, p1, p2):

    # Move p1'th to rightmost side
    bit1 = (n >> p1) & 1

    # Move p2'th to rightmost side
    bit2 = (n >> p2) & 1

    # XOR the two bits
    x = (bit1 ^ bit2)

    # Put the xor bit back to their original positions
    x = (x << p1) | (x << p2)

    # XOR 'x' with the original number so that the
    # two sets are swapped
    result = n ^ x
    return result

# Driver program to test above function
if __name__ == '__main__':
    res = swapBits(28, 0, 3)
    print("Result = ", res)

# This code is contributed by nirajgusain5
```

**Output**

```
Result = 21 
```

***时间复杂度:** O(1)*

***辅助空间:**O(1)*T4】

## C++

```
//C++ code for swapping given bits of a number
#include<iostream>
using namespace std;
int swapBits(int n, int p1, int p2)
{
    //left-shift 1 p1 and p2 times
    //and using XOR
    n ^= 1 << p1;
    n ^= 1 << p2;
    return n;
}

//Driver Code
int main()
{
    cout << "Result = " << swapBits(28, 0, 3);
    return 0;
}

//This code is contributed by yashbeersingh42
```

## C

```
//C code for swapping given bits of a number
#include<stdio.h>
int swapBits(int n, int p1, int p2)
{
    //left-shift 1 p1 and p2 times
    //and using XOR
    n ^= 1 << p1;
    n ^= 1 << p2;
    return n;
}

//Driver Code
int main()
{
    printf("Result = %d", swapBits(28, 0, 3));
    return 0;
}

//This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for swapping
// given bits of a number
import java.util.*;
class Main{

public static int swapBits(int n,
                           int p1,
                           int p2)
{
  //left-shift 1 p1 and
  // p2 times and using XOR
  n ^= 1 << p1;
  n ^= 1 << p2;
  return n;
}   

// Driver code
public static void main(String[] args)
{
  System.out.print("Result = " +
                   swapBits(28, 0, 3));
}
}

// This code is contributed by divyeshrabadiya07
```

## 计算机编程语言

```
# Python code for swapping given bits of a number
def swapBits(n, p1, p2):

  # left-shift 1 p1 and p2 times
  # and using XOR
  n ^= 1 << p1
  n ^= 1 << p2
  return n

# Driver Code
print("Result =",swapBits(28, 0, 3))

# This code is contributed by rag2127
```

## C#

```
// C# code for swapping given bits of a number
using System;
class GFG {

  static int swapBits(int n, int p1, int p2)
  {
    // left-shift 1 p1 and p2 times
    // and using XOR
    n ^= 1 << p1;
    n ^= 1 << p2;
    return n;
  }

  // Driver code
  static void Main() {
    Console.WriteLine("Result = " + swapBits(28, 0, 3));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // JavaScript code for swapping given bits of a number

    function swapBits(n, p1, p2)
    {
        //left-shift 1 p1 and p2 times
        //and using XOR
        n ^= 1 << p1;
        n ^= 1 << p2;
        return n;
    }

    document.write("Result = " + swapBits(28, 0, 3));

</script>
```

**Output**

```
Result = 21
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论