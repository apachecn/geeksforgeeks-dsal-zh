# 一个序列的第 n 个项，由当前项与其最大和最小数字的乘积

相加而成

> 原文:[https://www . geeksforgeeks . org/第 n 个序列术语由当前术语与其最大和最小数字乘积之和构成/](https://www.geeksforgeeks.org/nth-term-of-a-sequence-formed-by-sum-of-current-term-with-product-of-its-largest-and-smallest-digit/)

给定两个数字 **N** 和 **K** ，其中 K 代表序列的起始项。任务是找到由当前项和当前项的最大和最小位数的乘积形成的序列的**第 n 项**，即

> A <sub>N+1</sub> = A <sub>N</sub> +最大值(A <sub>N</sub> 的位数)*最小值(A <sub>N</sub> 的位数)

**例:**

> **输入:** K = 1， N = 5
> **输出:** 50
> **说明:**T8】A<sub>1</sub>= 1
> A<sub>2</sub>= A<sub>1</sub>+minDigit(A<sub>1</sub>)* maxDigit(A<sub>1</sub>)= 1+min(1)* max(1)= 1+1 * 1 = 2
> A<sub>3 = 2+min(2)* max(2)= 2+2 * 2 = 6
> A<sub>4</sub>= A<sub>3</sub>+minDigit(A<sub>3</sub>)* maxDigit(A<sub>3</sub>)= 6+min(6)* max(6)= 6+6 * 6 = 42
> A<sub>5</sub>= A<sub>4</sub>+minDigit( 2) = 42 + 2*4 = 50
> **输入:** K = 487，N = 2
> **输出:** 519
> **解释:**T56】A<sub>1</sub>= 487
> A<sub>2</sub>= A<sub>1</sub>+minDigit(A<sub>1</sub></sub>

**进场:**
让我们试着看一些观察，

> 当 K = 1 时，序列变成:1、2、6、42、50、50、50、…
> 当 K = 2 时，序列变成:2、6、42、50、50、50、…
> 。
> 。
> 当 K = 5 时，序列变成:5，30，30，30，30，30，30，…
> 。
> 。
> 同样，当 K = 10 时，序列变成:10，10，10，10，10，10，…

从上面的例子可以观察到，在一个整数至少有一个数字变成 0 之后，序列最终停止增加。如果任何一个数字变成 0，那么最小的数字总是 0，之后，序列中的所有整数保持不变。
所以方法是找到序列的项，直到在当前项的数字中遇到任意 0，
下面是上述方法的实现。

## C++

```
// C++ program for the above approach.

#include <bits/stdc++.h>
using namespace std;

// Function to find integer
int find(int K, int N)
{

    // because 1st integer is K itself
    N--;

    while (N--) {
        int curr_term = K;

        // Initialize min_d and max_d
        int min_d = 9;
        int max_d = 0;

        while (curr_term > 0) {
            int r = curr_term % 10;

            // updating min_d and max_d
            min_d = min(min_d, r);
            max_d = max(max_d, r);

            curr_term = curr_term / 10;
        }

        // break if min digit is 0
        if (min_d == 0) {
            break;
        }

        K = K + min_d * max_d;
    }

    return K;
}

// Driver code
int main()
{
    int K = 487;
    int N = 2;

    cout << find(K, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach.
import java.util.*;

class GFG{

// Function to find integer
static int find(int K, int N)
{

    // Because 1st integer is K itself
    N--;

    while (N-- != 0)
    {
        int curr_term = K;

        // Initialize min_d and max_d
        int min_d = 9;
        int max_d = 0;

        while (curr_term > 0)
        {
            int r = curr_term % 10;

            // Updating min_d and max_d
            min_d = Math.min(min_d, r);
            max_d = Math.max(max_d, r);

            curr_term = curr_term / 10;
        }

        // Break if min digit is 0
        if (min_d == 0)
        {
            break;
        }
        K = K + min_d * max_d;
    }
    return K;
}

// Driver code
public static void main(String[] args)
{
    int K = 487;
    int N = 2;

    System.out.print(find(K, N) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach.

# Function to find integer
def find(K, N):

    # Because 1st integer is K itself
    N = N - 1

    for i in range(0, N):
        curr_term = K

        # Initialize min_d and max_d
        min_d = 9
        max_d = 0

        while curr_term > 0:
            r = int(curr_term % 10)

            # Updating min_d and max_d
            min_d = min(min_d, r)
            max_d = max(max_d, r)

            curr_term = int(curr_term / 10)

        # Break if min digit is 0
        if min_d == 0:
           break

        K = K + min_d * max_d
        return K

# Driver code
K = 487
N = 2

print(find(K, N))

# This code is contributed by ishayadav181
```

## C#

```
// C# program for the above approach.
using System;

class GFG{

// Function to find integer
static int find(int K, int N)
{

    // Because 1st integer is K itself
    N--;

    while (N-- != 0)
    {
        int curr_term = K;

        // Initialize min_d and max_d
        int min_d = 9;
        int max_d = 0;

        while (curr_term > 0)
        {
            int r = curr_term % 10;

            // Updating min_d and max_d
            min_d = Math.Min(min_d, r);
            max_d = Math.Max(max_d, r);

            curr_term = (int)(curr_term / 10);
        }

        // Break if min digit is 0
        if (min_d == 0)
        {
            break;
        }

        K = K + min_d * max_d;
    }
    return K;
}

// Driver code
public static void Main()
{
    int K = 487;
    int N = 2;

    Console.Write(find(K, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach.

// Function to find integer
function find(K, N)
{

    // because 1st integer is K itself
    N--;

    while (N--) {
        let curr_term = K;

        // Initialize min_d and max_d
        let min_d = 9;
        let max_d = 0;

        while (curr_term > 0) {
            let r = curr_term % 10;

            // updating min_d and max_d
            min_d = Math.min(min_d, r);
            max_d = Math.max(max_d, r);

            curr_term = Math.floor(curr_term / 10);
        }

        // break if min digit is 0
        if (min_d == 0) {
            break;
        }

        K = K + min_d * max_d;
    }

    return K;
}

// Driver code

    let K = 487;
    let N = 2;

    document.write(find(K, N) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
519
```

***时间复杂度:** O(N)*

***辅助空间:**O(1)*T4】