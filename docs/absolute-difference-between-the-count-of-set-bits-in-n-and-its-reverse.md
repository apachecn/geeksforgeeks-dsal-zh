# N 中设定位的计数与其倒数之间的绝对差值

> 原文:[https://www . geeksforgeeks . org/n 进制位数与反位数的绝对差值/](https://www.geeksforgeeks.org/absolute-difference-between-the-count-of-set-bits-in-n-and-its-reverse/)

给定一个整数 **N** ，任务是找出存在于数字**N**T5】和数字 N 相反的[中的](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)[设定位的数量之间的绝对差异](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/)

**示例:**

> **输入:** N = 13
> **输出:** 2
> **解释:**
> 二进制表示(13)<sub>10</sub>=(1101)<sub>2</sub>
> 设置位计数= 3
> 13 的倒数为 31
> 二进制表示(31)<sub>10</sub>=(11111)<sub>2【T19</sub>
> 
> **输入:** N = 135
> **输出:** 0
> **解释:**
> 二进制表示的(135)<sub>10</sub>=(10000111)<sub>2</sub>
> 集合比特数= 4
> 135 的倒数为 531
> 二进制表示的(531)<sub>10</sub>=(10000000)

**方法:**主要思路是使用 [STL 库](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)的[位集功能](https://www.geeksforgeeks.org/c-bitset-and-its-application/)。

按照以下步骤解决给定的问题:

1.  [反转数字 **N**](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/) 的数字并将其存储在变量中，比如 **revN** 。
2.  使用[位设置](https://www.geeksforgeeks.org/c-bitset-and-its-application/)功能[统计**N**T5 中的设置位数。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
3.  返回 **N** 和 **revN** 中设定位数的绝对差值。

下面是上述方法的实现:

## C++14

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// reverse number of N
int reverse(int N)
{
    // Stores the
    // reverse of N
    int revn = 0;

    // Iterate while N exceeds 0
    while (N > 0) {
        // Extract last digit of N
        int b = N % 10;

        // Append the last digit
        // of N to revn
        revn = (revn * 10) + b;

        // Remove the last digit of N
        N = N / 10;
    }

    return revn;
}

// Function to find the absolute difference
// between the set bits in N and its reverse
int findAbsoluteDiffernce(int N)
{
    // Store N as bitset
    bitset<64> a(N);

    // Stores the reverse of N
    int revn = reverse(N);

    // Stores revn as bitset
    bitset<64> b(revn);

    // Count set bits in N
    int setBitsInN = a.count();

    // Count set bits in revn
    int setBitsInRevN = b.count();

    // Return the absolute difference of
    // set bits in N and its reverse
    return abs(setBitsInN - setBitsInRevN);
}

// Driver Code
int main()
{
    // Input
    int N = 13;

    // Function call to find absolute
    // difference between the count
    // of set bits in N and its reverse
    cout << findAbsoluteDiffernce(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the
// reverse number of N
static int reverse(int N)
{

    // Stores the
    // reverse of N
    int revn = 0;

    // Iterate while N exceeds 0
    while (N > 0)
    {

        // Extract last digit of N
        int b = N % 10;

        // Append the last digit
        // of N to revn
        revn = (revn * 10) + b;

        // Remove the last digit of N
        N = N / 10;
    }
    return revn;
}

// Function to find the absolute difference
// between the set bits in N and its reverse
static int findAbsoluteDiffernce(int N)
{

    // Count set bits in N
    int setBitsInN = Integer.bitCount(N);

    // Stores the reverse of N
    int revn = reverse(N);

    // Count set bits in revn
    int setBitsInRevN = Integer.bitCount(revn);

    // Return the absolute difference of
    // set bits in N and its reverse
    return Math.abs(setBitsInN - setBitsInRevN);
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 13;

    // Function call to find absolute
    // difference between the count
    // of set bits in N and its reverse
    System.out.println(findAbsoluteDiffernce(N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the
# reverse number of N
def reverse(N):

    # Stores the
    # reverse of N
    revn = 0

    # Iterate while N exceeds 0
    while (N > 0):

        # Extract last digit of N
        b = N % 10

        # Append the last digit
        # of N to revn
        revn = (revn * 10) + b

        # Remove the last digit of N
        N = N // 10

    return revn

def countSetBits(n):

    count = 0

    while n:
        count += (n & 1)
        n >>= 1

    return count

# Function to find the absolute difference
# between the set bits in N and its reverse
def findAbsoluteDiffernce(N):

    # Count set bits in N
    setBitsInN = countSetBits(N)

    # Stores the reverse of N
    revn = reverse(N)

    # Count set bits in revn
    setBitsInRevN = countSetBits(revn)

    # Return the absolute difference of
    # set bits in N and its reverse
    return abs(setBitsInN - setBitsInRevN)

# Driver Code

# Input
N = 13

# Function call to find absolute
# difference between the count
# of set bits in N and its reverse
print(findAbsoluteDiffernce(N))

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the
// reverse number of N
static int reverse(int N)
{

    // Stores the
    // reverse of N
    int revn = 0;

    // Iterate while N exceeds 0
    while (N > 0)
    {

        // Extract last digit of N
        int b = N % 10;

        // Append the last digit
        // of N to revn
        revn = (revn * 10) + b;

        // Remove the last digit of N
        N = N / 10;
    }
    return revn;
}

// Function to get no of set
// bits in binary representation
// of positive integer n
static int countSetBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Function to find the absolute difference
// between the set bits in N and its reverse
static int findAbsoluteDiffernce(int N)
{

    // Count set bits in N
    int setBitsInN = countSetBits(N);

    // Stores the reverse of N
    int revn = reverse(N);

    // Count set bits in revn
    int setBitsInRevN = countSetBits(revn);

    // Return the absolute difference of
    // set bits in N and its reverse
    return Math.Abs(setBitsInN - setBitsInRevN);
}

// Driver Code
public static void Main(string[] args)
{

    // Input
    int N = 13;

    // Function call to find absolute
    // difference between the count
    // of set bits in N and its reverse
    Console.WriteLine(findAbsoluteDiffernce(N));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

        // Javascript program for the
        // above approach

        // Function to find the
        // reverse number of N
        function reverse( n ) {
        // converting the number to String
            n = n + "";

       // splitting the digits into an array
            let arr = n.split("")

      // reversing the array
            let revn = arr.reverse()

            //joining all in a single string
            return revn.join("");
        }

        // Function to find
        // the absolute difference
        // between the set bits in N
        // and its reverse
        function findAbsoluteDiffernce(N) {

            // Count set bits in N
            let setBitsInN =
            N.toString(2).split('1').length - 1

            // Stores the reverse of N
            let revn = reverse(N);

            // Count set bits in revn
            let setBitsInRevN =
            revn.toString(2).split('1').length - 1

            // Return the absolute difference of
            // set bits in N and its reverse
            return Math.abs(setBitsInN - setBitsInRevN);
        }

        // Driver Code

        // Input
        let N = 13;

        // Function call to find absolute
        // difference between the count
        // of set bits in N and its reverse
        document.write(findAbsoluteDiffernce(N))

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*