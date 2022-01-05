# 仅由复数组成的子阵数量

> 原文:[https://www . geesforgeks . org/subarray-number-仅由-pronic-numbers 组成/](https://www.geeksforgeeks.org/number-of-subarrays-consisting-only-of-pronic-numbers/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算仅由[个复数](https://www.geeksforgeeks.org/check-given-number-pronic/)组成的[个子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。

**示例:**

> **输入:** arr[] = {5，6，12，3，4}
> **输出:** 3
> **解释:**仅由音位数字组成的子阵为:
> 
> 1.  {6}
> 2.  {12}
> 3.  {6, 12}
> 
> 因此，这种子阵列的总数是 3。
> 
> **输入:** arr[] = {0，4，20，30，5}
> **输出:** 4

**天真方法:**解决问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子数组，并且只计算那些由[发音数字](https://www.geeksforgeeks.org/check-given-number-pronic/)组成的子数组。检查所有子阵列后，打印获得的计数。

***时间复杂度:** O(√M * N <sup>3</sup> ，其中 **M** 是数组中出现的* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过保持[音位数](https://www.geeksforgeeks.org/check-given-number-pronic/)的连续序列的轨迹，然后计数形成的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量来优化。
按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**，存储[子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的总计数；初始化一个变量 **C** ，存储连续数组元素的计数，这些元素是[字根](https://www.geeksforgeeks.org/check-given-number-pronic/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   如果当前元素**arr【I】**是一个**音位数字**，那么将 **C** 增加 **1** 。
    *   否则，将**计数**增加**C *(C–1)/2**来计数具有 **C** 元素的子阵数量，并将 **C** 更新为 **0** 。
*   增加**的值，将**计为**C *(C–1)/2**。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the approach
#include <iostream>
#include <cmath>
using namespace std;

// Function to check if a number
// is pronic number or not
bool isPronic(int n)
{

    // Iterate over the range [1, sqrt(N)]
    int range = sqrt(n);

    for(int i = 0; i < range + 1; i++)
    {

        // Return true if N is pronic
        if (i * (i + 1) == n)
            return true;    
    }

    // Otherwise, return false
    return false;
}

// Function to count the number of
// subarrays consisting of pronic numbers
int countSub(int *arr, int n)
{

    // Stores the count of subarrays
    int ans = 0;

    // Stores the number of consecutive
    // array elements which are pronic
    int ispro = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If i is pronic
        if (isPronic(arr[i]))
            ispro += 1;
        else
            ispro = 0;

        ans += ispro;
    }

    // Return the total count
    return ans;
}

// Driver code
int main()
{
    int arr[5] = {5, 6, 12, 3, 4};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countSub(arr, n);

    return 0;
}

// This code is contributed by rohitsingh07052
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the approach
import java.lang.*;
class GFG
{

  // Function to check if a number
  // is pronic number or not
  static boolean isPronic(int n)
  {

    // Iterate over the range [1, sqrt(N)]
    int range = (int)Math.sqrt(n);

    for(int i = 0; i < range + 1; i++)
    {

      // Return true if N is pronic
      if (i * (i + 1) == n)
        return true;    
    }

    // Otherwise, return false
    return false;
  }

  // Function to count the number of
  // subarrays consisting of pronic numbers
  static int countSub(int[] arr, int n)
  {

    // Stores the count of subarrays
    int ans = 0;

    // Stores the number of consecutive
    // array elements which are pronic
    int ispro = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // If i is pronic
      if (isPronic(arr[i]))
        ispro += 1;
      else
        ispro = 0;

      ans += ispro;
    }

    // Return the total count
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = {5, 6, 12, 3, 4};
    int n = arr.length;
    System.out.print(countSub(arr, n));
  }
}

// This code is contributed by shivani
```

## 蟒蛇 3

```
# Python3 program for the approach

# Function to check if a number
# is pronic number or not
def isPronic(n):

    # Iterate over the range [1, sqrt(N)]
    for i in range(int(n ** (1 / 2)) + 1):

        # Return true if N is pronic
        if i * (i + 1) == n:
            return True

    # Otherwise, return false
    return False

# Function to count the number of
# subarrays consisting of pronic numbers
def countSub(arr):

    # Stores the count of subarrays
    ans = 0

    # Stores the number of consecutive
    # array elements which are pronic
    ispro = 0

    # Traverse the array
    for i in arr:

        # If i is pronic
        if isPronic(i):
            ispro += 1
        else:
            ispro = 0

        ans += ispro

    # Return the total count
    return ans

# Driver Code

arr = [5, 6, 12, 3, 4]
print(countSub(arr))
```

## C#

```
// C# program for the approach
using System;
class GFG
{

  // Function to check if a number
  // is pronic number or not
  static bool isPronic(int n)
  {

    // Iterate over the range [1, sqrt(N)]
    int range = (int)Math.Sqrt(n);        
    for(int i = 0; i < range + 1; i++)
    {

      // Return true if N is pronic
      if (i * (i + 1) == n)
        return true;    
    }

    // Otherwise, return false
    return false;
  }

  // Function to count the number of
  // subarrays consisting of pronic numbers
  static int countSub(int[] arr, int n)
  {

    // Stores the count of subarrays
    int ans = 0;

    // Stores the number of consecutive
    // array elements which are pronic
    int ispro = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // If i is pronic
      if (isPronic(arr[i]))
        ispro += 1;
      else
        ispro = 0;
      ans += ispro;
    }

    // Return the total count
    return ans;
  }

  // Driver code
  static void Main() {
    int[] arr = {5, 6, 12, 3, 4};
    int n = arr.Length;

    Console.WriteLine(countSub(arr, n));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the approach

// Function to check if a number
// is pronic number or not
function isPronic(n)
{

    // Iterate over the range [1, sqrt(N)]
    let range = Math.sqrt(n);

    for(let i = 0; i < range + 1; i++)
    {

        // Return true if N is pronic
        if (i * (i + 1) == n)
            return true;    
    }

    // Otherwise, return false
    return false;
}

// Function to count the number of
// subarrays consisting of pronic numbers
function countSub(arr, n)
{

    // Stores the count of subarrays
    let ans = 0;

    // Stores the number of consecutive
    // array elements which are pronic
    let ispro = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // If i is pronic
        if (isPronic(arr[i]))
            ispro += 1;
        else
            ispro = 0;

        ans += ispro;
    }

    // Return the total count
    return ans;
}

// Driver code
let arr = [5, 6, 12, 3, 4];
let n = arr.length;

document.write(countSub(arr, n));

// This code is contributed by souravmahato348.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(N*sqrt(M))，其中 **M** 是数组* 中出现的 [*最大元素。
***辅助空间:** O(1)**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)