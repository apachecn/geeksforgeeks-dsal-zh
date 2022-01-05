# 求配对数(a，b)，使得 a % b = K

> 原文:[https://www . geeksforgeeks . org/find-配对数-a-b-so-a-b-k/](https://www.geeksforgeeks.org/find-the-number-of-pairs-a-b-such-that-a-b-k/)

给定两个整数 **N** 和 **K** ，其中 **N，K > 0** ，任务是找出总对数 **(a，b)** ，其中 **1 ≤ a，b ≤ N** ，使得 **a % b = K** 。
**示例:**

> **输入:** N = 4，K = 2
> **输出:** 2
> 只有有效的对是(2，3)和(2，4)。
> **输入:** N = 11，K = 5
> **输出:** 7

**简单方法:**运行从 **1** 到 **n** 的两个循环，并计算所有对 **(i，j)** ，其中 **i % j = K** 。该方法的时间复杂度为 **O(n <sup>2</sup> )** 。
**有效方法:**最初总计**计数= N–K**，因为范围内的所有数字都是 **> K** 除以后会给出 **K** 作为余数。之后，对于所有的 **i > K** 都有精确的**(N–K)/I**数，这些数在除以 **i** 后会给出余数作为 **K** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required pairs
int CountAllPairs(int N, int K)
{

    int count = 0;

    if (N > K) {

        // Initial count
        count = N - K;
        for (int i = K + 1; i <= N; i++)
            count = count + ((N - K) / i);
    }

    return count;
}

// Driver code
int main()
{
    int N = 11, K = 5;

    cout << CountAllPairs(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
class GFG {

    // Function to return the count
    // of required pairs
    static int CountAllPairs(int N, int K)
    {

        int count = 0;

        if (N > K) {

            // Initial count
            count = N - K;
            for (int i = K + 1; i <= N; i++)
                count = count + ((N - K) / i);
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 11, K = 5;
        System.out.println(CountAllPairs(N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the count
# of required pairs
def CountAllPairs(N, K):
    count = 0
    if( N > K):

        # Initial count
        count = N - K
        for i in range(K + 1, N + 1):
            count = count + ((N - K) // i)

    return count

# Driver code
N = 11
K = 5
print(CountAllPairs(N, K))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the count
    // of required pairs
    static int CountAllPairs(int N, int K)
    {

        int count = 0;

        if (N > K) {

            // Initial count
            count = N - K;
            for (int i = K + 1; i <= N; i++)
                count = count + ((N - K) / i);
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int N = 11, K = 5;
        Console.WriteLine(CountAllPairs(N, K));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of required pairs
function CountAllPairs($N, $K)
{
    $count = 0;

    if( $N > $K){

        // Initial count
        $count = $N - $K;
        for($i = $K+1; $i <= $N ; $i++)
        {
                $x = ((($N - $K) / $i));
                $count = $count + (int)($x);
        }
    }

    return $count;
}

    // Driver code
    $N = 11;
    $K = 5;
    echo(CountAllPairs($N, $K));

?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the count
    // of required pairs
    function CountAllPairs( N,  K)
    {

        let count = 0;

        if (N > K) {

            // Initial count
            count = N - K;
            for (let i = K + 1; i <= N; i++)
                count = count + parseInt((N - K) / i);
        }

        return count;
    }

    // Driver code
        let N = 11, K = 5;
        document.write(CountAllPairs(N, K));

//contributed by sravan (171fa07058)

</script>
```

**Output:** 

```
7
```