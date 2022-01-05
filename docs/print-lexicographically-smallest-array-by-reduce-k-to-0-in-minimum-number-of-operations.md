# 通过在最少操作次数下将 K 减少到 0 来打印字典最小数组

> 原文:[https://www . geeksforgeeks . org/print-按字典顺序-最小数组-最小运算数中的 k 减 0/](https://www.geeksforgeeks.org/print-lexicographically-smallest-array-by-reduce-k-to-0-in-minimum-number-of-operations/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K，**的任务是通过执行以下操作将 **K** 的值减少到 **0** 。一个操作定义为选择 **2** 索引 **i，j** 并从 **arr[i](即 arr[I]= arr[I]–X)**中减去 **arr[i]** 和 **K(即 X = min(arr[i]，K)** 的最小值，并将最小值加到**arr[j](arr[j]= arr[j]+X)【T21 请注意[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的元素不能为负。**

**示例:**

> ***输入:** N = 4，K = 2，arr[] = {4，3，2，1}*
> ***输出:** 2 2 3 3*
> ***解释:***
> *操作 1:选择指数 **0** 和 **3、**然后减去 **arr[0](=4)** 和 **K 的最小值**现在，修改后的数组是{2，3，2，3}*
> *现在，对修改后的数组进行排序并打印出来。*
> 
> ***输入:** N = 3，K = 15，arr[] = {1，2，3}*
> ***输出:** 0 0 6*
> ***解释:***
> *操作 1:选择指数 **0** 和 **2、**然后减去 **arr[0](=1)** 和**K(= 11)**现在修改后的数组是{0，2，4}。*
> *操作 2:选择指数 **1** 和 **2、**然后从 **arr[1]** 中减去 **arr[1](=2)** 和 **K(=15)** 的最小值，即 **arr[1](=2)** 中的 **arr[2](=4)。**现在修改后的数组是{0，0，6}。*
> *现在，对修改后的数组进行排序并打印。*

**方法:**这个问题可以通过[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**来解决。按照以下步骤解决问题:

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，并执行以下步骤:
    *   如果 **arr[i]** 小于 **K，**则采取以下步骤。
    *   从变量 **K 中减去**arr【I】**，将**arr【I】**的值加到**arr【n-1】**上，将**arr【I】**的值设置为 **0。****
    *   否则，从 **arr[i]的值中减去 **K** ，**将 **K** 的值加到 **arr[n-1]** 并将 **K** 的值设置为 **0** ，[断开](https://www.geeksforgeeks.org/break-statement-cc/)回路。
*   [整理](https://www.geeksforgeeks.org/sort-c-stl/)[阵](https://www.geeksforgeeks.org/array-data-structure/)T4【arr】。
*   执行上述步骤后，打印[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find the resultant array.
void solve(int n, int k, int arr[])
{

    for (int i = 0; i < n - 1; i++) {

        // checking if aith value less than K

        if (arr[i] < k)

        {
            // substracting ai value from K
            k = k - arr[i];

            // Adding ai value to an-1
            arr[n - 1]
                = arr[n - 1]
                  + arr[i];

            arr[i] = 0;
        }

        // if arr[i] value is greater than  K
        else {

            arr[i] = arr[i] - k;
            arr[n - 1] = arr[n - 1] + k;
            k = 0;
        }
    }

    // sorting the given array
    // to know about this function
    // check gfg stl sorting article
    sort(arr, arr + n);

    // Displaying the final array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{

    int N = 6;
    int K = 2;
    int arr[N] = { 3, 1, 4, 6, 2, 5 };

    solve(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;
class GFG
{

  // Function to find the resultant array.
static void solve(int n, int k, int arr[])
{

    for (int i = 0; i < n - 1; i++) {

        // checking if aith value less than K
        if (arr[i] < k)

        {

            // substracting ai value from K
            k = k - arr[i];

            // Adding ai value to an-1
            arr[n - 1]
                = arr[n - 1]
                  + arr[i];

            arr[i] = 0;
        }

        // if arr[i] value is greater than  K
        else {

            arr[i] = arr[i] - k;
            arr[n - 1] = arr[n - 1] + k;
            k = 0;
        }
    }

    // sorting the given array
    // to know about this function
    // check gfg stl sorting article
    Arrays.sort(arr);

    // Displaying the final array
    for (int i = 0; i < n; i++)
        System.out.print( arr[i] + " ");
}

// Driver code
    public static void main (String[] args) {
         int N = 6;
    int K = 2;
    int arr[] = { 3, 1, 4, 6, 2, 5 };

    solve(N, K, arr);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach.
# Function to find the resultant array.
def solve( n,  k,  arr):

    for i in range(n-1):
        # checking if aith value less than K

        if (arr[i] < k):

            # substracting ai value from K
            k = k - arr[i]

            # Adding ai value to an-1
            arr[n - 1] = arr[n - 1] + arr[i]

            arr[i] = 0

        # if arr[i] value is greater than  K
        else:
            arr[i] = arr[i] - k
            arr[n - 1] = arr[n - 1] + k
            k = 0

    # sorting the given array
    # to know about this function
    # check gfg stl sorting article
    arr.sort()

    # Displaying the final array
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
N = 6
K = 2
arr = [ 3, 1, 4, 6, 2, 5 ]

solve(N, K, arr)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to find the resultant array.
  static void solve(int n, int k, int []arr)
  {

    for (int i = 0; i < n - 1; i++) {

      // checking if aith value less than K
      if (arr[i] < k)

      {

        // substracting ai value from K
        k = k - arr[i];

        // Adding ai value to an-1
        arr[n - 1]
          = arr[n - 1]
          + arr[i];

        arr[i] = 0;
      }

      // if arr[i] value is greater than  K
      else {

        arr[i] = arr[i] - k;
        arr[n - 1] = arr[n - 1] + k;
        k = 0;
      }
    }

    // sorting the given array
    // to know about this function
    // check gfg stl sorting article
    Array.Sort(arr);

    // Displaying the readonly array
    for (int i = 0; i < n; i++)
      Console.Write( arr[i] + " ");
  }

  // Driver code
  public static void Main(String[] args)
  {
    int N = 6;
    int K = 2;
    int []arr = { 3, 1, 4, 6, 2, 5 };

    solve(N, K, arr);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program for the above approach

  // Function to find the resultant array.
function solve(n , k , arr)
{

    for (var i = 0; i < n - 1; i++) {

        // checking if aith value less than K
        if (arr[i] < k)

        {

            // substracting ai value from K
            k = k - arr[i];

            // Adding ai value to an-1
            arr[n - 1]
                = arr[n - 1]
                  + arr[i];

            arr[i] = 0;
        }

        // if arr[i] value is greater than  K
        else {

            arr[i] = arr[i] - k;
            arr[n - 1] = arr[n - 1] + k;
            k = 0;
        }
    }

    // sorting the given array
    // to know about this function
    // check gfg stl sorting article
    arr.sort();

    // Displaying the final array
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Driver code
    var N = 6;
    var K = 2;
    var arr = [ 3, 1, 4, 6, 2, 5 ];

    solve(N, K, arr);

// This code contributed by shikhasingrajput
</script>
```

**Output**

```
1 1 2 4 6 7 
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*