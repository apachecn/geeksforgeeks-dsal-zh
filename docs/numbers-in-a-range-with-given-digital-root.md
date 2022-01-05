# 给定数字根范围内的数字

> 原文:[https://www . geesforgeks . org/numbers-in-a-range-with-给定-digital-root/](https://www.geeksforgeeks.org/numbers-in-a-range-with-given-digital-root/)

给定一个整数 **K** 和一系列连续的数字**【L，R】**。任务是统计给定范围内以数字根为 K (1 ≤ K ≤ 9)的数字。[数字根](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/)是一个数字的位数的总和，直到它变成一个位数。例如，256 - > 2 + 5 + 6 = 13 - > 1 + 3 = 4。

**示例:**

> **输入:** L = 10，R = 22，K = 3
> **输出:** 2
> 12 和 21 是数字和为 3 的范围内唯一的数字。
> 
> **输入:** L = 100，R = 200，K = 5
> **输出:** 11

**进场:**

*   首先要注意的是，对于任何数字，数字总和等于数字% 9。如果余数为 0，则位数之和为 9。
*   所以如果 K = 9，那么用 0 代替 K。
*   任务，现在是找到 L 到 R 范围内的数的计数，模 9 等于 k
*   将整个范围分成以 L (TotalRange / 9)开始的 9 个可能的最大组，因为在每个范围内将正好有一个模 9 等于 k 的数字
*   从 R 到 R 循环元素的剩余数量–剩余元素的计数，并检查是否有任何数量满足条件。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the count
// of required numbers
int countNumbers(int L, int R, int K)
{
    if (K == 9)
        K = 0;

    // Count of numbers present
    // in given range
    int totalnumbers = R - L + 1;

    // Number of groups of 9 elements
    // starting from L
    int factor9 = totalnumbers / 9;

    // Left over elements not covered
    // in factor 9
    int rem = totalnumbers % 9;

    // One Number in each group of 9
    int ans = factor9;

    // To check if any number in rem
    // satisfy the property
    for (int i = R; i > R - rem; i--) {
        int rem1 = i % 9;
        if (rem1 == K)
            ans++;
    }

    return ans;
}

// Driver code
int main()
{
    int L = 10;
    int R = 22;
    int K = 3;
    cout << countNumbers(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

// Function to return the count
// of required numbers
    static int countNumbers(int L, int R, int K) {
        if (K == 9) {
            K = 0;
        }

        // Count of numbers present
        // in given range
        int totalnumbers = R - L + 1;

        // Number of groups of 9 elements
        // starting from L
        int factor9 = totalnumbers / 9;

        // Left over elements not covered
        // in factor 9
        int rem = totalnumbers % 9;

        // One Number in each group of 9
        int ans = factor9;

        // To check if any number in rem
        // satisfy the property
        for (int i = R; i > R - rem; i--) {
            int rem1 = i % 9;
            if (rem1 == K) {
                ans++;
            }
        }

        return ans;
    }

// Driver code
    public static void main(String[] args) {
        int L = 10;
        int R = 22;
        int K = 3;
        System.out.println(countNumbers(L, R, K));
    }
}
/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required numbers
def countNumbers(L, R, K):

    if (K == 9):
        K = 0

    # Count of numbers present
    # in given range
    totalnumbers = R - L + 1

    # Number of groups of 9 elements
    # starting from L
    factor9 = totalnumbers // 9

    # Left over elements not covered
    # in factor 9
    rem = totalnumbers % 9

    # One Number in each group of 9
    ans = factor9

    # To check if any number in rem
    # satisfy the property
    for i in range(R, R - rem, -1):
        rem1 = i % 9
        if (rem1 == K):
            ans += 1

    return ans

# Driver code
L = 10
R = 22
K = 3
print(countNumbers(L, R, K))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System ;

class GFG
{

    // Function to return the count
    // of required numbers
    static int countNumbers(int L, int R, int K)
    {
        if (K == 9)
        {
            K = 0;
        }

        // Count of numbers present
        // in given range
        int totalnumbers = R - L + 1;

        // Number of groups of 9 elements
        // starting from L
        int factor9 = totalnumbers / 9;

        // Left over elements not covered
        // in factor 9
        int rem = totalnumbers % 9;

        // One Number in each group of 9
        int ans = factor9;

        // To check if any number in rem
        // satisfy the property
        for (int i = R; i > R - rem; i--)
        {
            int rem1 = i % 9;
            if (rem1 == K)
            {
                ans++;
            }
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int L = 10;
        int R = 22;
        int K = 3;

        Console.WriteLine(countNumbers(L, R, K));
    }
}

/* This code is contributed by Ryuga */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of required numbers
function countNumbers($L, $R, $K)
{
    if ($K == 9)
        $K = 0;

    // Count of numbers present
    // in given range
    $totalnumbers = $R - $L + 1;

    // Number of groups of 9 elements
    // starting from L
    $factor9 = intval($totalnumbers / 9);

    // Left over elements not covered
    // in factor 9
    $rem = $totalnumbers % 9;

    // One Number in each group of 9
    $ans = $factor9;

    // To check if any number in rem
    // satisfy the property
    for ($i = $R; $i > $R - $rem; $i--)
    {
        $rem1 = $i % 9;
        if ($rem1 == $K)
            $ans++;
    }

    return $ans;
}

// Driver code
$L = 10;
$R = 22;
$K = 3;
echo countNumbers($L, $R, $K);

// This code is contributed by Ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of required numbers
function countNumbers(L, R, K)
{
    if (K == 9)
    {
        K = 0;
    }

    // Count of numbers present
    // in given range
    var totalnumbers = R - L + 1;

    // Number of groups of 9 elements
    // starting from L
    var factor9 = totalnumbers / 9;

    // Left over elements not covered
    // in factor 9
    var rem = totalnumbers % 9;

    // One Number in each group of 9
    var ans = factor9;

    // To check if any number in rem
    // satisfy the property
    for(var i = R; i > R - rem; i--)
    {
        var rem1 = i % 9;
        if (rem1 == K)
        {
            ans++;
        }
    }

    return ans;
}

// Driver Code
var L = 10;
var R = 22;
var K = 3;

document.write(Math.round(countNumbers(L, R, K)));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
2
```