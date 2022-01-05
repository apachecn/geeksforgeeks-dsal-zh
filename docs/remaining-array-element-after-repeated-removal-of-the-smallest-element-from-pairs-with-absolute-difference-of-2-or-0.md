# 从绝对差为 2 或 0 的对中重复移除最小元素后剩余的数组元素

> 原文:[https://www . geeksforgeeks . org/从绝对差值为 2 或 0 的对中重复移除最小元素后的剩余数组元素/](https://www.geeksforgeeks.org/remaining-array-element-after-repeated-removal-of-the-smallest-element-from-pairs-with-absolute-difference-of-2-or-0/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是检查是否有可能通过重复移除绝对差值为 2 或 0 的一对中的最小元素来将数组的大小减小到 **1** 。如果无法减少，则打印**-1”**。否则，打印数组中最后剩余的元素。

**示例:**

> **输入:** arr[] = {2，4，6，8，0，8}
> **输出:** 8
> **解释:**
> arr[] = {2，4，6，8，0，8}，从对(2，0)中移除 0。
> arr[] = {2，4，6，8，8}。从对(2，4)上拆下 2 个。
> arr[] = {4，6，8，8}，从对(4，6)中删除 4。
> arr[] = {6，8，8}。从对(6，8)上拆下 6 个。
> arr[] = {8，8}。拆下 8。
> arr[] = {8}
> 
> **输入:** arr[] = {1，7，3，3}
> **输出:** -1
> **解释:**
> arr[] = {1，7，3，3}。从配对(1，3)中移除 1 个。
> arr[] = {7，3，3}。从一对(3，3)中移除 3 个。
> arr[] = {7，3}。不可能再移除了。

**方法:**按照以下步骤解决问题:

*   [给定数组按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [从最小元素开始遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查是否存在除 **2** 或 **0** 以外的任意一对具有绝对差异的相邻元素。
*   如果发现是真的，那么打印**-1”**。否则，打印阵列中存在的[最大元素，因为这将是执行给定操作后唯一剩余的阵列元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the last remaining
// array element after repeatedly removing
// the smallest from pairs having absolute
// difference 2 or 0
void findLastElement(int arr[], int N)
{
    // Sort the given array in
    // ascending order
    sort(arr, arr + N);
    int i = 0;

    // Traverse the array
    for (i = 1; i < N; i++) {

        // If difference between
        // adjacent elements is
        // not equal to 0 or 2
        if (arr[i] - arr[i - 1] != 0
            && arr[i] - arr[i - 1] != 2) {

            cout << "-1" << endl;
            return;
        }
    }

    // If operations can be performed
    cout << arr[N - 1] << endl;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 6, 8, 0, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findLastElement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to find the last remaining
  // array element after repeatedly removing
  // the smallest from pairs having absolute
  // difference 2 or 0
  static void findLastElement(int arr[], int N)
  {
    // Sort the given array in
    // ascending order
    Arrays.sort(arr);
    int i = 0;

    // Traverse the array
    for (i = 1; i < N; i++) {

      // If difference between
      // adjacent elements is
      // not equal to 0 or 2
      if (arr[i] - arr[i - 1] != 0
          && arr[i] - arr[i - 1] != 2)
      {

        System.out.println("-1");
        return;
      }
    }

    // If operations can be performed
    System.out.println( arr[N - 1]);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 2, 4, 6, 8, 0, 8 };
    int N = arr.length;
    findLastElement(arr, N);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the last remaining
# array element after repeatedly removing
# the smallest from pairs having absolute
# difference 2 or 0
def findLastElement(arr, N):

    # Sort the given array in
    # ascending order
    arr.sort();
    i = 0;

    # Traverse the array
    for i in range(1, N):

        # If difference between
        # adjacent elements is
        # not equal to 0 or 2
        if (arr[i] - arr[i - 1] != 0\
                and arr[i] - arr[i - 1] != 2):
            print("-1");
            return;

    # If operations can be performed
    print(arr[N - 1]);

# Driver Code
if __name__ == '__main__':
    arr = [2, 4, 6, 8, 0, 8];
    N = len(arr);
    findLastElement(arr, N);

# This code is contributed by 29AjayKumar.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the last remaining
  // array element after repeatedly removing
  // the smallest from pairs having absolute
  // difference 2 or 0
  static void findLastElement(int []arr, int N)
  {

    // Sort the given array in
    // ascending order
    Array.Sort(arr);
    int i = 0;

    // Traverse the array
    for (i = 1; i < N; i++)
    {

      // If difference between
      // adjacent elements is
      // not equal to 0 or 2
      if (arr[i] - arr[i - 1] != 0
          && arr[i] - arr[i - 1] != 2)
      {
        Console.WriteLine("-1");
        return;
      }
    }

    // If operations can be performed
    Console.WriteLine(arr[N - 1]);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 2, 4, 6, 8, 0, 8 };
    int N = arr.Length;
    findLastElement(arr, N);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the last remaining
// array element after repeatedly removing
// the smallest from pairs having absolute
// difference 2 or 0
function findLastElement(arr, N)
{

    // Sort the given array in
    // ascending order
    arr.sort();
    let i = 0;

    // Traverse the array
    for (i = 1; i < N; i++)
    {

        // If difference between
        // adjacent elements is
        // not equal to 0 or 2
        if (arr[i] - arr[i - 1] != 0
            && arr[i] - arr[i - 1] != 2)
        {

            document.write("-1" + "<br>");
            return;
        }
    }

    // If operations can be performed
    document.write(arr[N - 1] + "<br>");
}

// Driver Code
    let arr = [ 2, 4, 6, 8, 0, 8 ];
    let N = arr.length;
    findLastElement(arr, N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*