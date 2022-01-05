# 检查是否存在奇数和的长度为 K 的子序列

> 原文:[https://www . geeksforgeeks . org/check-如果存在奇数和长度为 k 的子序列/](https://www.geeksforgeeks.org/check-if-a-subsequence-of-length-k-with-odd-sum-exists/)

给定整数数组 **arr[]** ，任务是检查是否有可能从数组中获得 **K** 元素的子序列，使得它们的和为**奇数**。如果可能，打印**是**。否则，打印**否**。
**举例:**

> **输入:** arr[] = {2，5，6，7，4}，K = 3
> **输出:**是
> **解释:**
> 子序列{2，5，6}，{ 2，6，7}和{ 2，7，4 }有奇数和
> **输入:** arr[] = { 1，5，7，11 }，K = 4
> **输出:**否
> 因此不存在这样的子序列。

**天真方法:**
解决这个问题最简单的方法是生成所有长度为 **K** 的子序列，并检查这些子序列中是否有任何一个具有奇数和。这种方法的时间复杂度是指数级的，因此效率很低。
**有效方法:**
解决上述问题的有效方法是**计算数组中奇数元素**的数量，然后，当不可能找到奇数和的子序列时，简单地检查所有的边缘情况。
当不能生成这样的子序列时要考虑的边缘情况如下:

*   如果数组中没有奇数元素，任何子序列将只包含偶数元素，并且将获得一个偶数和。因此，不可能生成奇数和的子序列。
*   如果 **K** 是偶数，并且数组中没有偶数元素，则不可能有奇数和的子序列。

对于所有其他情况，有可能生成一个奇数和的子序列。
以下是上述方法的实施:

## C++

```
// C++ program to check if a
// subsequence of length K
// with odd sum exists in the
// given array
#include <bits/stdc++.h>
using namespace std;

// Function to check if any required
// subsequence exists or not
bool isSubseqPossible(int arr[], int N, int K)
{
    int i;
    // Store count of odd and
    // even elements in the array
    int odd = 0, even = 0;

    // Calculate the count of
    // odd and even elements
    for (i = 0; i < N; i++) {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If no odd elements exists
    // or no even elements exists
    // when K is even
    if (odd == 0
|| (even == 0 && K % 2 == 0))

        // Subsequence is not possible
        return false;

    // Possible otherwise
    return true;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 5, 7, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    cout << (isSubseqPossible(arr, N, K)
                 ? "Yes"
                 : "No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// subsequence of length K
// with odd sum exists in the
// given array
class GFG{

// Function to check if any required
// subsequence exists or not
static boolean isSubseqPossible(int []arr,
                             int N, int K)
{
    int i;

    // Store count of odd and
    // even elements in the array
    int odd = 0, even = 0;

    // Calculate the count of
    // odd and even elements
    for (i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If no odd elements exists
    // or no even elements exists
    // when K is even
    if (odd == 0 || (even == 0 && K % 2 == 0))

        // Subsequence is not possible
        return false;

    // Possible otherwise
    return true;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 2, 3, 5, 7, 4 };
    int N = arr.length;
    int K = 3;
    System.out.print(isSubseqPossible(arr, N, K) ?
                                           "Yes" : "No");
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to check if a subsequence
# of length K with odd sum exists in the
# given array

# Function to check if any required
# subsequence exists or not
def isSubseqPossible(arr, N, K):

    i = 0

    # Store count of odd and
    # even elements in the array
    odd = 0
    even = 0

    # Calculate the count of
    # odd and even elements
    for i in range(N):
        if (arr[i] % 2 == 1):
            odd += 1
        else:
            even += 1

    # If no odd element exists or no
    # even element exists when K even
    if (odd == 0 or (even == 0 and K % 2 == 0)):

        # Subsequence is not possible
        return False

    # Otherwise possible
    return True

# Driver code
if __name__ == '__main__':

    arr = [ 2, 3, 5, 7, 4 ]
    N = len(arr)
    K = 3

    print("Yes" if isSubseqPossible(arr, N, K) else "No")

# This code is contributed by himanshu77
```

## C#

```
// C# program to check if a
// subsequence of length K
// with odd sum exists in the
// given array
using System;
class GFG{

// Function to check if any required
// subsequence exists or not
static bool isSubseqPossible(int []arr,
                             int N, int K)
{
    int i;

    // Store count of odd and
    // even elements in the array
    int odd = 0, even = 0;

    // Calculate the count of
    // odd and even elements
    for (i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If no odd elements exists
    // or no even elements exists
    // when K is even
    if (odd == 0 || (even == 0 && K % 2 == 0))

        // Subsequence is not possible
        return false;

    // Possible otherwise
    return true;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 3, 5, 7, 4 };
    int N = arr.Length;
    int K = 3;
    Console.Write(isSubseqPossible(arr, N, K) ?
                                        "Yes" : "No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to check if a
// subsequence of length K
// with odd sum exists in the
// given array

// Function to check if any required
// subsequence exists or not
function isSubseqPossible(arr, N, K)
{
    let i;

    // Store count of odd and
    // even elements in the array
    let odd = 0, even = 0;

    // Calculate the count of
    // odd and even elements
    for (i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If no odd elements exists
    // or no even elements exists
    // when K is even
    if (odd == 0 || (even == 0 && K % 2 == 0))

        // Subsequence is not possible
        return false;

    // Possible otherwise
    return true;
}

// Driver Code

    let arr = [ 2, 3, 5, 7, 4 ];
    let N = arr.length;
    let K = 3;
    document.write(isSubseqPossible(arr, N, K) ?
                                     "Yes" : "No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*