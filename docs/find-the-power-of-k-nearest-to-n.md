# 求最接近 N 的 K 的幂

> 原文:[https://www . geesforgeks . org/find-k 的幂最接近 n/](https://www.geeksforgeeks.org/find-the-power-of-k-nearest-to-n/)

给定两个整数 **N** & **K.** 任务是为整数 N 寻找 K 的最近幂，如果有两个最近的幂，考虑较大的一个。

**示例:**

> **输入:** N = 5，K = 3
> **输出:** 3
> **说明:**3 的幂是 3，9，27，。。。其中 3 是最接近 5 的，因为它有 2 的距离。
> 
> **输入:** N = 32，K = 7
> T3】输出:49
> T6】说明:7 的幂是 7，49，343，。。。在这些数字中，49 最接近 32。
> 
> **输入:** N = 6，K = 3
> **输出:** 9
> **说明:**3 和 9 都有距离= 3。但是 9 在 3 和 9 之间更大。

**方法:**按照以下步骤解决这个问题:

1.  对于 **N** 这个数，求 K 的最近的幂，大的小的。
2.  K 的较小幂将是**原木 <sub>K</sub> N** 的**地板值**(说 X)。所以数值会是**幂(K，X)** 。[P 的最低值=最接近 P 且≤ P 的整数]
3.  而 K 的更大幂将是**原木 <sub>K</sub> N** 的**上限值**(说 Y)。所以数值会是**幂(K，Y)** 。[P 的最大值=最接近 P 的整数≥ P]
4.  从 **N** 计算这两个值的差，并按照问题陈述中的规定打印最近的值。

下面是上述方法的实现。

## C++

```
// C++ program to
// implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find nearest power
int nearestPowerOfK(int N, int K)
{
    // Finding log of the element
    int lg = log(N) / log(K);

    // Calculating the two possible
    // nearest values
    int a = pow(K, lg);
    int b = pow(K, lg + 1);

    // Finding the closest one
    if ((N - a) < (b - N))
        return a;
    return b;
}

// Driver Code
int main()
{
    int N = 32, K = 7;
    cout << nearestPowerOfK(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;
public class GFG
{

// Function to find nearest power
static int nearestPowerOfK(int N, int K)
{
    // Finding log of the element
    int lg = (int)(Math.log(N) / Math.log(K));

    // Calculating the two possible
    // nearest values
    int a = (int)Math.pow(K, lg);
    int b = (int)Math.pow(K, lg + 1);

    // Finding the closest one
    if ((N - a) < (b - N))
        return a;
    return b;
}

// Driver Code
public static void main(String args[])
{
    int N = 32, K = 7;

    System.out.println(nearestPowerOfK(N, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program to implement the above approach
import math

# Function to find nearest power
def nearestPowerOfK(N, K):

    # Finding log of the element
    lg = math.log(N) // math.log(K)

    # Calculating the two possible
    # nearest values
    a = int(pow(K, lg))
    b = int(pow(K, lg + 1))

    # Finding the closest one
    if ((N - a) < (b - N)):
        return a

    return b

# Driver Code
if __name__ == "__main__":

    N = 32
    K = 7

    print(nearestPowerOfK(N, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

// Function to find nearest power
static int nearestPowerOfK(int N, int K)
{
    // Finding log of the element
    int lg = (int)(Math.Log(N) / Math.Log(K));

    // Calculating the two possible
    // nearest values
    int a = (int)Math.Pow(K, lg);
    int b = (int)Math.Pow(K, lg + 1);

    // Finding the closest one
    if ((N - a) < (b - N))
        return a;
    return b;
}

// Driver Code
public static void Main()
{
    int N = 32, K = 7;

    Console.Write(nearestPowerOfK(N, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find nearest power
function nearestPowerOfK(N, K)
{

    // Finding log of the element
    let lg = Math.floor(Math.log(N) /
                        Math.log(K));

    // Calculating the two possible
    // nearest values
    let a = Math.pow(K, lg);
    let b = Math.pow(K, lg + 1);

    // Finding the closest one
    if ((N - a) < (b - N))
        return a;

    return b;
}

// Driver Code
let N = 32, K = 7;

document.write(nearestPowerOfK(N, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
49
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)