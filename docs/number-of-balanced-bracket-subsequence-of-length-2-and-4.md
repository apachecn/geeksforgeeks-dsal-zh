# 长度为 2 和 4 的平衡括号子序列的数量

> 原文:[https://www . geeksforgeeks . org/number-of-balanced-branch-sequence-of-length-2-and-4/](https://www.geeksforgeeks.org/number-of-balanced-bracket-subsequence-of-length-2-and-4/)

给定偶数长度的括号序列。任务是从给定的长度为 2 和 4 的序列中找出多少种方法来制作平衡的括号子序列。
序列()是长度为 2 的括号序列。子序列是一个序列，可以通过删除一些元素或不删除元素而不改变其余元素的顺序，从另一个序列中派生出来。
**注:**“1”代表左括号，“2”代表右括号

**示例:**

```
Input: 1 2 1 1 2 2
Output: 14

Input: 1 2 1 2
Output: 4
```

**方法:**对于**长度为 2 的子序列**，我们将只看到每个 1 有多少个 2，这可以通过取序列中存在的 2 的数量的简单后缀和来容易地实现。所以首先取序列中 2 个数的后缀和。
对于 l **第 4 个子序列**有 2 个选择:

> 第一个是 1 1 2 2
> 另一个是 1 2 1 2。

*   对于第一个，从左到右运行一个循环以获得第一个开括号一个内部循环以获得下一个开括号现在从后缀数组中，我们可以获得第二个开括号之后的 2 的计数，并通过计数*(count-1)/2 计算子序列的数量，因为对于每个内开括号的结束括号，我们获得第一个开括号的 count-1 选择数量。
*   对于第二种类型的子序列，我们再次从左到右运行一个循环来获得第一个左括号，一个内部循环来获得下一个左括号。然后，我们通过简单地减去第二个左括号后的 2 的计数和第一个左括号后的 2 的计数并将其乘以第二个左括号后的 2 的计数来计算子序列的数量(我们从频率后缀数组中获得所有这些值)。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

void countWays(int a[], int n)
{
    int i, j;
    long suff[n];
    if (a[n - 1] == 2)
        suff[n - 1] = 1;

    // Taking the frequency suffix sum of the
    // number of 2's present after every index
    for (i = n - 2; i >= 0; i--)
    {
        if (a[i] == 2)
            suff[i] = suff[i + 1] + 1;
        else
            suff[i] = suff[i + 1];
    }

    // Storing the count of subsequence
    long ss = 0;

    // Subsequence of length 2
    for (i = 0; i < n; i++)
    {
        if (a[i] == 1)
            ss += suff[i];
    }

    // Subsequence of length 4 of type 1 1 2 2
    for (i = 0; i < n; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if (a[i] == 1 && a[j] == 1 && suff[j] >= 2)
            {
                ss += (suff[j]) * (suff[j] - 1) / 2;
            }
        }
    }

    // Subsequence of length 4 of type 1 2 1 2
    for (i = 0; i < n; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if (a[i] == 1 && a[j] == 1
                && (suff[i] - suff[j]) >= 1
                && suff[j] >= 1)
            {
                ss += (suff[i] - suff[j]) * suff[j];
            }
        }
    }
    cout << (ss);
}

// Driver code
int main()
{

    int a[] = { 1, 2, 1, 1, 2, 2 };
    int n = 6;
    countWays(a, n);
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {

    public static void countWays(int a[], int n)
    {

        int i, j;
        long suff[] = new long[n];
        if (a[n - 1] == 2)
            suff[n - 1] = 1;

        // Taking the frequency suffix sum of the
        // number of 2's present after every index
        for (i = n - 2; i >= 0; i--)
        {
            if (a[i] == 2)
                suff[i] = suff[i + 1] + 1;
            else
                suff[i] = suff[i + 1];
        }

        // Storing the count of subsequence
        long ss = 0;

        // Subsequence of length 2
        for (i = 0; i < n; i++)
        {
            if (a[i] == 1)
                ss += suff[i];
        }

        // Subsequence of length 4 of type 1 1 2 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1
                    && suff[j] >= 2)
                {
                    ss += (suff[j]) * (suff[j] - 1) / 2;
                }
            }
        }

        // Subsequence of length 4 of type 1 2 1 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1
                    && (suff[i] - suff[j]) >= 1
                    && suff[j] >= 1)
                {
                    ss += (suff[i] - suff[j]) * suff[j];
                }
            }
        }
        System.out.println(ss);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int a[] = { 1, 2, 1, 1, 2, 2 };
        int n = 6;
        countWays(a, n);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

def countWays(a, n):

    suff = [0] * n
    if (a[n - 1] == 2):
        suff[n - 1] = 1

    # Taking the frequency suffix sum
    # of the number of 2's present
    # after every index
    for i in range(n - 2, -1, -1):
        if (a[i] == 2):
            suff[i] = suff[i + 1] + 1
        else:
            suff[i] = suff[i + 1]

    # Storing the count of subsequence
    ss = 0

    # Subsequence of length 2
    for i in range(n):
        if (a[i] == 1):
            ss += suff[i]

    # Subsequence of length 4 of type 1 1 2 2
    for i in range(n):
        for j in range(i + 1, n):
            if (a[i] == 1 and
                    a[j] == 1 and suff[j] >= 2):
                ss += (suff[j]) * (suff[j] - 1) // 2

    # Subsequence of length 4
    # of type 1 2 1 2
    for i in range(n):
        for j in range(i + 1, n):
            if (a[i] == 1 and a[j] == 1 and
                (suff[i] - suff[j]) >= 1 and
                    suff[j] >= 1):
                ss += (suff[i] - suff[j]) * suff[j]

    print(ss)

# Driver Code
if __name__ == "__main__":

    a = [1, 2, 1, 1, 2, 2]
    n = 6
    countWays(a, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of
// above approach
using System;
class GFG
{
    public static void countWays(int[] a, int n)
    {

        int i, j;
        long[] suff = new long[n];
        if (a[n - 1] == 2)
            suff[n - 1] = 1;

        // Taking the frequency suffix
        // sum of the number of 2's
        // present after every index
        for (i = n - 2; i >= 0; i--)
        {
            if (a[i] == 2)
                suff[i] = suff[i + 1] + 1;
            else
                suff[i] = suff[i + 1];
        }

        // Storing the count of subsequence
        long ss = 0;

        // Subsequence of length 2
        for (i = 0; i < n; i++)
        {
            if (a[i] == 1)
                ss += suff[i];
        }

        // Subsequence of length 4
        // of type 1 1 2 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1
                    && suff[j] >= 2) {
                    ss += (suff[j]) * (suff[j] - 1) / 2;
                }
            }
        }

        // Subsequence of length 4
        // of type 1 2 1 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1
                    && (suff[i] - suff[j]) >= 1
                    && suff[j] >= 1) {
                    ss += (suff[i] - suff[j]) * suff[j];
                }
            }
        }
        Console.WriteLine(ss);
    }

    // Driver Code
    public static void Main()
    {
        int[] a = { 1, 2, 1, 1, 2, 2 };
        int n = 6;
        countWays(a, n);
    }
}

// This code is contributed by Shashank
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    function countWays(a, n)
    {
        let i, j;
        let suff = new Array(n);
        if (a[n - 1] == 2)
            suff[n - 1] = 1;

        // Taking the frequency suffix sum of the
        // number of 2's present after every index
        for (i = n - 2; i >= 0; i--)
        {
            if (a[i] == 2)
                suff[i] = suff[i + 1] + 1;
            else
                suff[i] = suff[i + 1];
        }

        // Storing the count of subsequence
        let ss = 0;

        // Subsequence of length 2
        for (i = 0; i < n; i++)
        {
            if (a[i] == 1)
                ss += suff[i];
        }

        // Subsequence of length 4 of type 1 1 2 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1 && suff[j] >= 2)
                {
                    ss += (suff[j]) * (suff[j] - 1) / 2;
                }
            }
        }

        // Subsequence of length 4 of type 1 2 1 2
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                if (a[i] == 1 && a[j] == 1
                    && (suff[i] - suff[j]) >= 1
                    && suff[j] >= 1)
                {
                    ss += (suff[i] - suff[j]) * suff[j];
                }
            }
        }
        document.write(ss);
    }

      let a = [ 1, 2, 1, 1, 2, 2 ];
    let n = 6;
    countWays(a, n);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
14
```

**时间复杂度:**O(N * N)
T3】辅助复杂度: O(N)