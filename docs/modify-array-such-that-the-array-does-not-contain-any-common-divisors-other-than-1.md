# 修改数组，使数组不包含除 1 以外的任何公约数

> 原文:[https://www . geesforgeks . org/modify-array-so-array-不包含除-1 以外的任何公约数/](https://www.geeksforgeeks.org/modify-array-such-that-the-array-does-not-contain-any-common-divisors-other-than-1/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是通过将数组的任何数组元素重复除以其任何除数 **d** (d ≤ **X** )来检查是否有可能修改该数组，使得该数组不包含除 **1** 以外的任何公约数。如果可以修改数组使其满足给定条件，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {6，15，6}，X = 6
> **输出:**
> 是
> 2 5 2
> **解释:**
> 操作 1:将 arr[0]除以 3(因为 3 ≤ 6)将 arr[]修改为{ 2，15，6 }。
> 操作 2:将 arr[1]除以 5(因为 5 ≤ 6)将 arr[]修改为{ 2，3，6 }。
> 因此，数组的[GCD = GCD({ 2，3，6}) = 1，这意味着数组除了 1 之外没有公约数，这是必需的条件。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
> 
> **输入:** arr[] = {10，20，30}，X = 4
> T3】输出:否

**方法:**思路是利用[欧几里德的 GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 找到给定数组的 [GCD。这给出了数组元素的所有公共因子。除去所有这些因素，就没有共同的因素了。因此，可以生成这样的阵列。否则，不可能生成这样的数组。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

按照以下步骤解决问题:

1.  初始化一个变量，比如说 **G，**来存储给定数组的 [GCD。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**和[计算 GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 并将其存储在变量中，比如 **G** 。
3.  迭代范围**【2，X】**，检查 **G** 的除数是否大于 **X** 。
4.  如果发现为真，则打印**“否”**。否则，打印**“是”。**
5.  否则，通过将所有元素除以 **G** 修改数组后，[打印数组元素](https://practice.geeksforgeeks.org/problems/print-elements-of-array4910/1)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to modify the array such that
// there is no common factor between
// array elements except 1
void checkCommonDivisor(int arr[],
                        int N, int X)
{
    // Stores GCD of the array
    int G = 0;

    // Calculate GCD of the array
    for (int i = 0; i < N; i++) {
        G = __gcd(G, arr[i]);
    }

    int copy_G = G;

    for (int divisor = 2;
         divisor <= X; divisor++) {

        // If the current divisor
        // is smaller than X
        while (G % divisor == 0) {

            // Divide GCD by the
            // current divisor
            G = G / divisor;
        }
    }

    // If possible
    if (G <= X) {
        cout << "Yes\n";

        // Print the modified array
        for (int i = 0; i < N; i++)
            cout << arr[i] / copy_G << " ";
        cout << endl;
    }

    // Otherwise
    else
        cout << "No";
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 6, 15, 6 }, X = 6;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    checkCommonDivisor(arr, N, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if it is possible
// to modify the array such that
// there is no common factor between
// array elements except 1
static void checkCommonDivisor(int[] arr,
                               int N, int X)
{

    // Stores GCD of the array
    int G = 0;

    // Calculate GCD of the array
    for(int i = 0; i < N; i++)
    {
        G = gcd(G, arr[i]);
    }

    int copy_G = G;

    for(int divisor = 2;
            divisor <= X;
            divisor++)
    {

        // If the current divisor
        // is smaller than X
        while (G % divisor == 0)
        {

            // Divide GCD by the
            // current divisor
            G = G / divisor;
        }
    }

    // If possible
    if (G <= X)
    {
        System.out.println("Yes");

        // Print the modified array
        for(int i = 0; i < N; i++)
            System.out.print((arr[i] / copy_G) + " ");

        System.out.println();
    }

    // Otherwise
    else
        System.out.println("No");
}

// Calculating gcd
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 6, 15, 6 };
    int X = 6;

    // Size of the array
    int N = arr.length;

    checkCommonDivisor(arr, N, X);
}
}

// This code is contributed by user_qa7r
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if it is possible
# to modify the array such that
# there is no common factor between
# array elements except 1
def checkCommonDivisor(arr, N, X):

    # Stores GCD of the array
    G = 0

    # Calculate GCD of the array
    for i in range(N):
        G = math.gcd(G, arr[i])

    copy_G = G

    for divisor in range(2, X + 1):

        # If the current divisor
        # is smaller than X
        while (G % divisor == 0):

            # Divide GCD by the
            # current divisor
            G = G // divisor

    # If possible
    if (G <= X):
        print("Yes")

        # Print the modified array
        for i in range(N):
            print(arr[i] // copy_G, end = " ")

        print()

    # Otherwise
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [6, 15, 6]
    X = 6

    # Size of the array
    N = len(arr)
    checkCommonDivisor(arr, N, X)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int GCD(int a, int b)
{
    return b == 0 ? a : GCD(b, a % b);
}

// Function to check if it is possible
// to modify the array such that
// there is no common factor between
// array elements except 1
static void checkCommonDivisor(int []arr,
                               int N, int X)
{

    // Stores GCD of the array
    int G = 0;

    // Calculate GCD of the array
    for(int i = 0; i < N; i++)
    {
        G = GCD(G, arr[i]);
    }

    int copy_G = G;

    for(int divisor = 2;
            divisor <= X;
            divisor++)
    {

        // If the current divisor
        // is smaller than X
        while (G % divisor == 0)
        {

            // Divide GCD by the
            // current divisor
            G = G / divisor;
        }
    }

    // If possible
    if (G <= X)
    {
        Console.WriteLine("Yes");

        // Print the modified array
        for(int i = 0; i < N; i++)
            Console.Write(arr[i] / copy_G + " ");

        Console.Write("\n");
    }

    // Otherwise
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main()
{

    // Given array
    int []arr = { 6, 15, 6 };
    int X = 6;

    // Size of the array
    int N = arr.Length;

    checkCommonDivisor(arr, N, X);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to check if it is possible
    // to modify the array such that
    // there is no common factor between
    // array elements except 1
    function checkCommonDivisor(arr , N , X) {

        // Stores GCD of the array
        var G = 0;

        // Calculate GCD of the array
        for (i = 0; i < N; i++) {
            G = gcd(G, arr[i]);
        }

        var copy_G = G;

        for (divisor = 2; divisor <= X; divisor++) {

            // If the current divisor
            // is smaller than X
            while (G % divisor == 0) {

                // Divide GCD by the
                // current divisor
                G = G / divisor;
            }
        }

        // If possible
        if (G <= X) {
            document.write("Yes<br/>");

            // Print the modified array
            for (i = 0; i < N; i++)
                document.write((arr[i] / copy_G) + " ");

            document.write();
        }

        // Otherwise
        else
            document.write("No");
    }

    // Calculating gcd
    function gcd(a , b) {
        if (b == 0)
            return a;

        return gcd(b, a % b);
    }

    // Driver Code

        var arr = [ 6, 15, 6 ];
        var X = 6;

        // Size of the array
        var N = arr.length;

        checkCommonDivisor(arr, N, X);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Yes
2 5 2
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*