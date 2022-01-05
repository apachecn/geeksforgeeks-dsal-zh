# 取消设置给定数字的最低有效 K 位

> 原文:[https://www . geesforgeks . org/unset-最低有效 k 位给定数字/](https://www.geeksforgeeks.org/unset-least-significant-k-bits-of-a-given-number/)

给定一个整数 **N** ，任务是打印通过从 **N** 中取消设置最低有效 **K** 位获得的数字。

**示例:**

> **输入:** N = 200，K=5
> **输出:** 192
> **解释:**
> (200)<sub>10</sub>=(11001000)<sub>2</sub>T13】从上述二进制表示中取消设置最低有效 K(= 5)位，得到的新数为(11000000) <sub>2</sub> = (192)
> 
> **输入:** N = 730，K = 3
> T3】输出: 720

**方法:**按照以下步骤解决问题:

*   想法是创建一个表单的掩码 **111111100000…** 。
*   要创建遮罩，从所有遮罩开始，如 **1111111111…** 。
*   生成全 1 有两种可能的选择。或者通过用 **1** 翻转所有 **0** s，或者通过使用 [2s 补码](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)并将其左移 **K** 位来生成。

> 面具=(~ 0)<面具=(-1)<k+1)

*   最后，打印 **K + 1** 的值，因为它是从右到左从零开始的索引。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value
// after unsetting K LSBs
int clearLastBit(int N, int K)
{
    // Create a mask
    int mask = (-1 << K + 1);

    // Bitwise AND operation with
    // the number and the mask
    return N = N & mask;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 730, K = 3;

    // Function Call
    cout << clearLastBit(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to return the value
// after unsetting K LSBs
static int clearLastBit(int N, int K)
{
    // Create a mask
    int mask = (-1 << K + 1);

    // Bitwise AND operation with
    // the number and the mask
    return N = N & mask;
}

// Driver Code
public static void main(String[] args)
{
    // Given N and K
    int N = 730, K = 3;

    // Function Call
    System.out.print(clearLastBit(N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the value
# after unsetting K LSBs
def clearLastBit(N, K):

    # Create a mask
    mask = (-1 << K + 1)

    # Bitwise AND operation with
    # the number and the mask
    N = N & mask

    return N

# Driver Code

# Given N and K
N = 730
K = 3

# Function call
print(clearLastBit(N, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to return the value
// after unsetting K LSBs
static int clearLastBit(int N,
                        int K)
{
  // Create a mask
  int mask = (-1 << K + 1);

  // Bitwise AND operation with
  // the number and the mask
  return N = N & mask;
}

// Driver Code
public static void Main(String[] args)
{
  // Given N and K
  int N = 730, K = 3;

  // Function Call
  Console.Write(clearLastBit(N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to return the value
// after unsetting K LSBs
function clearLastBit(N , K)
{
    // Create a mask
    var mask = (-1 << K + 1);

    // Bitwise AND operation with
    // the number and the mask
    return N = N & mask;
}

// Driver Code
//Given N and K
var N = 730, K = 3;

// Function Call
document.write(clearLastBit(N, K));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
720
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)