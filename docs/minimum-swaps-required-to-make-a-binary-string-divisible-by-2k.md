# 使二进制字符串可被 2^k 除尽所需的最小交换次数

> 原文:[https://www . geesforgeks . org/minimum-swaps-required-make-a-binary-string-除尽-2k/](https://www.geeksforgeeks.org/minimum-swaps-required-to-make-a-binary-string-divisible-by-2k/)

给定一个长度为 **N** 的二进制字符串 **S** 和一个整数 **K** ，任务是找到使二进制字符串被 **2 <sup>K</sup>** 整除所需的最小相邻交换次数。如果不可能，则打印 **-1** 。

**示例:**

> **输入:**S =“100111”，K = 2
> **输出:** 6
> 将最右边的零对换 3 次
> 向右，我们得到“101110”。
> 将第二个最右边的零
> 向右对换 3 次，得到“111100”。
> **输入:**S =“1011”，K = 2
> **输出:** -1

**方法 1:** 一种方法是从最右边的零开始交换。所以，让我们把这个问题换个更简单的说法。需要最少数量的交换，以便在右端至少有 **K** 个连续的零可用。
一种方法是模拟交换。从最右边的零开始，交换它，直到它的右边有 1，它不是字符串的结尾。这将对最右边的零 **K** 执行。这种方法的时间复杂度将是 **O(N * K)** 。

**方法 2:** 这里表现更好的关键是避免做模拟。
T3【观察:

> 在 **K** 最右边的零中，每个零需要被交换 **X** 次，其中 **X** 是该零右边的 1 的数量。

因此，对于 **K** 最右边的零，任务是找到它们中每一个右边的 1 的数量的和。

**算法:**

*   初始化变量 **c_zero = 0** ， **c_one = 0** 和 **ans = 0** 。
*   运行从**I = N–1**到 **i = 0** 的循环。
    *   如果 **S[i] = 0** 则更新 **c_zero = c_zero + 1** 和 **ans = ans + c_one** 。
    *   如果 **S[i] = 1** ，则更新 **c_one = c_one + 1** 。
    *   如果 **c_zero = K** 则断开。
*   如果 **c_zero < K** 则返回 **-1** 。
*   最后，返回**和**。

因此，这种方法的时间复杂度将是 **O(N)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum swaps required
int findMinSwaps(string s, int k)
{
    // To store the final answer
    int ans = 0;

    // To store the count of one and zero
    int c_one = 0, c_zero = 0;

    // Loop from end of the string
    for (int i = s.size() - 1; i >= 0; i--) {

        // If s[i] = 1
        if (s[i] == '1')
            c_one++;

        // If s[i] = 0
        if (s[i] == '0')
            c_zero++, ans += c_one;

        // If c_zero = k
        if (c_zero == k)
            break;
    }

    // If the result can't
    // be achieved
    if (c_zero < k)
        return -1;

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    string s = "100111";
    int k = 2;

    cout << findMinSwaps(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the minimum swaps required
    static int findMinSwaps(String s, int k)
    {
        // To store the final answer
        int ans = 0;

        // To store the count of one and zero
        int c_one = 0, c_zero = 0;

        // Loop from end of the string
        for (int i = s.length() - 1; i >= 0; i--)
        {

            // If s[i] = 1
            if (s.charAt(i) == '1')
                c_one++;

            // If s[i] = 0
            if (s.charAt(i) == '0')
            {
                c_zero++;
                ans += c_one;
            }

            // If c_zero = k
            if (c_zero == k)
                break;
        }

        // If the result can't
        // be achieved
        if (c_zero < k)
            return -1;

        // Return the final answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "100111";
        int k = 2;

        System.out.println(findMinSwaps(s, k));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum swaps required
def findMinSwaps(s, k) :

    # To store the final answer
    ans = 0;

    # To store the count of one and zero
    c_one = 0; c_zero = 0;

    # Loop from end of the string
    for i in range(len(s)-1, -1, -1) :

        # If s[i] = 1
        if (s[i] == '1') :
            c_one += 1;

        # If s[i] = 0
        if (s[i] == '0') :
            c_zero += 1;
            ans += c_one;

        # If c_zero = k
        if (c_zero == k) :
            break;

    # If the result can't
    # be achieved
    if (c_zero < k) :
        return -1;

    # Return the final answer
    return ans;

# Driver code
if __name__ == "__main__" :

    s = "100111";
    k = 2;

    print(findMinSwaps(s, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum swaps required
    static int findMinSwaps(string s, int k)
    {
        // To store the final answer
        int ans = 0;

        // To store the count of one and zero
        int c_one = 0, c_zero = 0;

        // Loop from end of the string
        for (int i = s.Length - 1; i >= 0; i--)
        {

            // If s[i] = 1
            if (s[i] == '1')
                c_one++;

            // If s[i] = 0
            if (s[i] == '0')
            {
                c_zero++;
                ans += c_one;
            }

            // If c_zero = k
            if (c_zero == k)
                break;
        }

        // If the result can't
        // be achieved
        if (c_zero < k)
            return -1;

        // Return the final answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        string s = "100111";
        int k = 2;

        Console.WriteLine(findMinSwaps(s, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum swaps required
function findMinSwaps(s, k)
{
    // To store the final answer
    var ans = 0;

    // To store the count of one and zero
    var c_one = 0, c_zero = 0;

    // Loop from end of the string
    for (var i = s.length - 1; i >= 0; i--) {

        // If s[i] = 1
        if (s[i] == '1')
            c_one++;

        // If s[i] = 0
        if (s[i] == '0')
            c_zero++, ans += c_one;

        // If c_zero = k
        if (c_zero == k)
            break;
    }

    // If the result can't
    // be achieved
    if (c_zero < k)
        return -1;

    // Return the final answer
    return ans;
}

// Driver code
var s = "100111";
var k = 2;
document.write( findMinSwaps(s, k));

</script>
```

**Output:** 

```
6
```