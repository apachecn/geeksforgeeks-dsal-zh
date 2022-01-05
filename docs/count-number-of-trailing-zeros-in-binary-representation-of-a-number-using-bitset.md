# 使用位组

计算一个数字的二进制表示中尾随零的数量

> 原文:[https://www . geeksforgeeks . org/count-二进制表示的尾随零的数量-使用位集/](https://www.geeksforgeeks.org/count-number-of-trailing-zeros-in-binary-representation-of-a-number-using-bitset/)

给定一个数字。任务是使用位集计算一个数的二进制表示中尾随零的个数。
**例:**

```
Input : N = 16
Output : 4
Binary representation of N is 10000\. Therefore,
number of zeroes at the end is 4.

Input : N = 8
Output : 3
```

**方法:**我们只需设置位集中的数字，然后从位集的 0 个索引开始迭代，一旦我们得到 1，我们将打破循环，因为在此之后没有尾随零。
以下是上述办法的实施:

## C++

```
// C++ program to count number of trailing zeros
// in Binary representation of a number
// using Bitset

#include <bits/stdc++.h>
using namespace std;

// Function to count number of trailing zeros in
// Binary representation of a number
// using Bitset
int CountTrailingZeros(int n)
{
    // declare bitset of 64 bits
    bitset<64> bit;

    // set bitset with the value
    bit |= n;

    int zero = 0;

    for (int i = 0; i < 64; i++) {
        if (bit[i] == 0)
            zero++;
        // if '1' comes then break
        else
            break;
    }

    return zero;
}

// Driver Code
int main()
{
    int n = 4;

    int ans = CountTrailingZeros(n);

    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of trailing zeros
// in Binary representation of a number
// using Bitset
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

    // Function to count number of trailing zeros in
    // Binary representation of a number
    // using Bitset
    static int CountTrailingZeros(int n)
    {

        String bit = Integer.toBinaryString(n);
        StringBuilder bit1 = new StringBuilder();
        bit1.append(bit);
        bit1=bit1.reverse();
        int zero = 0;

        for (int i = 0; i < 64; i++) {
            if (bit1.charAt(i) == '0')
                zero++;
            // if '1' comes then break
            else
                break;
        }

        return zero;
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 4;

        int ans = CountTrailingZeros(n);

        System.out.println(ans);
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to count
# number of trailing zeros in
# Binary representation of a number

# Function to count number of
# trailing zeros in Binary
# representation of a number
def CountTrailingZeros(n):

    # declare bitset of 64 bits
    bit = bin(n)[2:]
    bit = bit[::-1]

    zero = 0;

    for i in range(len(bit)):
        if (bit[i] == '0'):
            zero += 1

        # if '1' comes then break
        else:
            break

    return zero

# Driver Code
n = 4

ans = CountTrailingZeros(n)

print(ans)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to count number of trailing zeros
// in Binary representation of a number
// using Bitset
using System;
class GFG
{

  // Function to count number of trailing zeros in
  // Binary representation of a number
  // using Bitset
  static int CountTrailingZeros(int n)
  {
    string bit=Convert.ToString(n, 2);
    char[] charArray = bit.ToCharArray();
    Array.Reverse( charArray );
    string bit1 = new string( charArray );
    int zero = 0;
    for (int i = 0; i < 64; i++)
    {
      if (bit1[i] == '0')
      {
        zero++;
      }

      // if '1' comes then break
      else
      {
        break;
      }
    }
    return zero;
  }

  // Driver Code
  static public void Main ()
  {
    int n = 4;
    int ans = CountTrailingZeros(n);
    Console.WriteLine(ans);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program to count number of trailing zeros
// in Binary representation of a number
// using Bitset

    // Function to count number of trailing zeros in
    // Binary representation of a number
    // using Bitset
    function CountTrailingZeros(n)
    {
        let bit = n.toString(2);
        let bit1=bit.split("");
        bit1=bit1.reverse();
        let zero = 0;

        for (let i = 0; i < 64; i++) {
            if (bit1[i] == '0')
                zero++;
            // if '1' comes then break
            else
                break;
        }

        return zero;
    }

    // Driver Code
    let n = 4;
    let ans = CountTrailingZeros(n);
    document.write(ans);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```