# 以 K 为模得出 R 的自然数(最多 N 个)之和

> 原文:[https://www . geesforgeks . org/sum-自然数-up-n-what-with-k-yield-r/](https://www.geeksforgeeks.org/sum-natural-numbers-up-to-n-whose-modulo-with-k-yield-r/)

给定三个整数 **N** 、 **K** 和 **R** 。任务是计算从 **1** 到 **N** 的所有数字的和，通过 **K** 的除法得到余数 **R** 。
**举例:**

> **输入:** N = 20，K = 4，R = 3
> **输出:** 55
> 3、7、11、15 和 19 是唯一给出 3 作为 4 除余数的数字。
> 3 + 7 + 11 + 15 + 19 = 55
> **输入:** N = 15，K = 13，R = 2
> **输出:** 17

**进场:**

*   初始化**和= 0** 并用 **K** 取每个元素从 **1** 到 **N** 的模。
*   如果余数等于 **R** ，那么更新 **sum = sum + i** ，其中 **i** 是当前给出 **R** 除以 **K** 的余数。
*   最后打印**和**的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum
long long int count(int N, int K, int R)
{
    long long int sum = 0;
    for (int i = 1; i <= N; i++) {

        // If current number gives R as the
        // remainder on dividing by K
        if (i % K == R)

            // Update the sum
            sum += i;
    }

    // Return the sum
    return sum;
}

// Driver code
int main()
{
    int N = 20, K = 4, R = 3;
    cout << count(N, K, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to return the sum
static long count(int N, int K, int R)
{
    long sum = 0;
    for (int i = 1; i <= N; i++)
    {

        // If current number gives R as the
        // remainder on dividing by K
        if (i % K == R)

            // Update the sum
            sum += i;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int N = 20, K = 4, R = 3;
    System.out.println(count(N, K, R));
}
}

// This code is contributed by
// prerna saini.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the sum
def count(N, K, R):
    sum = 0
    for i in range(1, N + 1):

        # If current number gives R as the
        # remainder on dividing by K
        if (i % K == R):

            # Update the sum
            sum += i

    # Return the sum
    return sum

# Driver code
if __name__ == '__main__':
    N = 20
    K = 4
    R = 3
    print(count(N, K, R))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the sum
static long count(int N, int K, int R)
{
    long sum = 0;
    for (int i = 1; i <= N; i++)
    {

        // If current number gives R as the
        // remainder on dividing by K
        if (i % K == R)

            // Update the sum
            sum += i;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void Main()
{
    int N = 20, K = 4, R = 3;
    Console.Write(count(N, K, R));
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum
function count1($N, $K, $R)
{
    $sum = 0;
    for ($i = 1; $i <= $N; $i++)
    {

        // If current number gives R as the
        // remainder on dividing by K
        if ($i % $K == $R)

            // Update the sum
            $sum += $i;
    }

    // Return the sum
    return $sum;
}

// Driver code
$N = 20; $K = 4; $R = 3;
echo count1($N, $K, $R);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the sum
    function count(N , K , R) {
        var sum = 0;
        for (i = 1; i <= N; i++) {

            // If current number gives R as the
            // remainder on dividing by K
            if (i % K == R)

                // Update the sum
                sum += i;
        }

        // Return the sum
        return sum;
    }

    // Driver code

        var N = 20, K = 4, R = 3;
        document.write(count(N, K, R));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
55
```