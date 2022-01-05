# 通过在任意步骤将其更改为 2*N 或 N/10 来将 N 更改为 1 的最少步骤

> 原文:[https://www . geesforgeks . org/通过在任意步骤将其更改为 2n 或 n-10 来更改 n-1 的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-to-change-n-to-1-by-changing-it-to-2n-or-n-10-at-any-step/)

给定一个整数 **N，**求将 **N** 变为 **1 的最小操作数。**如果不可能，打印 **-1。**一次操作定义为将 **N** 转换为数字 **2*N** 或将 **N** 转换为数字 **N/10(仅当 N 可被 10 整除)。**

**示例:**

> **输入:** N = 50
> **输出:** 3
> **说明:** N 可以通过如下三步转换为 1:
> ->首先将 N 乘以 2，将 N 从 50 变为 100 (2*N)
> - >然后，将 N 除以 10，将 N 从 100 变为 10 (N/10)
> - >然后，将 N 除以 10，再进行更改
> 
> **输入:** N = 120
> **输出:** -1
> **说明:【Geek 没有可能到达位置 1。**

**方法:N** 只有当 **N** 在每一步通过**将**乘以 **2** 或者**将**除以 **10** 才能被转换为 **1** 。如果 **N** 除了 **2** 和 **5** 之外还有一个质因数，那么按照这些步骤 **N** 不能简化为 **1** 。而且如果 **N** 的素分解中 **2s** 的个数大于 **5s** ，那么 **N** 就不能将其减少到 **1** 了，因为不可能中和掉所有的 **2s** 。相等数量的 **2s** 和 **5s** 可以通过将数量除以 **10** 来中和。多余的 **5s** 可以用多余的 **2s** 相乘再除以 **10** 来中和。按照以下步骤解决问题:

*   将变量**二进制**和**五进制**初始化为 **0** ，以计数 **N.** 的[素因子化](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)中的 **2** 和 **5** 的数量
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **N%2** 等于 **0** ，执行以下步骤:
    *   将数字 **N** 除以 **2。**
    *   将**二进制**的值增加 **1。**
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **N%5** 等于 **0** ，执行以下步骤:
    *   将数字 **N** 除以 **5。**
    *   将**五**的数值增加 **1。**
*   如果 **N** 等于 **1** ，**二的数量**小于等于**五的数量，**则打印**2 *五-二**作为答案。
*   否则，打印 **-1。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be changed
// to 1 or not.
void check(int N)
{
    int twos = 0, fives = 0;

    // Count the number of 2 in the prime
    // factorisation of N
    while (N % 2 == 0) {
        N /= 2;
        twos++;
    }

    // Count the number of 5 in the prime
    // factorisation of N
    while (N % 5 == 0) {
        N /= 5;
        fives++;
    }

    if (N == 1 && twos <= fives) {
        cout << 2 * fives - twos;
    }
    else {
        cout << -1;
    }
}

// Driver Code
int main()
{
    int N = 50;

    check(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if N can be changed
// to 1 or not.
static void check(int N)
{
    int twos = 0, fives = 0;

    // Count the number of 2 in the prime
    // factorisation of N
    while (N % 2 == 0)
    {
        N /= 2;
        twos++;
    }

    // Count the number of 5 in the prime
    // factorisation of N
    while (N % 5 == 0)
    {
        N /= 5;
        fives++;
    }

    if (N == 1 && twos <= fives)
    {
        System.out.println( 2 * fives - twos);
    }
    else
    {
        System.out.println(-1);
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 50;

    check(N);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if N can be changed
# to 1 or not.
def check(N):
    twos = 0
    fives = 0

    # Count the number of 2 in the prime
    # factorisation of N
    while (N % 2 == 0):
        N /= 2
        twos += 1

    # Count the number of 5 in the prime
    # factorisation of N
    while (N % 5 == 0):
        N /= 5
        fives += 1

    if (N == 1 and twos <= fives):
        print(2 * fives - twos)

    else:
        print(-1)

# Driver Code
if __name__ == '__main__':
    N = 50
    check(N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if N can be changed
// to 1 or not.
static void check(int N)
{
    int twos = 0, fives = 0;

    // Count the number of 2 in the prime
    // factorisation of N
    while (N % 2 == 0) {
        N /= 2;
        twos++;
    }

    // Count the number of 5 in the prime
    // factorisation of N
    while (N % 5 == 0) {
        N /= 5;
        fives++;
    }

    if (N == 1 && twos <= fives) {
        Console.Write( 2 * fives - twos);
    }
    else {
        Console.Write(-1);
    }
}

// Driver Code
public static void Main()
{
     int N = 50;

    check(N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if N can be changed
// to 1 or not.
function check(N)
{
    var twos = 0, fives = 0;

    // Count the number of 2 in the prime
    // factorisation of N
    while (N % 2 == 0)
    {
        N /= 2;
        twos++;
    }

    // Count the number of 5 in the prime
    // factorisation of N
    while (N % 5 == 0)
    {
        N /= 5;
        fives++;
    }

    if (N == 1 && twos <= fives)
    {
        document.write(2 * fives - twos);
    }
    else
    {
        document.write(-1);
    }
}

// Driver Code
var N = 50;
check(N);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
3
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*