# 将给定数字的数字旋转 K

> 原文:[https://www . geesforgeks . org/rotate-digits-of-a-number-by-k/](https://www.geeksforgeeks.org/rotate-digits-of-a-given-number-by-k/)

给定两个整数 **N** 和 **K** ，任务是将 **N** 的位数旋转 K，如果 **K** 是正整数，向左旋转其位数。否则，向右旋转它的数字。

**示例:**

> **输入:** N = 12345，K = 2
> **输出:** 34512
> **解释:**
> 向左旋转 N(= 12345)乘以 K(= 2)将 N 修改为 34512。
> 因此，需要的输出是 34512
> 
> **输入:** N = 12345，K = -3
> **输出:** 34512
> **解释:**
> 右旋转 N(= 12345)乘 K( = -3)将 N 修改为 34512。
> 因此，需要的输出是 34512

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **X** ，将位数存储在 **N** 中。
*   更新 **K = (K + X) % X** 将其简化为左旋转的情况。
*   删除 **N** 的第一个 **K** 数字，并将所有删除的数字追加到 **N** 数字的右侧。
*   最后，打印 **N** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// digits in N
int numberOfDigit(int N)
{

    // Stores count of
    // digits in N
    int digit = 0;

    // Calculate the count
    // of digits in N
    while (N > 0) {

        // Update digit
        digit++;

        // Update N
        N /= 10;
    }
    return digit;
}

// Function to rotate the digits of N by K
void rotateNumberByK(int N, int K)
{

    // Stores count of digits in N
    int X = numberOfDigit(N);

    // Update K so that only need to
    // handle left rotation
    K = ((K % X) + X) % X;

    // Stores first K digits of N
    int left_no = N / (int)(pow(10, X - K));

    // Remove first K digits of N
    N = N % (int)(pow(10, X - K));

    // Stores count of digits in left_no
    int left_digit = numberOfDigit(left_no);

    // Append left_no to the right of
    // digits of N
    N = (N * (int)(pow(10, left_digit))) + left_no;
    cout << N;
}

// Driver code
int main()
{
    int N = 12345, K = 7;

    // Function Call
    rotateNumberByK(N, K);
    return 0;
}

// The code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;

class GFG {

    // Function to find the count of
    // digits in N
    static int numberOfDigit(int N)
    {

        // Stores count of
        // digits in N
        int digit = 0;

        // Calculate the count
        // of digits in N
        while (N > 0) {

            // Update digit
            digit++;

            // Update N
            N /= 10;
        }
        return digit;
    }

    // Function to rotate the digits of N by K
    static void rotateNumberByK(int N, int K)
    {

        // Stores count of digits in N
        int X = numberOfDigit(N);

        // Update K so that only need to
        // handle left rotation
        K = ((K % X) + X) % X;

        // Stores first K digits of N
        int left_no = N / (int)(Math.pow(10,
                                         X - K));

        // Remove first K digits of N
        N = N % (int)(Math.pow(10, X - K));

        // Stores count of digits in left_no
        int left_digit = numberOfDigit(left_no);

        // Append left_no to the right of
        // digits of N
        N = (N * (int)(Math.pow(10, left_digit)))
            + left_no;

        System.out.println(N);
    }

    // Driver Code
    public static void main(String args[])
    {

        int N = 12345, K = 7;

        // Function Call
        rotateNumberByK(N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the count of
# digits in N
def numberOfDigit(N):

    # Stores count of
    # digits in N
    digit = 0

    # Calculate the count
    # of digits in N
    while (N > 0):

        # Update digit
        digit += 1

        # Update N
        N //= 10
    return digit

# Function to rotate the digits of N by K
def rotateNumberByK(N, K):

    # Stores count of digits in N
    X = numberOfDigit(N)

    # Update K so that only need to
    # handle left rotation
    K = ((K % X) + X) % X

    # Stores first K digits of N
    left_no = N // pow(10, X - K)

    # Remove first K digits of N
    N = N % pow(10, X - K)

    # Stores count of digits in left_no
    left_digit = numberOfDigit(left_no)

    # Append left_no to the right of
    # digits of N
    N = N * pow(10, left_digit) + left_no
    print(N)

# Driver Code
if __name__ == '__main__':
    N, K = 12345, 7

    # Function Call
    rotateNumberByK(N, K)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to find the count of
    // digits in N
    static int numberOfDigit(int N)
    {

        // Stores count of
        // digits in N
        int digit = 0;

        // Calculate the count
        // of digits in N
        while (N > 0)
        {

            // Update digit
            digit++;

            // Update N
            N /= 10;
        }
        return digit;
    }

    // Function to rotate the digits of N by K
    static void rotateNumberByK(int N, int K)
    {

        // Stores count of digits in N
        int X = numberOfDigit(N);

        // Update K so that only need to
        // handle left rotation
        K = ((K % X) + X) % X;

        // Stores first K digits of N
        int left_no = N / (int)(Math.Pow(10,
                                         X - K));

        // Remove first K digits of N
        N = N % (int)(Math.Pow(10, X - K));

        // Stores count of digits in left_no
        int left_digit = numberOfDigit(left_no);

        // Append left_no to the right of
        // digits of N
        N = (N * (int)(Math.Pow(10, left_digit)))
            + left_no;

        Console.WriteLine(N);
    }

    // Driver Code
    public static void Main(string []args)
    {

        int N = 12345, K = 7;

        // Function Call
        rotateNumberByK(N, K);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to find the count of
    // digits in N
    function numberOfDigit(N)
    {

        // Stores count of
        // digits in N
        let digit = 0;

        // Calculate the count
        // of digits in N
        while (N > 0) {

            // Update digit
            digit++;

            // Update N
            N = Math.floor( N / 10);
        }
        return digit;
    }

    // Function to rotate the digits of N by K
    function rotateNumberByK(N, K)
    {

        // Stores count of digits in N
        let X = numberOfDigit(N);

        // Update K so that only need to
        // handle left rotation
        K = ((K % X) + X) % X;

        // Stores first K digits of N
        let left_no = Math.floor (N / Math.floor(Math.pow(10,
                                         X - K)));

        // Remove first K digits of N
        N = N % Math.floor(Math.pow(10, X - K));

        // Stores count of digits in left_no
        let left_digit = numberOfDigit(left_no);

        // Append left_no to the right of
        // digits of N
        N = (N * Math.floor(Math.pow(10, left_digit)))
            + left_no;

        document.write(N);
    }

// Driver Code

    let N = 12345, K = 7;

        // Function Call
        rotateNumberByK(N, K);

  // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
34512
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*