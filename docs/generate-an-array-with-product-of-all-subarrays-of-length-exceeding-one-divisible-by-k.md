# 生成长度超过 1 的所有子阵列的乘积可被 K 整除的数组

> 原文:[https://www . geeksforgeeks . org/生成长度超过 1 的所有子阵列的乘积的数组，可被 k 整除/](https://www.geeksforgeeks.org/generate-an-array-with-product-of-all-subarrays-of-length-exceeding-one-divisible-by-k/)

给定两个正整数 **N** 和 **K** ，任务是生成一个长度为 **N** 的数组，使得长度大于 **1** 的每个子数组[的乘积必须能被 **K** 整除，数组](https://www.geeksforgeeks.org/product-of-all-subarrays-of-an-array/)的[最大元素必须小于 **K** 。如果没有这样的数组，则打印 **-1** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** N = 3，K = 20
> **输出:** {15，12，5}
> **说明:**所有长度大于 1 的子阵都是{15，12}，{12，5}，{15，12，5}它们对应的乘积是 180，60，900，都可以被 20 整除。
> 
> **输入:** N = 4，K = 100
> **输出:** {90，90，90，90}

**方法:**给定的问题可以通过以下观察来解决:

> 可以观察到，通过使长度为 **2** 的每个子阵列的积被 **K** 整除，长度大于 **2** 的每个子阵列的积将自动被 **K** 整除。

所以想法是取 **K** 的两个除数，说 **d1** 和 **d2** ，这样 **d1 * d2 = K** 在数组中交替放置。按照以下步骤解决问题:

1.  初始化两个整数变量 **d1** 和 **d2** 。
2.  [检查 K 是否为质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果发现是真的，打印 **-1** 。
3.  否则，计算 **K** 的除数，并将两个除数存储在 **d1** 和 **d2** 中。
4.  之后，从 **i = 0 到 N–1**进行遍历。
5.  如果 **i** 为偶数，打印 **d1** 。否则，打印 **d2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to check if the required
// array can be generated or not
void array_divisbleby_k(int N, int K)
{
    // To check if divisor exists
    bool flag = false;

    // To store divisiors of K
    int d1, d2;

    // Check if K is prime or not
    for (int i = 2; i * i <= K; i++) {

        if (K % i == 0) {
            flag = true;
            d1 = i;
            d2 = K / i;
            break;
        }
    }

    // If array can be generated
    if (flag) {

        // Print d1 and d2 alternatively
        for (int i = 0; i < N; i++) {

            if (i % 2 == 1) {
                cout << d2 << " ";
            }
            else {
                cout << d1 << " ";
            }
        }
    }

    else {

        // No such array can be generated
        cout << -1;
    }
}
// Driver Code
int main()
{
    // Given N and K
    int N = 5, K = 21;

    // Function Call
    array_divisbleby_k(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the required
// array can be generated or not
public static void array_divisbleby_k(int N,
                                      int K)
{

    // To check if divisor exists
    boolean flag = false;

    // To store divisiors of K
    int d1 = 0, d2 = 0;

    // Check if K is prime or not
    for(int i = 2; i * i <= K; i++)
    {
        if (K % i == 0)
        {
            flag = true;
            d1 = i;
            d2 = K / i;
            break;
        }
    }

    // If array can be generated
    if (flag)
    {

        // Print d1 and d2 alternatively
        for(int i = 0; i < N; i++)
        {
            if (i % 2 == 1)
            {
                System.out.print(d2 + " ");
            }
            else
            {
                System.out.print(d1 + " ");
            }
        }
    }

    else
    {

        // No such array can be generated
        System.out.print(-1);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 5, K = 21;

    // Function Call
    array_divisbleby_k(N, K);
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the required
# array can be generated or not
def array_divisbleby_k(N, K):

    # To check if divisor exists
    flag = False

    # To store divisiors of K
    d1, d2 = 0, 0

    # Check if K is prime or not
    for i in range(2, int(K ** (1 / 2)) + 1):
        if (K % i == 0):
            flag = True
            d1 = i
            d2 = K // i
            break

    # If array can be generated
    if (flag):

        # Print d1 and d2 alternatively
        for i in range(N):
            if (i % 2 == 1):
                print(d2, end = " ")
            else:
                print(d1, end = " ")

    else:

        # No such array can be generated
        print(-1)

# Driver Code
if __name__ == "__main__":

    # Given N and K
    N = 5
    K = 21

    # Function Call
    array_divisbleby_k(N, K)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the required
// array can be generated or not
public static void array_divisbleby_k(int N,
                                      int K)
{

    // To check if divisor exists
    bool flag = false;

    // To store divisiors of K
    int d1 = 0, d2 = 0;

    // Check if K is prime or not
    for(int i = 2; i * i <= K; i++)
    {
        if (K % i == 0)
        {
            flag = true;
            d1 = i;
            d2 = K / i;
            break;
        }
    }

    // If array can be generated
    if (flag)
    {

        // Print d1 and d2 alternatively
        for(int i = 0; i < N; i++)
        {
            if (i % 2 == 1)
            {
                Console.Write(d2 + " ");
            }
            else
            {
                Console.Write(d1 + " ");
            }
        }
    }

    else
    {

        // No such array can be generated
        Console.Write(-1);
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given N and K
    int N = 5, K = 21;

    // Function Call
    array_divisbleby_k(N, K);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if the required
    // array can be generated or not
    function array_divisbleby_k(N, K)
    {

        // To check if divisor exists
        let flag = false;

        // To store divisiors of K
        let d1 = 0, d2 = 0;

        // Check if K is prime or not
        for(let i = 2; i * i <= K; i++)
        {
            if (K % i == 0)
            {
                flag = true;
                d1 = i;
                d2 = K / i;
                break;
            }
        }

        // If array can be generated
        if (flag)
        {

            // Print d1 and d2 alternatively
            for(let i = 0; i < N; i++)
            {
                if (i % 2 == 1)
                {
                    document.write(d2 + " ");
                }
                else
                {
                    document.write(d1 + " ");
                }
            }
        }

        else
        {

            // No such array can be generated
            document.write(-1);
        }
    }

    // Given N and K
    let N = 5, K = 21;

    // Function Call
    array_divisbleby_k(N, K);

// This code is contributed by suresh07.
</script>
```

**输出:**

```
3 7 3 7 3
```

***时间复杂度:**O(N+√K)*
T5**辅助空间:** O(1)