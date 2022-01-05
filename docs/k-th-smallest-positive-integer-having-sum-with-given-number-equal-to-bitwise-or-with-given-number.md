# 第 K 个最小正整数，给定数的和等于给定数的按位“或”

> 原文:[https://www . geesforgeks . org/k-th-最小正整数-具有给定数的和-等于给定数的按位或/](https://www.geeksforgeeks.org/k-th-smallest-positive-integer-having-sum-with-given-number-equal-to-bitwise-or-with-given-number/)

给定两个正整数 **X** 和 **K** ，任务是找到第**K**-个最小正整数 **Y、**，使得 **X + Y = X | Y** ，其中|表示 [**<u>按位“或”运算。</u>**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

**示例:**

> **输入:** X = 5，K = 1
> **输出:** 2
> **说明:**第一个数字是 2 as (2 + 5 = 2 | 5)
> 
> **输入:** X = 5，K = 5
> **输出:** 18
> **说明:**正确值列表为 2，8，10，16，18。第五个数字是这个列表是 18

**方法:**给定问题可以通过以下步骤解决:

*   让最终值为 **Y** 。从 [**<u>属性的按位运算，</u>**](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/) 可知 **X + Y = X & Y + X | Y** ，其中&是两个数的按位 AND
*   要使问题陈述中的等式为真， **X & Y** 的值必须为 0
*   因此，对于所有位置，如果第 I 位在 **X** 中为开，那么对于 Y 的所有可能解，它必须为关
*   例如，如果二进制的 **X** = 1001101001(十进制的 617)，那么 Y 的最后十位必须是 **Y** = 0**00*0**0，其中‘*’表示 0 或 1。此外，我们可以在数字的开头填充任意数量的数字，因为所有高位都是零
*   所以最终的解决方案是将所有位可以为 0 或 1 的位置视为从左到右的序列，并找到 **K** 的二进制表示法。
*   按照 **K** 的二进制记数法填充所有位置

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate K-th smallest
// solution(Y) of equation X+Y = X|Y
long long KthSolution(long long X, long long K)
{
    // Initialize the variable
    // to store the answer
    long long ans = 0;

    for (int i = 0; i < 64; i++) {

        // The i-th bit of X is off
        if (!(X & (1LL << i))) {

            // The i-bit of K is on
            if (K & 1) {
                ans |= (1LL << i);
            }

            // Divide K by 2
            K >>= 1;

            // If K becomes 0 then break
            if (!K) {
                break;
            }
        }
    }
    return ans;
}
// Driver Code
int main()
{
    long long X = 5, K = 5;
    cout << KthSolution(X, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to calculate K-th smallest
    // solution(Y) of equation X+Y = X|Y
    static long KthSolution(long X, long K)
    {

        // Initialize the variable
        // to store the answer
        long ans = 0;

        for (int i = 0; i < 64; i++) {

            // The i-th bit of X is off
            if ((X & (1 << i)) == 0) {

                // The i-bit of K is on
                if ((K & 1) > 0) {
                    ans |= (1 << i);
                }

                // Divide K by 2
                K >>= 1;

                // If K becomes 0 then break
                if (K == 0) {
                    break;
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
         long X = 5, K = 5;
        System.out.println(KthSolution(X, K));
    }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to calculate K-th smallest
# solution(Y) of equation X+Y = X|Y
def KthSolution(X, K):

    # Initialize the variable
    # to store the answer
    ans = 0

    for i in range(0, 64):

        # The i-th bit of X is off
        if (not (X & (1 << i))):

            # The i-bit of K is on
            if (K & 1):
                ans |= (1 << i)

            # Divide K by 2
            K >>= 1

            # If K becomes 0 then break
            if (not K):
                break

    return ans

# Driver Code
if __name__ == "__main__":

    X = 5
    K = 5
    print(KthSolution(X, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

    // Function to calculate K-th smallest
    // solution(Y) of equation X+Y = X|Y
    static long KthSolution(long X, long K)
    {
        // Initialize the variable
        // to store the answer
        long ans = 0;

        for (int i = 0; i < 64; i++) {

            // The i-th bit of X is off
            if ((X & (1LL << i)) == 0) {

                // The i-bit of K is on
                if ((K & 1) > 0) {
                    ans |= (1LL << i);
                }

                // Divide K by 2
                K >>= 1;

                // If K becomes 0 then break
                if (K == 0) {
                    break;
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        long X = 5, K = 5;
        Console.Write(KthSolution(X, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to calculate K-th smallest
        // solution(Y) of equation X+Y = X|Y
        function KthSolution(X, K)
        {

            // Initialize the variable
            // to store the answer
            let ans = 0;

            for (let i = 0; i < 64; i++) {

                // The i-th bit of X is off
                if (!(X & (1 << i))) {

                    // The i-bit of K is on
                    if (K & 1) {
                        ans |= (1 << i);
                    }

                    // Divide K by 2
                    K >>= 1;

                    // If K becomes 0 then break
                    if (!K) {
                        break;
                    }
                }
            }
            return ans;
        }

        // Driver Code
        let X = 5, K = 5;
        document.write(KthSolution(X, K));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
18
```

**时间复杂度:** O(log(N))
**辅助空间:** O(1)