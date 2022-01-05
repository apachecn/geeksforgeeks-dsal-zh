# 求最小正数 Y，使 X 和 Y 的位“与”为零

> 原文:[https://www . geeksforgeeks . org/find-minist-正数-y-so-x 和-y 的按位运算等于零/](https://www.geeksforgeeks.org/find-smallest-positive-number-y-such-that-bitwise-and-of-x-and-y-is-zero/)

给定一个整数 **X** 。任务是找到最小的正数 **Y** ( > 0)，使得 **X** [和](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) **Y** 为零**。
**示例:**** 

> ****输入:** X = 3
> **输出:** 4
> 4 是最小正数，其与 3 的按位 AND 为零
> **输入:** X = 10
> **输出:** 1**

****途径:**T2【有 2 例:** 

*   **如果 **X** 的二进制表示包含全 1，那么 **Y** 的所有位都应该是 **0** ，使**和**运算的结果为零。那么 **X+1** 就是我们的答案，也就是第一个正整数。** 
*   **如果 **X** 的二进制表示不包含全 1，那么在 **X** 中找到第一个位置，该位置的位是 **0** 。那么我们的答案将是**功率(2，位置)**** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program to find smallest number Y for
// a given value of X such that X AND Y is zero
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Method to find smallest number Y for
// a given value of X such that X AND Y is zero
int findSmallestNonZeroY(int A_num)
{

    // Convert the number into its binary form
    string A_binary = bitset<8>(A_num).to_string();
    int B = 1;
    int length = A_binary.size();
    int no_ones = __builtin_popcount(A_num);

    // Case 1 : If all bits are ones,
    // then return the next number
    if (length == no_ones )
        return A_num + 1;

    // Case 2 : find the first 0-bit
    // index and return the Y
    for (int i=0;i<length;i++)
    {
            char ch = A_binary[length - i - 1];

            if (ch == '0')
            {
                B = pow(2.0, i);
                break;
            }
        }
    return B;
}

// Driver Code
int main()
{
    int X = findSmallestNonZeroY(10);
    cout << X;
}

// This code is contributed by mohit kumar 29
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find smallest number Y for
// a given value of X such that X AND Y is zero
import java.lang.*;

public class Main {

    // Method to find smallest number Y for
    // a given value of X such that X AND Y is zero
    static long findSmallestNonZeroY(long A_num)
    {
        // Convert the number into its binary form
        String A_binary = Long.toBinaryString(A_num);
        long B = 1;
        int len = A_binary.length();
        int no_ones = Long.bitCount(A_num);

        // Case 1 : If all bits are ones,
        // then return the next number
        if (len == no_ones) {
            return A_num + 1;
        }

        // Case 2 : find the first 0-bit
        // index and return the Y
        for (int i = 0; i < len; i++) {
            char ch = A_binary.charAt(len - i - 1);
            if (ch == '0') {
                B = (long)Math.pow(2.0, (double)i);
                break;
            }
        }
        return B;
    }

    // Driver code
    public static void main(String[] args)
    {
        long X = findSmallestNonZeroY(10);
        System.out.println(X);
    }
}
```

## **蟒蛇 3**

```
# Python3 program to find smallest number Y for
# a given value of X such that X AND Y is zero

# Method to find smallest number Y for
# a given value of X such that X AND Y is zero
def findSmallestNonZeroY(A_num) :

    # Convert the number into its binary form
    A_binary = bin(A_num)
    B = 1
    length = len(A_binary);
    no_ones = (A_binary).count('1');

    # Case 1 : If all bits are ones,
    # then return the next number
    if length == no_ones :
        return A_num + 1;

    # Case 2 : find the first 0-bit
    # index and return the Y
    for i in range(length) :
            ch = A_binary[length - i - 1];

            if (ch == '0') :
                B = pow(2.0, i);
                break;

    return B;

# Driver Code
if __name__ == "__main__" :
    X = findSmallestNonZeroY(10);
    print(X)

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# program to find smallest number Y for
// a given value of X such that X AND Y is zero
using System;

class GFG
{

    // Method to find smallest number Y for
    // a given value of X such that X AND Y is zero
    static long findSmallestNonZeroY(long A_num)
    {
        // Convert the number into its binary form
        String A_binary = Convert.ToString(A_num, 2);
        long B = 1;
        int len = A_binary.Length;
        int no_ones = bitCount(A_num);

        // Case 1 : If all bits are ones,
        // then return the next number
        if (len == no_ones)
        {
            return A_num + 1;
        }

        // Case 2 : find the first 0-bit
        // index and return the Y
        for (int i = 0; i < len; i++)
        {
            char ch = A_binary[len - i - 1];
            if (ch == '0')
            {
                B = (long)Math.Pow(2.0, (double)i);
                break;
            }
        }
        return B;
    }

    static int bitCount(long x)
    {
        // To store the count
        // of set bits
        int setBits = 0;
        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }
        return setBits;
    }

    // Driver code
    public static void Main(String[] args)
    {
        long X = findSmallestNonZeroY(10);
        Console.WriteLine(X);
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// Javascript program to find smallest number Y for
// a given value of X such that X AND Y is zero

// Method to find smallest number Y for
    // a given value of X such that X AND Y is zero
function findSmallestNonZeroY(A_num)
{
    // Convert the number into its binary form
        let A_binary = (A_num >>> 0).toString(2);
        let B = 1;
        let len = A_binary.length;
        let no_ones = bitCount(A_num);

        // Case 1 : If all bits are ones,
        // then return the next number
        if (len == no_ones) {
            return A_num + 1;
        }

        // Case 2 : find the first 0-bit
        // index and return the Y
        for (let i = 0; i < len; i++) {
            let ch = A_binary[len - i - 1];
            if (ch == '0') {
                B = Math.floor(Math.pow(2.0, i));
                break;
            }
        }
        return B;
}
function bitCount(x)
{
    // To store the count
        // of set bits
        let setBits = 0;
        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }
        return setBits;
}

// Driver code
let X = findSmallestNonZeroY(10);
document.write(X);

// This code is contributed by unknown2108
</script>
```

****Output:** 

```
1
```** 

****时间复杂度:**O(1)
T3】辅助空间: O(1)**