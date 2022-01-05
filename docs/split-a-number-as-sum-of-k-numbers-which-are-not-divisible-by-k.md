# 将一个数拆分为 K 个不能被 K 整除的数的和

> 原文:[https://www . geeksforgeeks . org/split-a-number-as-sum-k-numbers-哪些不能被 k 整除/](https://www.geeksforgeeks.org/split-a-number-as-sum-of-k-numbers-which-are-not-divisible-by-k/)

给定两个数字 **N** 和 **K** ，任务是将这个数字拆分为 **K** 个正整数，使得它们的和等于 **N** ，并且这些 **K** 个整数都不是 K 的倍数。
**注:***N>= 2*
**示例:**

> **输入:** N = 10，K = 3
> **输出:** 1，1，8
> **输入:** N = 18，K = 3
> **输出:** 1，1，16

**方法:**
要将 **N** 拆分为 **K** 个数字，我们需要通过以下步骤来处理问题:

*   检查 **N** 是否能被 **K** 整除。
*   如果 **N** 被 **K** 整除，那么**N–K+1**就不能被 **K** 整除。因此，我们可以将 N 拆分为**N–K+1**作为一部分，其余所有**K–1**部分作为 **1** 。
*   如果 **N** 不能被 **K** 整除:
    *   如果 **K** 为 2，则不能拆分。
    *   否则，将 **N** 分割成 **K-2** 零件作为全部 **1** 和 **2** 和**N–K**作为剩余的两个零件。

下面的代码是上述方法的实现:

## C++

```
// C++ program to split a number
// as sum of K numbers which are
// not divisible by K

#include <iostream>
using namespace std;

// Function to split into K parts
// and print them
void printKParts(int N, int K)
{
    if (N % K == 0) {

        // Print 1 K - 1 times
        for (int i = 1; i < K; i++)
            cout << "1, ";

        // Print N - K + 1
        cout << N - (K - 1) << endl;
    }
    else {
        if (K == 2) {
            cout << "Not Possible" << endl;
            return;
        }

        // Print 1 K-2 times
        for (int i = 1; i < K - 1; i++)
            cout << 1 << ", ";

        // Print 2 and N - K
        cout << 2 << ", "
             << N - K << endl;
    }
}

// Driver code
int main()
{
    int N = 18, K = 5;
    printKParts(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split a number
// as sum of K numbers which are
// not divisible by K
class GFG{

// Function to split into K parts
// and print them
static void printKParts(int N, int K)
{
    if (N % K == 0)
    {

        // Print 1 K - 1 times
        for(int i = 1; i < K; i++)
           System.out.print("1, ");

        // Print N - K + 1
        System.out.print(N - (K - 1) + "\n");
    }
    else
    {
        if (K == 2)
        {
            System.out.print("Not Possible" + "\n");
            return;
        }

        // Print 1 K-2 times
        for(int i = 1; i < K - 1; i++)
           System.out.print(1 + ", ");

        // Print 2 and N - K
        System.out.print(2 + ", " + (N - K) + "\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 18, K = 5;

    printKParts(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to split a number
# as sum of K numbers which are
# not divisible by K

# Function to split into K parts
# and print them
def printKParts(N, K):

    if (N % K == 0):

        # Print 1 K - 1 times
        for i in range(1, K):
            print("1, ");

        # Print N - K + 1
        print(N - (K - 1), end = "");
    else:
        if (K == 2):
            print("Not Possible", end = "");
            return;

    # Print 1 K-2 times
    for i in range(1, K - 1):
        print(1, end = ", ");

    # Print 2 and N - K
    print(2, ", ", (N - K), end = "");

# Driver code
if __name__ == '__main__':

    N = 18;
    K = 5;

    printKParts(N, K);

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program to split a number
// as sum of K numbers which are
// not divisible by K
using System;

class GFG{

// Function to split into K parts
// and print them
static void printKParts(int N, int K)
{
    if (N % K == 0)
    {

        // Print 1 K - 1 times
        for(int i = 1; i < K; i++)
           Console.Write("1, ");

        // Print N - K + 1
        Console.Write(N - (K - 1) + "\n");
    }
    else
    {
        if (K == 2)
        {
            Console.Write("Not Possible" + "\n");
            return;
        }

        // Print 1 K-2 times
        for(int i = 1; i < K - 1; i++)
           Console.Write(1 + ", ");

        // Print 2 and N - K
        Console.Write(2 + ", " + (N - K) + "\n");
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 18, K = 5;

    printKParts(N, K);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to split a number
// as sum of K numbers which are
// not divisible by K

// Function to split into K parts
// and print them
function printKParts(N, K)
{
    if (N % K == 0) {

        // Print 1 K - 1 times
        for (var i = 1; i < K; i++)
            document.write( "1, ");

        // Print N - K + 1
        document.write( (N - (K - 1)) + "<br>");
    }
    else {
        if (K == 2) {
            document.write( "Not Possible" + "<br>");
            return;
        }

        // Print 1 K-2 times
        for (var i = 1; i < K - 1; i++)
            document.write( 1 + ", ");

        // Print 2 and N - K
        document.write( 2 + ", "
             + (N - K) + "<br>");
    }
}

// Driver code
var N = 18, K = 5;
printKParts(N, K);

</script>
```

**Output:** 

```
1, 1, 1, 2, 13
```

**时间复杂度:** *O(K)*