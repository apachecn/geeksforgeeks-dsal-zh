# 在对 D

执行给定操作后可到达的数组元素数量

> 原文:[https://www . geeksforgeeks . org/执行 d 上给定操作后可到达的数组元素数量/](https://www.geeksforgeeks.org/number-of-elements-from-the-array-which-are-reachable-after-performing-given-operations-on-d/)

给定一个数组 **arr[]** 和三个整数 **D** 、 **A** 和 **B** 。你可以从数字 **D** 开始，任何时候你都可以在当前数字上加或减 A 或 B。这意味着您可以任意多次执行以下四个操作:

1.  将 **A** 加到当前号码上。
2.  从当前数字中减去 **A** 。
3.  将 **B** 加到当前号码上。
4.  从当前数字中减去 **B** 。

任务是从给定的数组中找到整数的计数，在执行上述操作后可以达到该计数。
**例:**

> **输入:** arr[] = {4，5，6，7，8，9}，D = 4，A = 4，B = 6
> **输出:** 3
> 可达数为:
> 4 = 4
> 6 = 4+6–4
> 8 = 4+4
> **输入:** arr[] = {24，53，126，547，48，97}，D = 2，A = 5

**方法:**这个问题可以用[丢番图方程](https://www.geeksforgeeks.org/linear-diophantine-equations/)
的一个性质来解决，让我们想从数组中得到的整数为 **x** 。如果我们从 **D** 开始，可以对其进行任意次数的加减 **A** 或 **B** ，那就意味着我们需要找出下面的方程是否有整数解。

> D + p * A + q * B = x

如果它在 **p** 和 **q** 中有整数解，那么意味着我们可以从 **D** 到达整数 **x** ，否则不行。
将该等式重新排列为

> p * A+q * B = x–D

这个方程有一个整数解当且仅当**(x–D)% GCD(A，B) = 0** 。
现在迭代数组中的整数，检查这个方程对于当前的 **x** 是否有解。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the GCD
// of a and b
int GCD(int a, int b)
{
    if (b == 0)
        return a;
    return GCD(b, a % b);
}

// Function to return the count of reachable
// integers from the given array
int findReachable(int arr[], int D, int A,
                  int B, int n)
{

    // GCD of A and B
    int gcd_AB = GCD(A, B);

    // To store the count of reachable integers
    int count = 0;
    for (int i = 0; i < n; i++) {

        // If current element can be reached
        if ((arr[i] - D) % gcd_AB == 0)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(int);
    int D = 4, A = 4, B = 6;

    cout << findReachable(arr, D, A, B, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the GCD
    // of a and b
    static int GCD(int a, int b)
    {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    // Function to return the count of reachable
    // integers from the given array
    static int findReachable(int[] arr, int D, int A,
                    int B, int n)
    {

        // GCD of A and B
        int gcd_AB = GCD(A, B);

        // To store the count of reachable integers
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // If current element can be reached
            if ((arr[i] - D) % gcd_AB == 0)
                count++;
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 4, 5, 6, 7, 8, 9 };
        int n = arr.length;
        int D = 4, A = 4, B = 6;

        System.out.println(findReachable(arr, D, A, B, n));

    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the GCD
# of a and b
def GCD(a, b):
    if (b == 0):
        return a;
    return GCD(b, a % b);

# Function to return the count of reachable
# integers from the given array
def findReachable(arr, D, A, B, n):

    # GCD of A and B
    gcd_AB = GCD(A, B);

    # To store the count of reachable integers
    count = 0;
    for i in range(n):

        # If current element can be reached
        if ((arr[i] - D) % gcd_AB == 0):
            count+=1;

    # Return the count
    return count;

# Driver code
arr = [ 4, 5, 6, 7, 8, 9 ];
n = len(arr);
D = 4; A = 4; B = 6;

print(findReachable(arr, D, A, B, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the GCD
    // of a and b
    static int GCD(int a, int b)
    {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    // Function to return the count of reachable
    // integers from the given array
    static int findReachable(int[] arr, int D, int A,
                    int B, int n)
    {

        // GCD of A and B
        int gcd_AB = GCD(A, B);

        // To store the count of reachable integers
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // If current element can be reached
            if ((arr[i] - D) % gcd_AB == 0)
                count++;
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void Main()
    {

        int []arr = { 4, 5, 6, 7, 8, 9 };
        int n = arr.Length;
        int D = 4, A = 4, B = 6;

        Console.WriteLine(findReachable(arr, D, A, B, n));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the GCD
    // of a and b
    function GCD(a , b) {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    // Function to return the count of reachable
    // integers from the given array
    function findReachable(arr, D, A, B, n)
    {

        // GCD of A and B
        var gcd_AB = GCD(A, B);

        // To store the count of reachable integers
        var count = 0;
        for (i = 0; i < n; i++)
        {

            // If current element can be reached
            if ((arr[i] - D) % gcd_AB == 0)
                count++;
        }

        // Return the count
        return count;
    }

    // Driver code
        var arr = [ 4, 5, 6, 7, 8, 9 ];
        var n = arr.length;
        var D = 4, A = 4, B = 6;

        document.write(findReachable(arr, D, A, B, n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```