# 生成一个最大元素最小化且数组元素之和可被 K 整除的 N 长度数组

> 原文:[https://www . geesforgeks . org/generate-an-n-length-array-having-max-element-minimum-and-sum-array-elements-除尽-k/](https://www.geeksforgeeks.org/generate-an-n-length-array-having-maximum-element-minimized-and-sum-of-array-elements-divisible-by-k/)

给定两个正整数 **N** 和 **K** ，任务是最小化数组的[最大元素，数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的和[为正，可被 **K** 整除。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** N = 4，K = 50
> **输出:** 13
> **解释**生成的数组为{12，13，12，13}。数组的和是 50，可以被 K (= 50)整除。数组中存在的最大元素是 13，这是可能的最小值。
> 
> **输入:** N = 3，K = 3
> T3】输出: 1

**方法:**给定的问题可以在以下观察的基础上解决:

*   为了最小化阵列的[最大元素，每对阵列元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的[绝对差必须最多为**1**，](https://www.geeksforgeeks.org/sum-absolute-differences-pairs-given-array/)[阵列元素](https://www.geeksforgeeks.org/python-program-to-find-sum-of-array/)之和必须为 **K** 。
*   因此，所有 **N** 元素的值必须至少等于 **(K/N)** 的[楼层值，以及剩余 **(K%N)** 元素乘以 **1** 得到数组元素](https://www.geeksforgeeks.org/floor-value-kth-root-of-a-number-using-recursive-binary-search/)[之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **K** 。

从上面的观察，构造的数组的最小最大值是 **(K/N)** 的[天花板值。](https://www.geeksforgeeks.org/multiple-of-x-closest-to-n/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the maximum
// element present in an N-length array
// having sum of elements divisible by K
int minimumValue(int N, int K)
{
    // Return the ceil value of (K / N)
    return ceil((double)K / (double)N);
}

// Driver Code
int main()
{
    int N = 4, K = 50;
    cout << minimumValue(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to minimize the maximum
// element present in an N-length array
// having sum of elements divisible by K
static int minimumValue(int N, int K)
{

    // Return the ceil value of (K / N)
    return(int)Math.ceil((double)K / (double)N);
}

// Driver code
public static void main(String[] args)
{
    int N = 4, K = 50;

    System.out.print(minimumValue(N, K));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to minimize the maximum
# element present in an N-length array
# having sum of elements divisible by K

def minimumValue(N, K):
    # Return the ceil value of (K / N)
    return math.ceil(K / N)

# Driver Code
N = 4
K = 50
print(minimumValue(N, K))

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to minimize the maximum
// element present in an N-length array
// having sum of elements divisible by K
static int minimumValue(int N, int K)
{

    // Return the ceil value of (K / N)
    return(int)Math.Ceiling((double)K / (double)N);
}

// Driver Code
public static void Main()
{
    int N = 4, K = 50;

    Console.WriteLine(minimumValue(N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to minimize the maximum
// element present in an N-length array
// having sum of elements divisible by K
function minimumValue(N, K)
{

    // Return the ceil value of (K / N)
    return Math.ceil(K / N);
}

// Driver Code

    let N = 4, K = 50;

    document.write(minimumValue(N, K));

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)