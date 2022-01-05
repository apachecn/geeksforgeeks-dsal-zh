# 覆盖二进制数组所需的最短时间

> 原文:[https://www . geesforgeks . org/覆盖二进制数组所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-cover-a-binary-array/)

给定一个**整数 N** ，它表示最初用 0 填充的布尔数组的大小，还给定一个大小为 **K** 的**数组 arr[]** ，它由布尔数组中出现“1”的(基于 1 的)索引组成。现在，在一个时间单位，布尔数组中 arr[i]的相邻单元变为 1，即 **010** 变为 **111** 。找出将整个数组转换为 1 所需的最短时间。
**举例:**

> **输入:** N = 5，arr[] = {1，4}
> **输出:** 1
> **解释:**
> 最初布尔数组的大小为 5，用 5 个零填充。arr[]表示布尔数组中 1 出现的位置。因此，布尔数组变成 10010。
> 现在，在时间(t) = 1 时，第 3 和第 5 位置的 0 变为 1 = > 10111，同时，第 2 位置的 0 变为 1 = > 11111。所有 1 最初在同一时刻递增其相邻的 0。所以在 t=1 时，字符串被转换为全 1。
> **输入:** N=7，arr[] = {1，7}
> **输出:** 3
> **解释:**
> 在时间(t) = 1 时，10000001 变为 1100011
> 在时间(t) = 2 时，1100011 变为 1110111
> 在时间(t) = 3 时，1110111 变为 111

**方法:**
要解决上面提到的问题，我们必须观察到我们需要找到最长的**零段，直到 1 出现。例如，对于二进制数 00010000010000，最长的 0 段是从第 4 位到第 10 位。现在，观察指数之间有 50，这是一个奇数。因此，我们可以得出结论，要覆盖 5 个零，我们需要 5/2 + 1，也就是 3 个时间单位，因为所有其他部分将在小于或等于 3 个时间单位的情况下被填充。** 

*   **如果最长的零段是奇数，那么我们可以得出结论，需要 x/2 + 1 时间单位，其中 x 是最长段中的 0 数。**
*   **如果最长的零段是偶数，那么我们可以得出结论，需要 x/2 个时间单位，其中 x 是最长段中的 0 数。**

**我们可以计算连续段的最大长度，直到布尔数组中出现 1，然后根据长度是奇数还是偶数返回答案。
**以下是上述方法的实施:**** 

## **C++**

```
// CPP implementation to find the
// Minimum time required to cover a Binary Array
#include <bits/stdc++.h>
using namespace std;

// function to calculate the time
int solve(vector<int> arr, int n)
{

    int k = arr.size();

    // Map to mark or store the binary values
    bool mp[n + 2];

    // Firstly fill the boolean
    // array with all zeroes
    for (int i = 0; i <= n; i++) {
        mp[i] = 0;
    }

    // Mark the 1s
    for (int i = 0; i < k; i++) {
        mp[arr[i]] = 1;
    }

    // Number of 0s until first '1' occurs
    int leftSegment = arr[0] - 1;

    // Maximum Number of 0s in between 2 '1's.
    for (int i = 1; i < k; i++) {
        leftSegment = max(leftSegment, arr[i] - arr[i - 1] - 1);
    }

    // Number of 0s from right until first '1' occurs
    int rightSegment = n - arr[k - 1];

    // Return maximum from left and right segment
    int maxSegment = max(leftSegment, rightSegment);

    int tim;

    // check if count is odd
    if (maxSegment & 1)
        tim = (maxSegment / 2) + 1;

    // check ifcount is even
    else
        tim = maxSegment / 2;

    // return the time
    return tim;
}

// driver code
int main()
{
    // initialise N
    int N = 5;

    // array initialisation
    vector<int> arr = { 1, 4 };

    cout << solve(arr, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the
// Minimum time required to cover a Binary Array
class GFG {

    // function to calculate the time
    static int solve(int []arr, int n)
    {

        int k = arr.length;

        // Map to mark or store the binary values
        int mp[] = new int[n + 2];

        // Firstly fill the boolean
        // array with all zeroes
        for (int i = 0; i <= n; i++) {
            mp[i] = 0;
        }

        // Mark the 1s
        for (int i = 0; i < k; i++) {
            mp[arr[i]] = 1;
        }

        // Number of 0s until first '1' occurs
        int leftSegment = arr[0] - 1;

        // Maximum Number of 0s in between 2 '1's.
        for (int i = 1; i < k; i++) {
            leftSegment = Math.max(leftSegment, arr[i] - arr[i - 1] - 1);
        }

        // Number of 0s from right until first '1' occurs
        int rightSegment = n - arr[k - 1];

        // Return maximum from left and right segment
        int maxSegment = Math.max(leftSegment, rightSegment);

        int tim;

        // check if count is odd
        if ((maxSegment & 1) == 1)
            tim = (maxSegment / 2) + 1;

        // check ifcount is even
        else
            tim = maxSegment / 2;

        // return the time
        return tim;
    }

    // driver code
    public static void main (String[] args)
    {
        // initialise N
        int N = 5;

        // array initialisation
        int arr[] = { 1, 4 };

        System.out.println(solve(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## **蟒蛇 3**

```
# Python3 implementation to find the
# Minimum time required to cover a Binary Array

# function to calculate the time
def solve(arr, n) :

    k = len(arr)

    # Map to mark or store the binary values
    # Firstly fill the boolean
    # array with all zeroes
    mp = [False for i in range(n + 2)]

    # Mark the 1s
    for i in range(k) :
        mp[arr[i]] = True

    # Number of 0s until first '1' occurs
    leftSegment = arr[0] - 1

    # Maximum Number of 0s in between 2 '1's.
    for i in range(1,k) :
        leftSegment = max(leftSegment, arr[i] - arr[i - 1] - 1)

    # Number of 0s from right until first '1' occurs
    rightSegment = n - arr[k - 1]

    # Return maximum from left and right segment
    maxSegment = max(leftSegment, rightSegment);

    tim = 0

    # check if count is odd
    if (maxSegment & 1) :
        tim = (maxSegment // 2) + 1

    # check ifcount is even
    else :
        tim = maxSegment // 2

    # return the time
    return tim

# Driver code
# initialise N
N = 5

# array initialisation
arr = [ 1, 4 ]

print(solve(arr, N))

# This code is contributed by Sanjit_Prasad
```

## **C#**

```
// C# implementation to find the
// Minimum time required to cover
// a Binary Array
using System;

class GFG{

// Function to calculate the time
static int solve(int[] arr, int n)
{
    int k = arr.Length;

    // Map to mark or store the binary values
    int[] mp = new int[n + 2];

    // Firstly fill the boolean
    // array with all zeroes
    for(int i = 0; i <= n; i++)
    {
        mp[i] = 0;
    }

    // Mark the 1s
    for(int i = 0; i < k; i++)
    {
        mp[arr[i]] = 1;
    }

    // Number of 0s until first '1' occurs
    int leftSegment = arr[0] - 1;

    // Maximum Number of 0s in between 2 '1's.
    for(int i = 1; i < k; i++)
    {
        leftSegment = Math.Max(leftSegment,
                               arr[i] -
                               arr[i - 1] - 1);
    }

    // Number of 0s from right until first '1' occurs
    int rightSegment = n - arr[k - 1];

    // Return maximum from left and right segment
    int maxSegment = Math.Max(leftSegment,
                              rightSegment);

    int tim;

    // Check if count is odd
    if ((maxSegment & 1) == 1)
        tim = (maxSegment / 2) + 1;

    // Check ifcount is even
    else
        tim = maxSegment / 2;

    // Return the time
    return tim;
}

// Driver code
public static void Main ()
{

    // Initialise N
    int N = 5;

    // Array initialisation
    int[] arr = { 1, 4 };

    Console.Write(solve(arr, N));
}
}

// This code is contributed by chitranayal
```

## **java 描述语言**

```
<script>

// JavaScript implementation to find the
// Minimum time required to cover a Binary Array

    // function to calculate the time
    function solve(arr, n)
    {

        let k = arr.length;

        // Map to mark or store the binary values
        let mp = Array.from({length: n+2}, (_, i) => 0);

        // Firstly fill the boolean
        // array with all zeroes
        for (let i = 0; i <= n; i++) {
            mp[i] = 0;
        }

        // Mark the 1s
        for (let i = 0; i < k; i++) {
            mp[arr[i]] = 1;
        }

        // Number of 0s until first '1' occurs
        let leftSegment = arr[0] - 1;

        // Maximum Number of 0s in between 2 '1's.
        for (let i = 1; i < k; i++) {
            leftSegment = Math.max(leftSegment, arr[i] -
            arr[i - 1] - 1);
        }

        // Number of 0s from right until first '1' occurs
        let rightSegment = n - arr[k - 1];

        // Return maximum from left and right segment
        let maxSegment = Math.max(leftSegment, rightSegment);

        let tim;

        // check if count is odd
        if ((maxSegment & 1) == 1)
            tim = (maxSegment / 2) + 1;

        // check ifcount is even
        else
            tim = maxSegment / 2;

        // return the time
        return tim;
    }
// Driver Code

    // initialise N
        let N = 5;

        // array initialisation
        let arr = [ 1, 4 ];

        document.write(solve(arr, N));

</script>
```

****Output:** 

```
1
```** 

**时间复杂度:0(N)**

**辅助空间:O(N)**