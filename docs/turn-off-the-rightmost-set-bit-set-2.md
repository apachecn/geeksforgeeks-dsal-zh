# 关闭最右边的设置位|设置 2

> 原文:[https://www . geesforgeks . org/off-最右边的 set-bit-set-2/](https://www.geeksforgeeks.org/turn-off-the-rightmost-set-bit-set-2/)

给定一个数字 **N** 。任务是取消设置最右边的 n 位
**示例:**

```
Input: N = 5 
Output: 4
Explanation:
101(5) -> 100(4)

Input : N = 78
Output : 76
Explanation:
1001110(78) -> 1001100(76)
```

**天真的方法:**

*   翻转最右侧设置位的一种简单方法是通过按位右移操作来查找数字中最右侧设置位的位置，以检查第一次出现的 1。

*   然后，在这个位置翻转钻头。翻转可以通过对给定的数字和该位置位设置的数字进行异或运算来完成。
    **重要属性翻转位:**

```
0 ^ 1 = 1
1 ^ 1 = 0

Xor with 1 flips the bit.
```

*   仅设置给定的位可以通过取 2 的位置幂来设置特定的位。

下面是上述方法的实现。

## C++

```
// C++ program to unset the rightmost
// set bit
#include <bits/stdc++.h>
using namespace std;

// Unsets the rightmost set bit 
// of n and returns the result
void FlipBits(int n)
{

    for (int bit = 0; bit < 32; bit++)
    {
        // Checking whether bit position is
        // set or not
        if ((n >> bit) & 1)
        {
            // If bit position is found set,
            // we flip this bit by xoring
            // given number and number with
            // bit position set
            n = n ^ (1ll << bit);
            break;
        }
    }

    cout<<"The number after unsetting the"; 
    cout<<" rightmost set bit "<< n; 

}
// Driver code
int main()
{

    int N = 12;

    FlipBits(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to unset the rightmost
// set bit
import java.util.*;

class GFG{

// Unsets the rightmost set bit
// of n and returns the result
static void FlipBits(int n)
{
    for(int bit = 0; bit < 32; bit++)
    {

       // Checking whether bit position 
       // is set or not
       if ((n >> bit) % 2 > 0)
       {

           // If bit position is found set,
           // we flip this bit by xoring
           // given number and number with
           // bit position set
           n = n ^ (1 << bit);
           break;
       }
    }
    System.out.print("The number after unsetting the");
    System.out.print(" rightmost set bit " + n);
}

// Driver code
public static void main(String[] args)
{
    int N = 12;

    FlipBits(N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to unset the rightmost
# set bit

# Unsets the rightmost set bit
# of n and returns the result
def FlipBits(n):

    for bit in range(32):

        # Checking whether bit position is
        # set or not
        if ((n >> bit) & 1):

            # If bit position is found set,
            # we flip this bit by xoring
            # given number and number with
            # bit position set
            n = n ^ (1 << bit)
            break

    print("The number after unsetting the", end = " ")
    print("rightmost set bit", n)

# Driver code
if __name__ == '__main__':

    N = 12;

    FlipBits(N)

# This code is contributed by BhupendraSingh
```

## C#

```
// C# program to unset the rightmost
// set bit
using System;

class GFG{

// Unsets the rightmost set bit
// of n and returns the result
static void FlipBits(int n)
{
    for(int bit = 0; bit < 32; bit++)
    {

       // Checking whether bit position
       // is set or not
       if ((n >> bit) % 2 > 0)
       {

           // If bit position is found set,
           // we flip this bit by xoring
           // given number and number with
           // bit position set
           n = n ^ (1 << bit);
           break;
       }
    }
    Console.Write("The number after unsetting the ");
    Console.Write("rightmost set bit " + n);
}

// Driver code
static void Main()
{
    int N = 12;

    FlipBits(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript program to unset the rightmost
    // set bit

    // Unsets the rightmost set bit
    // of n and returns the result
    function FlipBits(n)
    {

        for (let bit = 0; bit < 32; bit++)
        {
            // Checking whether bit position is
            // set or not
            if (((n >> bit) & 1) > 0)
            {
                // If bit position is found set,
                // we flip this bit by xoring
                // given number and number with
                // bit position set
                n = n ^ (1 << bit);
                break;
            }
        }

        document.write("The number after unsetting the");
        document.write(" rightmost set bit " + n);

    }

    // Driver code
    let N = 12;

    FlipBits(N);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
The number after unsetting the rightmost set bit 8
```

**时间复杂度:** O(32)

**辅助空间:** O(1)

**高效方法:**
我们可以翻转 O(1)中的 LSB。虽然天真的方法也很有效，但这个问题也有一个线性的解决方案。我们可以做到以下几点:

1.  获得数的 2 的补码(简单地说-n 给出 2 的补码)

2.  在数字和它的二进制补码之间执行按位“与”运算。

3.  从给定的数字中减去上述结果。

4.  最终结果是 LSB 翻转。

**解释**

```
             N = 1001110 (78)
2's compliment = 0110010
      N & (-N) = 0000010
N - (N & (-N)) = 1001100 (76)
```

## C++

```
// C++ program to unset the rightmost
// set bit
#include <bits/stdc++.h>
using namespace std;

// Unsets the rightmost set bit 
// of n and returns the result 
int FlipBits(unsigned int n) 
{ 
    return n -= (n & (-n));
} 

// Driver Code 
int main() 
{ 
    int N = 12; 
    cout<<"The number after unsetting the"; 
    cout<<" rightmost set bit: "<<FlipBits(N); 
    return 0; 
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to unset the rightmost set bit
import java.util.*;
class GFG{

// Unsets the rightmost set bit
// of n and returns the result
static int FlipBits(int n)
{
    return n -= (n & (-n));
}

// Driver Code
public static void main(String[] args)
{
    int N = 12;

    System.out.print("The number after unsetting the ");
    System.out.print("rightmost set bit: " + FlipBits(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to unset the rightmost set bit

# Unsets the rightmost set bit
# of n and returns the result
def FlipBits(n):

    n -= (n & (-n));
    return n;

# Driver Code
if __name__ == '__main__':

    N = 12;

    print("The number after unsetting the", end = "");
    print(" rightmost set bit: ", FlipBits(N));

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program to unset the rightmost set bit
using System;

class GFG{

// Unsets the rightmost set bit
// of n and returns the result
static int FlipBits(int n)
{
    return n -= (n & (-n));
}

// Driver Code
public static void Main(String[] args)
{
    int N = 12;

    Console.Write("The number after" +
                  "unsetting the ");
    Console.Write("rightmost set bit: " +
                  FlipBits(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program to unset the rightmost set bit

    // Unsets the rightmost set bit 
    // of n and returns the result 
    function FlipBits(n) 
    { 
        return n -= (n & (-n));
    } 

    let N = 12; 
    document.write("The number after unsetting the"); 
    document.write(" rightmost set bit: " + FlipBits(N));

</script>
```

**Output:** 

```
The number after unsetting the rightmost set bit: 8
```

**时间复杂度:** O(1)

**辅助空间:** O(1)