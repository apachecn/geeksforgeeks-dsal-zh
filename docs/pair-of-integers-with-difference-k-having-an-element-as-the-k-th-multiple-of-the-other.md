# 差为 K 的整数对，其中一个元素是另一个的 K 倍

> 原文:[https://www . geeksforgeeks . org/一对有差的整数 k 有一个元素作为另一个的第 k 倍/](https://www.geeksforgeeks.org/pair-of-integers-with-difference-k-having-an-element-as-the-k-th-multiple-of-the-other/)

给定一个整数 **K** ，任务是找到一对数字 **(A，B)** 使得**A–B = K**和**A/B = K**如果不能生成这样的对，则打印**“否”**。

**示例:**

> **输入:** K = 6
> **输出:** 7.2 1.2
> **说明:**
> 由于 7.2–1.2 = 6 和 7.2 / 1.2 = 6，所以对{7.2，1.2}满足必要条件。
> 
> **输入:**K = 1
> T3】输出:否

**方法:**
需要进行以下观察来解决问题:

*   给定的条件可以用方程的形式写成:
    1.  等式(1):**A–B = K =>A–B–K = 0**
    2.  等式(2):**A/B = K =>A –( K * B)= 0**
*   求解这两个方程，我们得到:

> (K *等式(1))–等式(2)= 0
> =>K * A–K * B–K<sup>2</sup>–(A–K * B)= 0
> =>K * A–K<sup>2</sup>–A–K * b+ K * B = 0
> =>A *(K-1)–K<sup>2</sup>= 0
> =>A *(K-1)= K【T10

*   替换等式(1)中的 A 值，可以得到 B 值为**K/(K–1)**
*   可以观察到，如果 **K** 的值是 **1** ，那么就找不到这样的对，因为 **A** 和 **B** 的*分母 T7】都变成了 0。*

按照以下步骤解决问题:

*   如果 **K** 等于 **1** ，则打印**“否”**。
*   否则，如果 **K** 等于除 **0** 以外的任何值，则计算值 **(K*K) / (K -1)** 和**K/(K–1)**并打印。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// required pair
void computePair(double K)
{
    // No pair possible
    if (K == 1) {
        cout << "No";
        return;
    }
    else {

        cout << K * K / (K - 1) << " ";
        cout << K / (K - 1) << endl;
    }
}

// Driver Code
int main()
{
    double K = 6;
    computePair(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above problem
class GFG{

// Function to find the
// required pair
static void computePair(double K)
{

    // No pair possible
    if (K == 1)
    {
        System.out.print("No");
        return;
    }
    else
    {
        System.out.print(K * K / (K - 1) + " ");
        System.out.print(K / (K - 1) + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    double K = 6;

    computePair(K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above problem

# Function to find the
# required pair
def computePair(K):

    # No pair possible
    if (K == 1):
        print("No")
        return

    else:
        print(K * K / (K - 1), end = " ")
        print(K / (K - 1))

# Driver Code
if __name__ == "__main__":

    K = 6

    computePair(K)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above problem
using System;

class GFG{

// Function to find the
// required pair
static void computePair(double K)
{

    // No pair possible
    if (K == 1)
    {
        Console.Write("No");
        return;
    }
    else
    {
        Console.Write(K * K / (K - 1) + " ");
        Console.Write(K / (K - 1) + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    double K = 6;

    computePair(K);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above problem

// Function to find the
// required pair
function computePair(K)
{
    // No pair possible
    if (K == 1) {
        document.write( "No");
        return;
    }
    else {

        document.write( K * K / (K - 1) + " ");
        document.write( K / (K - 1) );
    }
}

// Driver Code
var K = 6;
computePair(K);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
7.2 1.2
```

***时间复杂度:** O(1)*
***辅助空间；** O(1)*