# 求 N 和 N 的 32 位二进制表示反转形成的数之间的最大值

> 原文:[https://www . geeksforgeeks . org/find-n 和 n 的 32 位二进制表示反转形成的数字之间的最大值/](https://www.geeksforgeeks.org/find-the-maximum-between-n-and-the-number-formed-by-reversing-32-bit-binary-representation-of-n/)

给定一个正的 32 位整数 **N** ，任务是找出 **N** 的值与[十进制表示](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)对[求反](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)得到的数之间的最大值**N**T11】在一个 32 位整数中的二进制表示。

**示例:**

> **输入:** N = 6
> **输出:** 1610612736
> **解释:**
> 6 在 32 位整数中的二进制表示为 00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
> 反转这个二进制字符串得到(01100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
> N 与得到的数字之间的最大值为 1610612736。所以，打印 1610612736。
> 
> **输入:**N = 1610612736
> T3】输出: 1610612736

**方法:**按照以下步骤解决问题:

*   [计算数字 **N** 的二进制字符串](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)，并将其存储在字符串 **S** 中。
*   [反转](https://www.geeksforgeeks.org/stdreverse-in-c/)弦 **S** 。
*   [计算变量中新反转字符串 **S** 的十进制值](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)，比如 **M** 。
*   完成上述步骤后，打印 **N** 和 **M** 的最大值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that obtains the number
// using said operations from N
int reverseBin(int N)
{
    // Stores the binary representation
    // of the number N
    string S = "";
    int i;

    // Find the binary representation
    // of the number N
    for (i = 0; i < 32; i++) {

        // Check for the set bits
        if (N & (1LL << i))
            S += '1';
        else
            S += '0';
    }

    // Reverse the string S
    reverse(S.begin(), S.end());

    // Stores the obtained number
    int M = 0;

    // Calculating the decimal value
    for (i = 0; i < 32; i++) {

        // Check for set bits
        if (S[i] == '1')
            M += (1LL << i);
    }
    return M;
}

// Function to find the maximum value
// between N and the obtained number
int maximumOfTwo(int N)
{
    int M = reverseBin(N);

    return max(N, M);
}

// Driver Code
int main()
{
    int N = 6;
    cout << maximumOfTwo(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function that obtains the number
    // using said operations from N
    static int reverseBin(int N)
    {
        // Stores the binary representation
        // of the number N
        String S = "";
        int i;

        // Find the binary representation
        // of the number N
        for (i = 0; i < 32; i++) {

            // Check for the set bits
            if ((N & (1L << i)) != 0)
                S += '1';
            else
                S += '0';
        }

        // Reverse the string S
        S = (new StringBuilder(S)).reverse().toString();

        // Stores the obtained number
        int M = 0;

        // Calculating the decimal value
        for (i = 0; i < 32; i++) {

            // Check for set bits
            if (S.charAt(i) == '1')
                M += (1L << i);
        }
        return M;
    }

    // Function to find the maximum value
    // between N and the obtained number
    static int maximumOfTwo(int N)
    {
        int M = reverseBin(N);

        return Math.max(N, M);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 6;
        System.out.print(maximumOfTwo(N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that obtains the number
# using said operations from N
def reverseBin(N):

    # Stores the binary representation
    # of the number N
    S = ""
    i = 0

    # Find the binary representation
    # of the number N
    for i in range(32):

        # Check for the set bits
        if (N & (1 << i)):
            S += '1'
        else:
            S += '0'

    # Reverse the string S
    S = list(S)
    S = S[::-1]
    S = ''.join(S)

    # Stores the obtained number
    M = 0

    # Calculating the decimal value
    for i in range(32):

        # Check for set bits
        if (S[i] == '1'):
            M += (1 << i)

    return M

# Function to find the maximum value
# between N and the obtained number
def maximumOfTwo(N):

    M = reverseBin(N)

    return max(N, M)

# Driver Code
if __name__ == '__main__':

    N = 6
    print(maximumOfTwo(N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{
static string ReverseString(string s)
    {
        char[] array = s.ToCharArray();
        Array.Reverse(array);
        return new string(array);
    }

// Function that obtains the number
// using said operations from N
public static int reverseBin(int N)
{

    // Stores the binary representation
    // of the number N
    string S = "";
    int i;

    // Find the binary representation
    // of the number N
    for (i = 0; i < 32; i++) {

        // Check for the set bits
        if ((N & (1L << i)) != 0)
            S += '1';
        else
            S += '0';
    }

    // Reverse the string S
    S = ReverseString(S);

    // Stores the obtained number
    int M = 0;

    // Calculating the decimal value
    for (i = 0; i < 32; i++) {

        // Check for set bits
        if (S[i] == '1')
            M +=  (1 << i);
    }
    return M;
}

// Function to find the maximum value
// between N and the obtained number
static int maximumOfTwo(int N)
{
    int M = reverseBin(N);

    return Math.Max(N, M);
}

// Driver Code
static void Main()
{
    int N = 6;
    Console.Write(maximumOfTwo(N));

}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that obtains the number
// using said operations from N
function reverseBin(N)
{
    // Stores the binary representation
    // of the number N
    let S = "";
    let i;

    // Find the binary representation
    // of the number N
    for (i = 0; i < 32; i++) {

        // Check for the set bits
        if (N & (1 << i))
            S += '1';
        else
            S += '0';
    }

    // Reverse the string S
    S = S.split("").reverse().join("");

    // Stores the obtained number
    let M = 0;

    // Calculating the decimal value
    for (i = 0; i < 32; i++) {

        // Check for set bits
        if (S[i] == '1')
            M += (1 << i);
    }
    return M;
}

// Function to find the maximum value
// between N and the obtained number
function maximumOfTwo(N)
{
    let M = reverseBin(N);

    return Math.max(N, M);
}

// Driver Code
    let N = 6;
    document.write(maximumOfTwo(N));

</script>
```

**Output:** 

```
1610612736
```

***时间复杂度:**O(32)*
T5**辅助空间:** O(1)