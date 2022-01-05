# 前 N 个自然数的二进制表示的小数总和

> 原文:[https://www . geeksforgeeks . org/十进制数之和-第一个 n 个自然数的二进制表示/](https://www.geeksforgeeks.org/sum-of-decimals-that-are-binary-representations-of-first-n-natural-numbers/)

给定一个正整数 **N** ，任务是计算所有小数的和，可以表示为[第一个 **N** 自然数](https://www.geeksforgeeks.org/sum-of-natural-numbers-using-recursion/)的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)。

**示例:**

> **输入:** N = 3
> **输出:** 22
> **解释:**
> 1 的二进制表示为 01。
> 2 的二进制表示是 10。
> 3 的二进制表示是 11。
> 因此，要求总和= 01 + 10 + 11 = 22。
> 
> **输入:**N = 5
> T3】输出: 223

**天真方法:**解决问题最简单的方法是[在范围**【1，N】**上迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，在每次迭代中把[当前数转换成它的二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)[并加到总和](https://www.geeksforgeeks.org/sum-two-large-numbers/)上。将所有数字相加后，打印总和作为结果。

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(32)*

**有效方法:**上述方法也可以通过找到与 **N** 位置不相同的[最高有效位(MSB)](https://www.geeksforgeeks.org/find-significant-set-bit-number/) 的数字的贡献，然后找到其余数字的 MSB 的贡献来优化。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 **0** 来存储前 N 个自然数的二进制表示中所有数字的和。
*   [迭代至](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)**N**的值至少为**0**，执行以下步骤:
    *   将数字 **N** 的 [MSB 位置存储在变量 **X** 中，将**2<sup>(X–1)</sup>**<sup>的值存储在变量中，比如 **A** 。</sup>](https://www.geeksforgeeks.org/find-significant-set-bit-number/)
    *   初始化一个变量，将**曲线**设为 **0** ，以存储与 **N** 不具有相同 MSB 位置的数字的贡献。
    *   [迭代范围](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)**【1，X】**，在每次迭代中，将 **A** 加到变量 **cur** 上，然后将 **A** 乘以 **10** 。
    *   完成上述步骤后，将 **cur** 的值添加到 **ans** 并将变量 **rem** 中的剩余元素存储为**(N–2<sup>X</sup>+1)**。
    *   通过将**(雷姆* 10 <sup>X</sup> )** 加到 **ans** 上，将其余数字的 [MSB](https://www.geeksforgeeks.org/find-significant-set-bit-number/) 的贡献相加。
    *   将 **N** 的值更新为**(rem–1)**进行下一次迭代。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
const int MOD = 1e9 + 7;

// Function to find the sum of first
// N natural numbers represented
// in binary representation
void sumOfBinaryNumbers(int n)
{
    // Stores the resultant sum
    int ans = 0;

    int one = 1;

    // Iterate until the value of
    // N is greater than 0
    while (1) {

        // If N is less than 2
        if (n <= 1) {
            ans = (ans + n) % MOD;
            break;
        }

        // Store the MSB position of N
        int x = log2(n);

        int cur = 0;
        int add = (one << (x - 1));

        // Iterate in the range [1, x]
        // and add the contribution of
        // the  numbers from 1 to (2^x-1)
        for (int i = 1; i <= x; i++) {

            // Update the value of the
            // cur and add
            cur = (cur + add) % MOD;
            add = (add * 10 % MOD);
        }

        // Add the cur to ans
        ans = (ans + cur) % MOD;

        // Store the remaining numbers
        int rem = n - (one << x) + 1;

        // Add the contribution by MSB
        // by the remaining numbers
        int p = pow(10, x);
        p = (p * (rem % MOD)) % MOD;
        ans = (ans + p) % MOD;

        // The next iteration will
        // be repeated for 2^x - 1
        n = rem - 1;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int N = 3;
    sumOfBinaryNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/// Java program for the above approach
import java.io.*;
import java.lang.*;

class GFG
{
    static final int MOD = 1000000007;

    // Function to find the sum of first
    // N natural numbers represented
    // in binary representation
    static void sumOfBinaryNumbers(int n)
    {

        // Stores the resultant sum
        int ans = 0;

        int one = 1;

        // Iterate until the value of
        // N is greater than 0
        while (true) {

            // If N is less than 2
            if (n <= 1) {
                ans = (ans + n) % MOD;
                break;
            }

            // Store the MSB position of N
            int x = (int)(Math.log(n) / Math.log(2));

            int cur = 0;
            int add = (int)(Math.pow(2, (x - 1)));

            // Iterate in the range [1, x]
            // and add the contribution of
            // the  numbers from 1 to (2^x-1)
            for (int i = 1; i <= x; i++) {

                // Update the value of the
                // cur and add
                cur = (cur + add) % MOD;
                add = (add * 10 % MOD);
            }

            // Add the cur to ans
            ans = (ans + cur) % MOD;

            // Store the remaining numbers
            int rem = n - (int)(Math.pow(2, x)) + 1;

            // Add the contribution by MSB
            // by the remaining numbers
            int p = (int)Math.pow(10, x);
            p = (p * (rem % MOD)) % MOD;
            ans = (ans + p) % MOD;

            // The next iteration will
            // be repeated for 2^x - 1
            n = rem - 1;
        }

        // Print the result
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;

        sumOfBinaryNumbers(N);
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2, pow

MOD = 1000000007

# Function to find the sum of first
# N natural numbers represented
# in binary representation
def sumOfBinaryNumbers(n):

    # Stores the resultant sum
    ans = 0

    one = 1

    # Iterate until the value of
    # N is greater than 0
    while (1):

        # If N is less than 2
        if (n <= 1):
            ans = (ans + n) % MOD
            break

        # Store the MSB position of N
        x = int(log2(n))

        cur = 0
        add = (one << (x - 1))

        # Iterate in the range [1, x]
        # and add the contribution of
        # the  numbers from 1 to (2^x-1)
        for i in range(1, x + 1, 1):

            # Update the value of the
            # cur and add
            cur = (cur + add) % MOD
            add = (add * 10 % MOD)

        # Add the cur to ans
        ans = (ans + cur) % MOD

        # Store the remaining numbers
        rem = n - (one << x) + 1

        # Add the contribution by MSB
        # by the remaining numbers
        p = pow(10, x)
        p = (p * (rem % MOD)) % MOD
        ans = (ans + p) % MOD

        # The next iteration will
        # be repeated for 2^x - 1
        n = rem - 1

    # Print the result
    print(int(ans))

# Driver Code
if __name__ == '__main__':

    N = 3

    sumOfBinaryNumbers(N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
class GFG{

const int MOD = 1000000007;

// Function to find the sum of first
// N natural numbers represented
// in binary representation
static void sumOfBinaryNumbers(int n)
{

    // Stores the resultant sum
    int ans = 0;

    int one = 1;

    // Iterate until the value of
    // N is greater than 0
    while (true)
    {

        // If N is less than 2
        if (n <= 1)
        {
            ans = (ans + n) % MOD;
            break;
        }

        // Store the MSB position of N
        int x = (int)Math.Log(n, 2);

        int cur = 0;
        int add = (one << (x - 1));

        // Iterate in the range [1, x]
        // and add the contribution of
        // the  numbers from 1 to (2^x-1)
        for(int i = 1; i <= x; i++)
        {

            // Update the value of the
            // cur and add
            cur = (cur + add) % MOD;
            add = (add * 10 % MOD);
        }

        // Add the cur to ans
        ans = (ans + cur) % MOD;

        // Store the remaining numbers
        int rem = n - (one << x) + 1;

        // Add the contribution by MSB
        // by the remaining numbers
        int p = (int)Math.Pow(10, x);
        p = (p * (rem % MOD)) % MOD;
        ans = (ans + p) % MOD;

        // The next iteration will
        // be repeated for 2^x - 1
        n = rem - 1;
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{
    int N = 3;

    sumOfBinaryNumbers(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

let MOD = 1000000007;

    // Function to find the sum of first
    // N natural numbers represented
    // in binary representation
    function sumOfBinaryNumbers(n)
    {

        // Stores the resultant sum
        let ans = 0;

        let one = 1;

        // Iterate until the value of
        // N is greater than 0
        while (true) {

            // If N is less than 2
            if (n <= 1) {
                ans = (ans + n) % MOD;
                break;
            }

            // Store the MSB position of N
            let x = Math.floor(Math.log(n) / Math.log(2));

            let cur = 0;
            let add = Math.floor(Math.pow(2, (x - 1)));

            // Iterate in the range [1, x]
            // and add the contribution of
            // the  numbers from 1 to (2^x-1)
            for (let i = 1; i <= x; i++) {

                // Update the value of the
                // cur and add
                cur = (cur + add) % MOD;
                add = (add * 10 % MOD);
            }

            // Add the cur to ans
            ans = (ans + cur) % MOD;

            // Store the remaining numbers
            let rem = n - Math.floor(Math.pow(2, x)) + 1;

            // Add the contribution by MSB
            // by the remaining numbers
            let p = Math.floor(Math.pow(10, x));
            p = (p * (rem % MOD)) % MOD;
            ans = (ans + p) % MOD;

            // The next iteration will
            // be repeated for 2^x - 1
            n = rem - 1;
        }

        // Print the result
         document.write(ans);
    }

// Driver code

    let N = 3;

    sumOfBinaryNumbers(N);

</script>
```

**Output:** 

```
22
```

**时间复杂度:**O(log N)
T3】辅助空间: O(1)