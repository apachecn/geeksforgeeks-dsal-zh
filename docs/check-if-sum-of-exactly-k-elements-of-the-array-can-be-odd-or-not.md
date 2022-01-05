# 检查数组中正好 K 个元素的和是否为奇数

> 原文:[https://www . geesforgeks . org/check-if-sum-of-of-the-of-the-array-elements-can-odd-or-not/](https://www.geeksforgeeks.org/check-if-sum-of-exactly-k-elements-of-the-array-can-be-odd-or-not/)

给定一个数组， **arr[]** 和一个整数 **K** 。通过选择数组中精确的 **K** 元素，检查是否有可能得到一个奇数和。

**示例:**

> **输入:** arr[] = {1，2，3}，K = 2
> **输出:**可能的
> **解释:**
> {2，3} ⇾ 2 + 3 = 5
> 
> **输入:** arr[] = {2，2，4，2}，K = 4
> **输出:**不可能
> **解释:** {2，2，4，2} ⇾ 2 + 2 + 4 + 2 = 10
> 因为 k 等于数组的大小，所以没有其他可能

**进场:**观察发现有三种情况。

*   首先，计算奇数和偶数元素的数量。
*   **情况 1:** 当所有元素都是偶数时。那么，和将总是偶数，而不考虑 K 的值为**偶数+偶数=偶数**。
*   **情况 2:** 当所有元素都是奇数时。那么，和将只取决于 K 的值
    **如果 K 是奇数**，那么和将是奇数，因为每个奇数对使和为偶数，最终，一个奇数元素使和为奇数，因为**偶数+奇数=奇数**。
    **如果 K 是偶数，**则每个奇数元素配对成为偶数，因此总和成为偶数。
*   **情况 3:** 当 K < = N 时，那么和只取决于奇数元素的个数。如果奇数元素的数量是偶数，那么和将是偶数，因为**奇数+奇数=偶数**，这意味着每个奇数对都将变成偶数。如果我们将偶数元素加到和中，和将保持为偶数**偶数+偶数=偶数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function returns true if
// it is possible to have
// odd sum
bool isPossible(int arr[],
                int N, int K)
{
    int oddCount = 0, evenCount = 0;

    // counting number of odd
    // and even elements
    for (int i = 0; i < N; i++) {
        if (arr[i] % 2 == 0)
            evenCount++;
        else
            oddCount++;
    }
    if (evenCount == N
        || (oddCount == N && K % 2 == 0)
        || (K == N && oddCount % 2 == 0))
        return false;
    else
        return true;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 8 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);

    if (isPossible(arr, N, K))
        cout << "Possible";
    else
        cout << "Not Possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function returns true if
// it is possible to have
// odd sum
static boolean isPossible(int arr[],
                          int N, int K)
{
    int oddCount = 0, evenCount = 0;

    // Counting number of odd
    // and even elements
    for(int i = 0; i < N; i++)
    {
       if (arr[i] % 2 == 0)
       {
           evenCount++;
       }
       else
       {
           oddCount++;
       }
    }
    if (evenCount == N ||
       (oddCount == N && K % 2 == 0) ||
       (K == N && oddCount % 2 == 0))
    {
        return false;
    }
    else
    {
        return true;
    }
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 8 };
    int K = 5;
    int N = arr.length;

    if (isPossible(arr, N, K))
    {
        System.out.println("Possible");
    }
    else
    {
        System.out.println("Not Possible");
    }
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function returns true if it
# is possible to have odd sum
def isPossible(arr, N, K):

    oddCount = 0
    evenCount = 0

    # Counting number of odd
    # and even elements
    for i in range(N):
        if (arr[i] % 2 == 0):
            evenCount += 1
        else:
            oddCount += 1

    if (evenCount == N or
       (oddCount == N and K % 2 == 0) or
       (K == N and oddCount % 2 == 0)):
        return False
    else:
        return True

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5, 8 ]
    K = 5
    N = len(arr)

    if (isPossible(arr, N, K)):
        print("Possible")
    else:
        print("Not Possible")

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function returns true if
// it is possible to have
// odd sum
static bool isPossible(int []arr,
                       int N, int K)
{
    int oddCount = 0, evenCount = 0;

    // Counting number of odd
    // and even elements
    for(int i = 0; i < N; i++)
    {
       if (arr[i] % 2 == 0)
       {
           evenCount++;
       }
       else
       {
           oddCount++;
       }
    }
    if (evenCount == N ||
       (oddCount == N && K % 2 == 0) ||
       (K == N && oddCount % 2 == 0))
    {
        return false;
    }
    else
    {
        return true;
    }
}

// Driver code
public static void Main (string[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 8 };
    int K = 5;
    int N = arr.Length;

    if (isPossible(arr, N, K))
    {
        Console.WriteLine("Possible");
    }
    else
    {
        Console.WriteLine("Not Possible");
    }
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function returns true if
// it is possible to have
// odd sum
function isPossible(arr, N, K)
{
    let oddCount = 0, evenCount = 0;

    // Counting number of odd
    // and even elements
    for(let i = 0; i < N; i++)
    {
       if (arr[i] % 2 == 0)
       {
           evenCount++;
       }
       else
       {
           oddCount++;
       }
    }
    if (evenCount == N ||
       (oddCount == N && K % 2 == 0) ||
       (K == N && oddCount % 2 == 0))
    {
        return false;
    }
    else
    {
        return true;
    }
}

  // Driver Code

    let arr = [ 1, 2, 3, 4, 5, 8 ];
    let K = 5;
    let N = arr.length;

    if (isPossible(arr, N, K))
    {
        document.write("Possible");
    }
    else
    {
        document.write("Not Possible");
    }

// This code is contributed by target_2.
</script>
```

**Output**

```
Possible
```

**时间复杂度:** O(N)