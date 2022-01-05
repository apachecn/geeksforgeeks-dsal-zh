# 2 键键盘问题

> 原文:[https://www.geeksforgeeks.org/2-keys-keyboard-problem/](https://www.geeksforgeeks.org/2-keys-keyboard-problem/)

给定正整数 **N** 和一个[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 最初是**【A】**，任务是通过在每个步骤中执行以下操作之一，将形成由 **N** 个 **A 的**组成的串所需的操作次数降至最低:

*   复制字符串 **S** 中出现的所有字符。
*   将所有字符追加到上次复制的字符串 **S** 中。

**示例:**

> **输入:** N = 3
> **输出:** 3
> **说明:**
> 下面是执行的操作:
> **操作 1:** 复制初始字符串 S 一次，即“A”。
> **操作 2:** 将复制的字符串即“A”追加到字符串 S，将字符串 S 修改为“AA”。
> **操作 3:** 将复制的字符串即“A”追加到字符串 S，将字符串 S 修改为“AAA”。
> 因此，获得 3 A 所需的最小运算次数为 3。
> 
> **输入:**N = 7
> T3】输出: 7

**方法:**给定的问题可以基于以下观察来解决:

1.  如果**N = P<sub>1</sub>* P<sub>2</sub>* P<sub>m</sub>**其中 **{P <sub>1</sub> ，P <sub>2</sub> ，…，P <sub>m</sub> }** 为[质数](https://www.geeksforgeeks.org/prime-numbers/)则可以执行以下动作:
    1.  首先[复制字符串](https://www.geeksforgeeks.org/strcpy-in-c-cpp/)然后粘贴**(P<sub>1</sub>–1)**次。
    2.  同样，再次复制字符串并粘贴**(P<sub>2</sub>–1)**次。
    3.  用剩余的[质数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)执行 **M** 次，将得到 **A 的**的 **N** 号的字符串。
2.  因此，所需的最小移动总数由**(P<sub>1</sub>+P<sub>2</sub>+…+P<sub>m</sub>)**给出。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans** 为 **0** ，它存储运算的结果数。
*   [求给定整数 N 的素因子及其幂](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)。
*   现在，遍历**N**T3 的所有[素因子，并用](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)与其幂的乘积来增加 **ans** 的值。
*   最后，完成上述步骤后，打印**和**的值作为最终的最小移动次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of steps required to form N number
// of A's
int minSteps(int N)
{
    // Stores the count of steps needed
    int ans = 0;

    // Traverse over the range [2, N]
    for (int d = 2; d * d <= N; d++) {

        // Iterate while N is divisible
        // by d
        while (N % d == 0) {

            // Increment the value of
            // ans by d
            ans += d;

            // Divide N by d
            N /= d;
        }
    }

    // If N is not 1
    if (N != 1) {
        ans += N;
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    int N = 3;
    cout << minSteps(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG
{

    // Function to find the minimum number
    // of steps required to form N number
    // of A's
    static int minSteps(int N)
    {
        // Stores the count of steps needed
        int ans = 0;

        // Traverse over the range [2, N]
        for (int d = 2; d * d <= N; d++) {

            // Iterate while N is divisible
            // by d
            while (N % d == 0) {

                // Increment the value of
                // ans by d
                ans += d;

                // Divide N by d
                N /= d;
            }
        }

        // If N is not 1
        if (N != 1) {
            ans += N;
        }

        // Return the ans
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;
        minSteps(N);
        System.out.println(minSteps(N));
    }
}

// This code is contributed by lokesh potta.
```

## 蟒蛇 3

```
# Python3 program for the above approach
# Function to find the minimum number
# of steps required to form N number
# of A's
def minSteps( N):

    # Stores the count of steps needed
    ans = 0

    # Traverse over the range [2, N]
    d = 2
    while(d * d <= N):

        # Iterate while N is divisible
        # by d
        while (N % d == 0):

            # Increment the value of
            # ans by d
            ans += d

            # Divide N by d
            N /= d
        d += 1

    # If N is not 1
    if (N != 1):
        ans += N

    # Return the ans
    return ans

# Driver Code
N = 3
print(minSteps(N))

# This code is contributed by shivanisinghss2110   
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of steps required to form N number
// of A's
static int minSteps(int N)
{
    // Stores the count of steps needed
    int ans = 0;

    // Traverse over the range [2, N]
    for (int d = 2; d * d <= N; d++) {

        // Iterate while N is divisible
        // by d
        while (N % d == 0) {

            // Increment the value of
            // ans by d
            ans += d;

            // Divide N by d
            N /= d;
        }
    }

    // If N is not 1
    if (N != 1) {
        ans += N;
    }

    // Return the ans
    return ans;
}

// Driver Code
static public void Main ()
{

    int N = 3;
    Console.Write(minSteps(N));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript Program for the above approach
// Function to find the minimum number
    // of steps required to form N number
    // of A's
    function minSteps(N)
    {
        // Stores the count of steps needed
        var ans = 0;

        // Traverse over the range [2, N]
        for (var d = 2; d * d <= N; d++) {

            // Iterate while N is divisible
            // by d
            while (N % d == 0) {

                // Increment the value of
                // ans by d
                ans += d;

                // Divide N by d
                N /= d;
            }
        }

        // If N is not 1
        if (N != 1) {
            ans += N;
        }

        // Return the ans
        return ans;
    }

    // Driver Code
        var N = 3;
        minSteps(N);
        document.write(minSteps(N));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
3
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*