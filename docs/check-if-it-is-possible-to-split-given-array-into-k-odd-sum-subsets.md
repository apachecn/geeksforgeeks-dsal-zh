# 检查给定数组是否可以拆分成 K 个奇数和子集

> 原文:[https://www . geesforgeks . org/check-如果有可能将给定数组拆分为 k 个奇数和子集/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-split-given-array-into-k-odd-sum-subsets/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是检查是否有可能将给定的数组拆分为 **K** 个非空且不相交的子集，使得每个子集的元素之和为奇数。
**举例:**

> **输入:** K = 4，arr[] = {1，3，4，7，5，3，1}
> **输出:**是
> **说明:**
> 【1】、【3，4，7，5】、【3】和【1】是可能的子集。
> **输入:** K = 3，arr[] = {2，3，4，7，2}
> **输出:**否
> **说明:**
> 给定数组不能拆分为 3 个奇数和的子集。

**进场:**
要解决上述问题我们需要观察以下几点:

*   偶数不改变子集和的奇偶性，所以我们可以忽略。
*   如果数组中的**奇数个数小于 K** ，那么由于奇数个数不够，我们不能用奇数和把它拆分成 **K** 个子集。
*   设奇数为 **cnt** 。那么，只有当 **cnt % 2 = K % 2** 时，答案才总是可能的。这是因为我们将在第一个 **K-1 子集**中分配**一个奇数**，在最后一个子集**中分配**CNT–K-1**个奇数。现在由于 **cnt** 和 **K** 具有相同的奇偶性，所以**CNT–K–1**将是奇数，并且总和也是奇数。**

因此，为了解决这个问题，计算数组中出现的奇数个数。让这成为 *cnt* 。如果 **cnt** 大于 **K** 和 **cnt % 2 = K % 2** ，则答案为“是”。否则，答案是不可能的，我们会打印“否”。
以下是上述方法的实施:

## C++

```
// C++ implementation to check if it is
// possible to split array into K
// subsets with odd sum
#include <bits/stdc++.h>
using namespace std;

// Function to check if array
// can be split in required K
// subsets
bool checkArray(int n, int k, int arr[])
{
    // Store count of
    // odd numbers
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        // Check if element
        // is odd
        if (arr[i] & 1)
            cnt += 1;
    }

    // Check if split is possible
    if (cnt >= k && cnt % 2 == k % 2)
        return true;
    else
        return false;
}

// Driver Program
int main()
{
    int arr[] = { 1, 3, 4, 7, 5, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 4;

    if (checkArray(n, k, arr))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if it
// is possible to split array into K
// subsets with odd sum

class GFG{

// Function to check if array
// can be split in required K
// subsets
static boolean checkArray(int n, int k,
                          int arr[])
{

    // Store count of odd numbers
    int cnt = 0;
    for(int i = 0; i < n; i++)
    {

       // Check if element is odd
       if ((arr[i] & 1) != 0)
           cnt += 1;
    }

    // Check if split is possible
    if (cnt >= k && cnt % 2 == k % 2)
        return true;
    else
        return false;
}

// Driver code
public static void main (String []args)
{
    int arr[] = { 1, 3, 4, 7, 5, 3, 1 };
    int n = arr.length;
    int k = 4;

    if (checkArray(n, k, arr))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to check if
# it is possible to split array into
# K subsets with odd sum

# Function to check if array
# can be split in required K
# subsets
def checkArray(n, k, arr):

    # Store count of
    # odd numbers
    cnt = 0
    for i in range(n):

        # Check if element
        # is odd
        if (arr[i] & 1):
            cnt += 1

    # Check if split is possible
    if (cnt >= k and cnt % 2 == k % 2):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 3, 4, 7, 5, 3, 1 ]
    n = len(arr)
    k = 4

    if (checkArray(n, k, arr)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to check if it
// is possible to split array into K
// subsets with odd sum
using System;
class GFG{

// Function to check if array
// can be split in required K
// subsets
static bool checkArray(int n, int k,
                       int []arr)
{

    // Store count of odd numbers
    int cnt = 0;
    for(int i = 0; i < n; i++)
    {

        // Check if element is odd
        if ((arr[i] & 1) != 0)
            cnt += 1;
    }

    // Check if split is possible
    if (cnt >= k && cnt % 2 == k % 2)
        return true;
    else
        return false;
}

// Driver code
public static void Main (string []args)
{
    int []arr = { 1, 3, 4, 7, 5, 3, 1 };
    int n = arr.Length;
    int k = 4;

    if (checkArray(n, k, arr))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation to check if it
// is possible to split array into K
// subsets with odd sum
    // Function to check if array
    // can be split in required K
    // subsets
    function checkArray(n , k , arr) {

        // Store count of odd numbers
        var cnt = 0;
        for (i = 0; i < n; i++) {

            // Check if element is odd
            if ((arr[i] & 1) != 0)
                cnt += 1;
        }

        // Check if split is possible
        if (cnt >= k && cnt % 2 == k % 2)
            return true;
        else
            return false;
    }

    // Driver code

        var arr = [ 1, 3, 4, 7, 5, 3, 1 ];
        var n = arr.length;
        var k = 4;

        if (checkArray(n, k, arr))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*T4】