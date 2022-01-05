# 所有可能子阵列上最大和最小元素的最小乘积

> 原文:[https://www . geeksforgeeks . org/所有可能子阵列的最大和最小元素的最小乘积/](https://www.geeksforgeeks.org/minimum-product-of-maximum-and-minimum-element-over-all-possible-subarrays/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在所有可能的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到最大值和最小值的最小乘积。

**示例:**

> **输入:** arr[] = {6，4，5，6，2，4}
> **输出:** 8
> **解释:**
> 考虑子阵列{2，4}，这个子阵列的最小值和最大值的乘积是 2*4 = 8，这是所有可能的子阵列中的最小值。
> 
> **输入:** arr[] = {3，1，5，2，3，2 }
> T3】输出: 3

**天真法:**解决给定问题最简单的方法是[生成数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能子阵，求所有可能子阵的最大值和最小值的[乘积。检查所有子阵列后，打印获得的所有产品的最小值。](https://www.geeksforgeeks.org/maximum-product-subarray/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法也可以通过使用将相邻元素对视为[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的观察来优化，因为包括任何阵列元素都可能增加我们的最大元素，从而导致最大乘积。

所以思路是[求所有对相邻元素的乘积的最小值](https://www.geeksforgeeks.org/return-a-pair-with-maximum-product-in-array-of-integers/)求合成的最小乘积。

下面是上述方法的实现:

## C++

```
//  C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

//  Function to find the minimum product
//  of the minimum and maximum among all
//  the possible subarrays
int findMinMax(vector<int>& a)
{

    // Stores resultant minimum product
    int min_val = 1000000000;

    // Traverse the given array arr[]
    for (int i = 1; i < a.size(); ++i) {

        // Min of product of all two
        // pair of consecutive elements
        min_val = min(min_val, a[i] * a[i - 1]);
    }

    //  Return the resultant value
    return min_val;
}

//  Driver Code
int main()
{
    vector<int> arr = { 6, 4, 5, 6, 2, 4, 1 };

    cout << findMinMax(arr);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

  //  Function to find the minimum product
  //  of the minimum and maximum among all
  //  the possible subarrays
  static int findMinMax(int[] a)
  {

    // Stores resultant minimum product
    int min_val = 1000000000;

    // Traverse the given array arr[]
    for (int i = 1; i < a.length; ++i) {

      // Min of product of all two
      // pair of consecutive elements
      min_val = Math.min(min_val, a[i] * a[i - 1]);
    }

    //  Return the resultant value
    return min_val;
  }

  //  Driver Code
  public static void main (String[] args)
  {
    int[] arr = { 6, 4, 5, 6, 2, 4, 1 };

    System.out.println(findMinMax(arr));
  }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum product
# of the minimum and maximum among all
# the possible subarrays
def findMinMax(a):

    # Stores resultant minimum product
    min_val = 1000000000

       # Traverse the given array arr[]
    for i in range(1, len(a)):

        # Min of product of all two
        # pair of consecutive elements
        min_val = min(min_val, a[i]*a[i-1])

    # Return the resultant value
    return min_val

# Driver Code
if __name__ == ("__main__"):

    arr = [6, 4, 5, 6, 2, 4, 1]

    print(findMinMax(arr))
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  //  Function to find the minimum product
  //  of the minimum and maximum among all
  //  the possible subarrays
  static int findMinMax(int[] a)
  {

    // Stores resultant minimum product
    int min_val = 1000000000;

    // Traverse the given array arr[]
    for (int i = 1; i < a.Length; ++i) {

      // Min of product of all two
      // pair of consecutive elements
      min_val = Math.Min(min_val, a[i] * a[i - 1]);
    }

    //  Return the resultant value
    return min_val;
  }   

    // Driver Code
    public static void Main (string[] args)
    {
        int[] arr = { 6, 4, 5, 6, 2, 4, 1 };

        Console.WriteLine(findMinMax(arr));
    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
   <script>
        // JavaScript Program to implement
        // the above approach

//  Function to find the minimum product
//  of the minimum and maximum among all
//  the possible subarrays
function findMinMax( a)
{

    // Stores resultant minimum product
    let min_val = 1000000000;

    // Traverse the given array arr[]
    for (let i = 1; i < a.length; ++i) {

        // Min of product of all two
        // pair of consecutive elements
        min_val = Math.min(min_val, a[i] * a[i - 1]);
    }

    //  Return the resultant value
    return min_val;
}

//  Driver Code

    let arr = [6, 4, 5, 6, 2, 4, 1];
    document.write( findMinMax(arr))

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)