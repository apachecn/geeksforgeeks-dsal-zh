# 计算对数组进行排序的最少移动次数

> 原文:[https://www . geeksforgeeks . org/count-最小移动次数-前端或末端对数组进行排序/](https://www.geeksforgeeks.org/count-minimum-number-of-moves-to-front-or-end-to-sort-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到使[数组按非递减顺序排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)所需的到数组开头或结尾的最小移动。

**示例:**

> **输入:** arr[] = {4，7，2，3，9}
> **输出:** 2
> **解释:**
> 执行以下操作:
> 第一步:将元素 3 移动到数组的开头。现在，arr[]修改为{3，4，7，2，9}。
> 第二步:将元素 2 移动到数组的开头。现在，arr[]修改为{2，3，4，7，9}。
> 现在，对结果数组进行排序。
> 因此，所需的最小移动量为 2。
> 
> **输入:** arr[] = {1，4，5，7，12}
> **输出:** 0
> **说明:**
> 数组已经排序。因此，不需要移动。

**天真方法:**最简单的方法是检查每个数组元素，需要多少次移动才能[对给定数组进行排序](https://www.geeksforgeeks.org/sort-in-python/) **arr[]** 。对于每个数组元素，如果它不在其排序位置，会出现以下可能性:

*   要么将当前元素移到前面。
*   否则，将当前元素移动到最后。

执行上述操作后，打印排序数组所需的最小操作数。以下是相同的循环关系:

*   如果数组 **arr[]** 等于数组 **brr[]** ，则返回 **0** 。
*   如果**arr【I】**<**brr【j】**，那么操作计数将为:

> 1 +递归 _ 函数(arr，brr，i + 1，j + 1)

*   否则，可以通过取下列状态中的最大值来计算操作计数:
    1.  递归函数(arr，brr，i + 1，j)
    2.  递归函数(arr，brr，I，j + 1)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the minimum
// moves required to convert arr[] to brr[]
int minOperations(int arr1[], int arr2[],
                  int i, int j,
                  int n)
{
  // Base Case
  int f = 0;
  for (int i = 0; i < n; i++)
  {
    if (arr1[i] != arr2[i])
      f = 1;
    break;
  }
  if (f == 0)
    return 0;

  if (i >= n || j >= n)
    return 0;

  // If arr[i] < arr[j]
  if (arr1[i] < arr2[j])

    // Include the current element
    return 1 + minOperations(arr1, arr2,
                             i + 1, j + 1, n);

  // Otherwise, excluding the current element
  return max(minOperations(arr1, arr2,
                           i, j + 1, n),
             minOperations(arr1, arr2,
                           i + 1, j, n));
}

// Function that counts the minimum
// moves required to sort the array
void minOperationsUtil(int arr[], int n)
{
  int brr[n];

  for (int i = 0; i < n; i++)
    brr[i] = arr[i];

  sort(brr, brr + n);
  int f = 0;

  // If both the arrays are equal
  for (int i = 0; i < n; i++)
  {
    if (arr[i] != brr[i])

      // No moves required
      f = 1;
    break;
  }

  // Otherwise
  if (f == 1)

    // Print minimum
    // operations required
    cout << (minOperations(arr, brr,
                           0, 0, n));
  else
    cout << "0";
}

// Driver code
int main()
{
    int arr[] = {4, 7, 2, 3, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    minOperationsUtil(arr, n);
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;
import java.lang.Math;

class GFG{

// Function that counts the minimum
// moves required to convert arr[] to brr[]
static int minOperations(int arr1[], int arr2[],
                         int i, int j)
{

    // Base Case
    if (arr1.equals(arr2))
        return 0;

    if (i >= arr1.length || j >= arr2.length)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1);

    // Otherwise, excluding the current element
    return Math.max(minOperations(arr1, arr2,
                                  i, j + 1),
                    minOperations(arr1, arr2,
                                  i + 1, j));
}

// Function that counts the minimum
// moves required to sort the array
static void minOperationsUtil(int[] arr)
{
    int brr[] = new int[arr.length];

    for(int i = 0; i < arr.length; i++)
        brr[i] = arr[i];

    Arrays.sort(brr);

    // If both the arrays are equal
    if (arr.equals(brr))

        // No moves required
        System.out.print("0");

    // Otherwise
    else

        // Print minimum operations required
        System.out.println(minOperations(arr, brr,
                                         0, 0));
}

// Driver code
public static void main(final String[] args)
{
    int arr[] = { 4, 7, 2, 3, 9 };

    minOperationsUtil(arr);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the minimum
# moves required to convert arr[] to brr[]
def minOperations(arr1, arr2, i, j):

    # Base Case
    if arr1 == arr2:
        return 0

    if i >= len(arr1) or j >= len(arr2):
        return 0

    # If arr[i] < arr[j]
    if arr1[i] < arr2[j]:

        # Include the current element
        return 1 \
        + minOperations(arr1, arr2, i + 1, j + 1)

    # Otherwise, excluding the current element
    return max(minOperations(arr1, arr2, i, j + 1),
               minOperations(arr1, arr2, i + 1, j))

# Function that counts the minimum
# moves required to sort the array
def minOperationsUtil(arr):

    brr = sorted(arr);

    # If both the arrays are equal
    if(arr == brr):

        # No moves required
        print("0")

    # Otherwise
    else:

        # Print minimum operations required
        print(minOperations(arr, brr, 0, 0))

# Driver Code

arr = [4, 7, 2, 3, 9]

minOperationsUtil(arr)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts the minimum
// moves required to convert arr[] to brr[]
static int minOperations(int[] arr1, int[] arr2,
                         int i, int j)
{

    // Base Case
    if (arr1.Equals(arr2))
        return 0;

    if (i >= arr1.Length ||
        j >= arr2.Length)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1);

    // Otherwise, excluding the current element
    return Math.Max(minOperations(arr1, arr2,
                                  i, j + 1),
                    minOperations(arr1, arr2,
                                  i + 1, j));
}

// Function that counts the minimum
// moves required to sort the array
static void minOperationsUtil(int[] arr)
{
    int[] brr = new int[arr.Length];

    for(int i = 0; i < arr.Length; i++)
        brr[i] = arr[i];

    Array.Sort(brr);

    // If both the arrays are equal
    if (arr.Equals(brr))

        // No moves required
        Console.Write("0");

    // Otherwise
    else

        // Print minimum operations required
        Console.WriteLine(minOperations(arr, brr,
                                         0, 0));
}

// Driver code
static void Main()
{
    int[] arr = { 4, 7, 2, 3, 9 };

    minOperationsUtil(arr);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that counts the minimum
// moves required to convert arr[] to brr[]
function minOperations(arr1, arr2,
                       i, j, n)
{

    // Base Case
    let f = 0;
    for(let i = 0; i < n; i++)
    {
        if (arr1[i] != arr2[i])
        f = 1;
        break;
    }
    if (f == 0)
        return 0;

    if (i >= n || j >= n)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1, n);

    // Otherwise, excluding the current element
    return Math.max(minOperations(arr1, arr2,
                                  i, j + 1, n),
                    minOperations(arr1, arr2,
                                  i + 1, j, n));
}

// Function that counts the minimum
// moves required to sort the array
function minOperationsUtil(arr, n)
{
    let brr = new Array(n);

    for(let i = 0; i < n; i++)
        brr[i] = arr[i];

    brr.sort();
    let f = 0;

    // If both the arrays are equal
    for(let i = 0; i < n; i++)
    {
        if (arr[i] != brr[i])

        // No moves required
        f = 1;
        break;
    }

    // Otherwise
    if (f == 1)

        // Print minimum
        // operations required
        document.write(minOperations(arr, brr,
                                     0, 0, n));
    else
        cout << "0";
}

// Driver code
let arr = [ 4, 7, 2, 3, 9 ];
let n = arr.length;

minOperationsUtil(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
2
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法有很多[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。因此，上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决问题:

*   维护一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **表【】【】**来存储计算结果。
*   应用[递归](https://www.geeksforgeeks.org/recursion/)利用较小子问题的结果求解问题。
*   如果 **arr1[i] < arr2[j]** ，那么**返回 1 +个小操作(arr1，arr2，i + 1，j–1，表)**
*   否则，要么将数组的第**I**元素移到最后，要么将数组的第**j**元素移到前面。因此，循环关系为:

> 表[i][j] =最大值(最小值(arr1，arr2，I，j + 1，表)，最小值(arr1，arr2，i + 1，j，表))

*   最后，打印**表【0】【N–1】**中存储的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the minimum
// moves required to convert arr[] to brr[]
int minOperations(int arr1[], int arr2[],
                  int i, int j,
                  int n)
{
  // Base Case
  int f = 0;
  for (int i = 0; i < n; i++)
  {
    if (arr1[i] != arr2[i])
      f = 1;
    break;
  }
  if (f == 0)
    return 0;

  if (i >= n || j >= n)
    return 0;

  // If arr[i] < arr[j]
  if (arr1[i] < arr2[j])

    // Include the current element
    return 1 + minOperations(arr1, arr2,
                             i + 1, j + 1, n);

  // Otherwise, excluding the current element
  return max(minOperations(arr1, arr2,
                           i, j + 1, n),
             minOperations(arr1, arr2,
                           i + 1, j, n));
}

// Function that counts the minimum
// moves required to sort the array
void minOperationsUtil(int arr[], int n)
{
  int brr[n];

  for (int i = 0; i < n; i++)
    brr[i] = arr[i];

  sort(brr, brr + n);
  int f = 0;

  // If both the arrays are equal
  for (int i = 0; i < n; i++)
  {
    if (arr[i] != brr[i])

      // No moves required
      f = 1;
    break;
  }

  // Otherwise
  if (f == 1)

    // Print minimum
    // operations required
    cout << (minOperations(arr, brr,
                           0, 0, n));
  else
    cout << "0";
}

// Driver code
int main()
{
    int arr[] = {4, 7, 2, 3, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    minOperationsUtil(arr, n);
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;
import java.lang.Math;

class GFG{

// Function that counts the minimum
// moves required to convert arr[] to brr[]
static int minOperations(int arr1[], int arr2[],
                         int i, int j)
{

    // Base Case
    if (arr1.equals(arr2))
        return 0;

    if (i >= arr1.length || j >= arr2.length)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1);

    // Otherwise, excluding the current element
    return Math.max(minOperations(arr1, arr2,
                                  i, j + 1),
                    minOperations(arr1, arr2,
                                  i + 1, j));
}

// Function that counts the minimum
// moves required to sort the array
static void minOperationsUtil(int[] arr)
{
    int brr[] = new int[arr.length];

    for(int i = 0; i < arr.length; i++)
        brr[i] = arr[i];

    Arrays.sort(brr);

    // If both the arrays are equal
    if (arr.equals(brr))

        // No moves required
        System.out.print("0");

    // Otherwise
    else

        // Print minimum operations required
        System.out.println(minOperations(arr, brr,
                                         0, 0));
}

// Driver code
public static void main(final String[] args)
{
    int arr[] = { 4, 7, 2, 3, 9 };

    minOperationsUtil(arr);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the minimum
# moves required to covnert arr[] to brr[]
def minOperations(arr1, arr2, i, j):

    # Base Case
    if arr1 == arr2:
        return 0

    if i >= len(arr1) or j >= len(arr2):
        return 0

    # If arr[i] < arr[j]
    if arr1[i] < arr2[j]:

        # Include the current element
        return 1 \
        + minOperations(arr1, arr2, i + 1, j + 1)

    # Otherwise, excluding the current element
    return max(minOperations(arr1, arr2, i, j + 1),
               minOperations(arr1, arr2, i + 1, j))

# Function that counts the minimum
# moves required to sort the array
def minOperationsUtil(arr):

    brr = sorted(arr);

    # If both the arrays are equal
    if(arr == brr):

        # No moves required
        print("0")

    # Otherwise
    else:

        # Print minimum operations required
        print(minOperations(arr, brr, 0, 0))

# Driver Code

arr = [4, 7, 2, 3, 9]

minOperationsUtil(arr)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts the minimum
// moves required to convert arr[] to brr[]
static int minOperations(int[] arr1, int[] arr2,
                         int i, int j)
{

    // Base Case
    if (arr1.Equals(arr2))
        return 0;

    if (i >= arr1.Length ||
        j >= arr2.Length)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1);

    // Otherwise, excluding the current element
    return Math.Max(minOperations(arr1, arr2,
                                  i, j + 1),
                    minOperations(arr1, arr2,
                                  i + 1, j));
}

// Function that counts the minimum
// moves required to sort the array
static void minOperationsUtil(int[] arr)
{
    int[] brr = new int[arr.Length];

    for(int i = 0; i < arr.Length; i++)
        brr[i] = arr[i];

    Array.Sort(brr);

    // If both the arrays are equal
    if (arr.Equals(brr))

        // No moves required
        Console.Write("0");

    // Otherwise
    else

        // Print minimum operations required
        Console.WriteLine(minOperations(arr, brr,
                                         0, 0));
}

// Driver code
static void Main()
{
    int[] arr = { 4, 7, 2, 3, 9 };

    minOperationsUtil(arr);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that counts the minimum
// moves required to convert arr[] to brr[]
function minOperations(arr1, arr2,
                       i, j, n)
{

    // Base Case
    let f = 0;
    for(let i = 0; i < n; i++)
    {
        if (arr1[i] != arr2[i])
        f = 1;
        break;
    }
    if (f == 0)
        return 0;

    if (i >= n || j >= n)
        return 0;

    // If arr[i] < arr[j]
    if (arr1[i] < arr2[j])

        // Include the current element
        return 1 + minOperations(arr1, arr2,
                                 i + 1, j + 1, n);

    // Otherwise, excluding the current element
    return Math.max(minOperations(arr1, arr2,
                                  i, j + 1, n),
                    minOperations(arr1, arr2,
                                  i + 1, j, n));
}

// Function that counts the minimum
// moves required to sort the array
function minOperationsUtil(arr, n)
{
    let brr = new Array(n);

    for(let i = 0; i < n; i++)
        brr[i] = arr[i];

    brr.sort();
    let f = 0;

    // If both the arrays are equal
    for(let i = 0; i < n; i++)
    {
        if (arr[i] != brr[i])

        // No moves required
        f = 1;
        break;
    }

    // Otherwise
    if (f == 1)

        // Print minimum
        // operations required
        document.write(minOperations(arr, brr,
                                     0, 0, n));
    else
        cout << "0";
}

// Driver code
let arr = [ 4, 7, 2, 3, 9 ];
let n = arr.length;

minOperationsUtil(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N <sup>2</sup> )*

***辅助空间:** O(N <sup>2</sup> )*

我们使用两个变量，即 I 和 j 来确定动态规划阶段的唯一状态，I 和 j 中的每一个都可以获得从 0 到 N-1 的 N 个值。因此，递归将有 N*N 个转换，每个转换的成本为 0(1)。因此时间复杂度为 0(N * N)。

**更有效的方法:**排序给定的数组，保留元素的索引放在一边，现在找到索引值增加的最长条纹。这个最长的条纹反映了这些元素已经被排序，并对其余的元素执行上述操作。让我们以上面的数组为例，arr = [8，2，1，5，4]排序后，它们的索引值将是–[ 2，1，4，3，0]，这里最长的条纹是 2(1，4)，这意味着除了这 2 个数字之外，我们必须遵循上面的操作并对数组进行排序，因此，5(arr . length)–2 = 3 将是答案。

上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java algorithm for above approach

import java.util.*;

class GFG {

    // Pair class which will store element of array with its
    // index
    public static class Pair {
        int val;
        int idx;
        Pair(int val, int idx)
        {
            this.val = val;
            this.idx = idx;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        int[] arr = { 4, 7, 2, 3, 9 };
        System.out.println(minOperations(arr, n));
    }

    // Function to find minimum number of operation required
    // so that array becomes meaningful
    public static int minOperations(int[] arr, int n)
    {
        // Initializing array of Pair type which can be used
        // to sort arr with respect to its values
        Pair[] num = new Pair[n];
        for (int i = 0; i < n; i++) {
            num[i] = new Pair(arr[i], i);
        }

        // Sorting array num on the basis of value
        Arrays.sort(num, (Pair a, Pair b) -> a.val - b.val);

        // Initializing variables used to find maximum
        // length of increasing streak in index
        int res = 1;
        int streak = 1;
        int prev = num[0].idx;
        for (int i = 1; i < n; i++) {
            if (prev < num[i].idx) {
                res++;

                // Updating streak
                streak = Math.max(res, streak);
            }
            else
                res = 1;
            prev = num[i].idx;
        }

        // Returning number of elements left except streak
        return n - streak;
    }
}
```

## C++

```
// C++ algorithm of above approach

#include <bits/stdc++.h>
#include <vector>
using namespace std;

// Function to find minimum number of operation required
// so that array becomes meaningful
int minOperations(int arr[], int n)
{
    // Initializing vector of pair type which contains value
    // and index of arr
    vector<pair<int, int>> vect;
    for (int i = 0; i < n; i++) {
        vect.push_back(make_pair(arr[i], i));
    }

    // Sorting array num on the basis of value
    sort(vect.begin(), vect.end());

    // Initializing variables used to find maximum
    // length of increasing streak in index
    int res = 1;
    int streak = 1;
    int prev = vect[0].second;
    for (int i = 1; i < n; i++) {
        if (prev < vect[i].second) {
            res++;

            // Updating streak
            streak = max(streak, res);
        }
        else
            res = 1;
        prev = vect[i].second;
    }

    // Returning number of elements left except streak
    return n - streak;
}

// Driver Code
int main()
{
    int arr[] = { 4, 7, 2, 3, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int count = minOperations(arr, n);
    cout << count;
}
```

**Output**

```
2
```

**时间复杂度:** O(nlogn)

**辅助空间:** O(n)