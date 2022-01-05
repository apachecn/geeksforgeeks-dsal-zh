# 从 N 个自然数中计数 N 大小的非递减子阵列

> 原文:[https://www . geeksforgeeks . org/count-non-reduced-n-size-n-from-n-自然数子阵/](https://www.geeksforgeeks.org/count-non-decreasing-subarrays-of-size-n-from-n-natural-numbers/)

给定的是 **N** 个自然数，任务是找到大小为 N 的子阵列的计数，这些子阵列可以使用从 **1 到 N** 的元素形成，使得子阵列中的每个元素小于或等于其右边的元素(a[i] ≤ a[i+1])。
**例:**

> **输入:** N = 2
> **输出:** 3
> **解释:**
> 给定 N 个自然数的数组:{1，2}
> 可形成的必需子数组:【1，1】，【1，2】，【2，2】。
> **输入:** N = 3
> **输出:** 10
> **解释:**
> 给定 N 个自然数的数组:{1，2，3}
> 可以构成的必需子数组:【1，1，1】，【1，1，2】，【1，2，2】，【2，2，】,【1，1，3】，【1，3，3】，【3，3】

**进场:**

*   由于阵列的每个元素在 1 到 N 之间，并且子阵列可以具有非降序的重复元素，即**a[0]≤a[1]≤……。≤a[N–1]**。
*   从 n 个对象中选择替换 r 个对象的方式数量为![{{n+r-1}\choose{r}}  ](img/c128385a2f42bab53697485cfc3df2b7.png "Rendered by QuickLaTeX.com")(使用[结合重复](https://www.geeksforgeeks.org/combinations-with-repetitions/))。
*   这里 **r = N 和 n = N** 因为我们可以从 1 到 N 中进行选择，所以所有长度为 N 且元素从 1 到 N 的排序数组的计数将是![{{2*n-1}\choose{n}}  ](img/14205640f8ba7d2fa7609338a0e6eae5.png "Rendered by QuickLaTeX.com")。
*   现在可以借助[二项式系数](https://www.geeksforgeeks.org/binomial-coefficient-dp-9/)进一步展开。由此获得的系数将是所需的子阵列数。

以下是上述方法的实现:

## C++

```
// C++ program to count non decreasing subarrays
// of size N from N Natural numbers

#include <bits/stdc++.h>
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int C[k + 1];
    memset(C, 0, sizeof(C));

    // Since nC0 is 1
    C[0] = 1;

    for (int i = 1; i <= n; i++) {

        // Compute next row of pascal triangle using
        // the previous row
        for (int j = min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Function to find the count of required subarrays
int count_of_subarrays(int N)
{

    // The required count is the binomial coefficient
    // as explained in the approach above
    int count = binomialCoeff(2 * N - 1, N);

    return count;
}

// Driver Function
int main()
{

    int N = 3;

    cout << count_of_subarrays(N) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count non decreasing subarrays
// of size N from N Natural numbers
class GFG
{

// Returns value of Binomial Coefficient C(n, k)
static int binomialCoeff(int n, int k)
{
    int []C = new int[k + 1];

    // Since nC0 is 1
    C[0] = 1;

    for (int i = 1; i <= n; i++)
    {

        // Compute next row of pascal triangle using
        // the previous row
        for (int j = Math.min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Function to find the count of required subarrays
static int count_of_subarrays(int N)
{

    // The required count is the binomial coefficient
    // as explained in the approach above
    int count = binomialCoeff(2 * N - 1, N);

    return count;
}

// Driver Function
public static void main(String[] args)
{
    int N = 3;
    System.out.print(count_of_subarrays(N)+ "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count non decreasing subarrays
# of size N from N Natural numbers

# Returns value of Binomial Coefficient C(n, k)
def binomialCoeff(n, k) :

    C = [0] * (k + 1);

    # Since nC0 is 1
    C[0] = 1;

    for i in range(1, n + 1) :

        # Compute next row of pascal triangle using
        # the previous row
        for j in range(min(i, k), 0, -1) :
            C[j] = C[j] + C[j - 1];

    return C[k];

# Function to find the count of required subarrays
def count_of_subarrays(N) :

    # The required count is the binomial coefficient
    # as explained in the approach above
    count = binomialCoeff(2 * N - 1, N);

    return count;

# Driver Function
if __name__ == "__main__" :

    N = 3;

    print(count_of_subarrays(N)) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to count non decreasing subarrays
// of size N from N Natural numbers
using System;

class GFG
{

    // Returns value of Binomial Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int []C = new int[k + 1];

        // Since nC0 is 1
        C[0] = 1;

        for (int i = 1; i <= n; i++)
        {

            // Compute next row of pascal triangle using
            // the previous row
            for (int j = Math.Min(i, k); j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }
        return C[k];
    }

    // Function to find the count of required subarrays
    static int count_of_subarrays(int N)
    {

        // The required count is the binomial coefficient
        // as explained in the approach above
        int count = binomialCoeff(2 * N - 1, N);

        return count;
    }

    // Driver Function
    public static void Main()
    {
        int N = 3;
        Console.WriteLine(count_of_subarrays(N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to count non decreasing subarrays
// of size N from N Natural numbers

// Returns value of Binomial Coefficient C(n, k)
function binomialCoeff(n, k)
{
    var C = Array(k+1).fill(0);

    // Since nC0 is 1
    C[0] = 1;

    for (var i = 1; i <= n; i++) {

        // Compute next row of pascal triangle using
        // the previous row
        for (var j = Math.min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Function to find the count of required subarrays
function count_of_subarrays(N)
{

    // The required count is the binomial coefficient
    // as explained in the approach above
    var count = binomialCoeff(2 * N - 1, N);

    return count;
}

// Driver Function
var N = 3;
document.write( count_of_subarrays(N));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
10
```