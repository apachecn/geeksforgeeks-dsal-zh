# 生成所有 K 尺寸子阵列的和除以 N 后剩下余数 X 的阵列

> 原文:[https://www . geesforgeks . org/generate-array-what-sum-of-all-k-size-subarray-除以 n-leaks-余数-x/](https://www.geeksforgeeks.org/generate-array-whose-sum-of-all-k-size-subarrays-divided-by-n-leaves-remainder-x/)

给定三个整数 **N** 、 **K** 和 **X** ，任务是创建一个长度为 **N** 的数组，其所有 K 长度子数组的和以 **N** 为模为 **X** 。
**示例:**

> **输入:** N = 6，K = 3，X = 3
> **输出:** 9 6 6 9 6 6
> **解释:**
> 长度为 3 的所有子阵列及其各自的和%N 值如下:
> 【9，6，6】和= 21% 6 = 3
> 【6，6，9】和= 21% 6 = 3
> 【6，9，6】和= 21 % 6 = 3
> 6] sum = 21 % 6 = 3
> 由于它的所有子阵都有 sum % N = X (=3)，所以生成的数组是有效的。
> **输入:** N = 4，K = 2，X = 2
> **输出:** 6 4 6 4

**方法:**
我们可以观察到，为了使任何大小的子阵列的和 **K** 模 **N** 等于 **X** ，子阵列需要有一个等于 **N** 的**K–1**元素和一个等于 **N + X** 的元素。
**插图:**

> 如果 N = 6，K = 3，X = 3
> 这里，K 长度子阵列需要是{9，6，6}的置换，其中 2(K–1)个元素可被 6 整除，1 个元素的模 N 等于 X( 9%6 = 3)
> 子阵列的和% N = (21 % 6) = 3(与 X 相同)
> 因此，每个 K 长度

因此，请按照以下步骤解决问题:

*   迭代 **i** 从 **0** 到**N–1**，打印所需子阵列的 **i <sup>th</sup>** 元素。

*   如果 **i % K** 等于 **0** ，打印 **N + X** 。否则，对于 **i 的所有其他值，**打印 **N** 。

*   这确保了每个可能的 K 长度子阵列都有一个和 **K*N + X** 。因此，所有这些子阵列的和模 **N** 为 **X** 。

下面是上述方法的实现。

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function prints the required array
void createArray(int n, int k, int x)
{
    for (int i = 0; i < n; i++) {
        // First element of each K
        // length subarrays
        if (i % k == 0) {
            cout << x + n << " ";
        }
        else {
            cout << n << " ";
        }
    }
}

// Driver Program
int main()
{

    int N = 6, K = 3, X = 3;
    createArray(N, K, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG{

// Function prints the required array
static void createArray(int n, int k, int x)
{
    for(int i = 0; i < n; i++)
    {

       // First element of each K
       // length subarrays
       if (i % k == 0)
       {
           System.out.print((x + n) + " ");
       }
       else
       {
           System.out.print(n + " ");
       }
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 6, K = 3, X = 3;

    createArray(N, K, X);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function prints the required array
def createArray(n, k, x):

    for i in range(n):

        # First element of each K
        # length subarrays
        if (i % k == 0):
            print(x + n, end = " ")
        else :
            print(n, end = " ")

# Driver code
N = 6
K = 3
X = 3

createArray(N, K, X)

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function prints the required array
static void createArray(int n, int k, int x)
{
    for(int i = 0; i < n; i++)
    {

       // First element of each K
       // length subarrays
       if (i % k == 0)
       {
           Console.Write((x + n) + " ");
       }
       else
       {
           Console.Write(n + " ");
       }
    }
}

// Driver Code
public static void Main()
{
    int N = 6, K = 3, X = 3;

    createArray(N, K, X);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function prints the required array
function createArray(n, k, x)
{
    for (var i = 0; i < n; i++) {
        // First element of each K
        // length subarrays
        if (i % k == 0) {
            document.write( x + n + " ");
        }
        else {
            document.write( n + " ");
        }
    }
}

// Driver Program
var N = 6, K = 3, X = 3;
createArray(N, K, X);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
9 6 6 9 6 6
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*