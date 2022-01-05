# 从 N 个男人中选择一组 X 个男人的全部方法，包括或不包括一个特定的男人

> 原文:[https://www . geesforgeks . org/total-way-从 n-men-with-or-not-include-a-special-man 中选择一组 x-men/](https://www.geeksforgeeks.org/total-ways-of-selecting-a-group-of-x-men-from-n-men-with-or-without-including-a-particular-man/)

给定两个整数 **X** 和 **N** 。任务是找到从一组 **N** 男人中选择 **X** 男人的方法总数，包括或不包括一个特定的男人。
**举例:**

> **输入:**N = 3 X = 2
> T3】输出: 3
> 包括一个人说 M1，途径可以是(M1、M2)和(M1、M3)。
> 排除一个人说 M1，唯一的办法就是(M2、M3)。
> 总路= 2 + 1 = 3。
> **输入:** N = 5 X = 3
> **输出:** 10

**途径:**从 **N 个男人**中选择 **X 个男人**的途径总数为**<sup>N</sup>C<sub>X</sub>**

*   **包括特定的男人:**我们可以从**<sup>N–1</sup>C<sub>X–1</sub>**中的**(N–1)**中选择**(X–1)男人**。
*   **排除特定男性:**我们可以从**<sup>N–1</sup>C<sub>X</sub>**中的**(N–1)**中选择 **X 男性**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value of nCr
int nCr(int n, int r)
{

    // Initialize the answer
    int ans = 1;

    for (int i = 1; i <= r; i += 1) {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans /= i;
    }
    return ans;
}

// Function to return the count of ways
int total_ways(int N, int X)
{
    return (nCr(N - 1, X - 1) + nCr(N - 1, X));
}

// Driver code
int main()
{
    int N = 5, X = 3;

    cout << total_ways(N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the value of nCr
static int nCr(int n, int r)
{

    // Initialize the answer
    int ans = 1;

    for (int i = 1; i <= r; i += 1)
    {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans /= i;
    }
    return ans;
}

// Function to return the count of ways
static int total_ways(int N, int X)
{
    return (nCr(N - 1, X - 1) + nCr(N - 1, X));
}

// Driver code
public static void main (String[] args)
{
    int N = 5, X = 3;

    System.out.println (total_ways(N, X));
}
}

// This code is contributed by Sachin
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value of nCr
def nCr(n, r) :

    # Initialize the answer
    ans = 1;

    for i in range(1, r + 1) :

        # Divide simultaneously by
        # i to avoid overflow
        ans *= (n - r + i);
        ans //= i;

    return ans;

# Function to return the count of ways
def total_ways(N, X) :

    return (nCr(N - 1, X - 1) + nCr(N - 1, X));

# Driver code
if __name__ == "__main__" :

    N = 5; X = 3;

    print(total_ways(N, X));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the value of nCr
static int nCr(int n, int r)
{

    // Initialize the answer
    int ans = 1;

    for (int i = 1; i <= r; i += 1)
    {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans /= i;
    }
    return ans;
}

// Function to return the count of ways
static int total_ways(int N, int X)
{
    return (nCr(N - 1, X - 1) + nCr(N - 1, X));
}

// Driver code
public static void Main (String[] args)
{
    int N = 5, X = 3;

    Console.WriteLine(total_ways(N, X));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the value of nCr
    function nCr(n, r)
    {

        // Initialize the answer
        let ans = 1;

        for (let i = 1; i <= r; i += 1) {

            // Divide simultaneously by
            // i to avoid overflow
            ans *= (n - r + i);
            ans /= i;
        }
        return ans;
    }

    // Function to return the count of ways

    function total_ways(N, X)
    {
        return (nCr(N - 1, X - 1) + nCr(N - 1, X));
    }

    let N = 5, X = 3;

    document.write(total_ways(N, X));

</script>
```

**Output:** 

```
10
```