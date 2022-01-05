# 检查是否存在大小为 K 的子阵列，其元素组成可被 3 整除的数

> 原文:[https://www . geeksforgeeks . org/check-if-a-size-k-subarray-exists-of-elements-form-number-除尽-3/](https://www.geeksforgeeks.org/check-if-a-subarray-of-size-k-exists-whose-elements-form-a-number-divisible-by-3/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个正整数 **K** ，任务是找到一个大小为 **K** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其元素可用于生成[一个可被 3 整除的数。](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)如果不存在这样的子阵列，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {84，23，45，12 56，82}，K = 3
> **输出:** 12，56，82
> **说明:**
> 子阵{12，56，82}形成的数为 125682，可被 3 整除。
> 
> **输入:** arr[] = {84，23，45，14 56，82}，K = 3
> **输出:** -1

**天真方法:**最简单的方法是[从给定的阵列中生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)大小 **K** ，对于每个子阵列，检查该子阵列形成的数是否能被 **3** 整除。

***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 一个数可以被 3 整除当且仅当该数的位数之和可以被 3 整除。

按照以下步骤解决问题:

1.  将数组前 K 个元素的和存储在一个变量中，比如**和**。
2.  [遍历数组的剩余元素](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
3.  使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)，从**和**中减去子阵列的第一个元素，并将下一个阵列元素添加到子阵列中。
4.  每一步，检查**和**是否能被 3 整除。
5.  如果发现为真，则打印当前 **K** 大小的子阵列。
6.  如果没有找到这样的子阵列，则打印-1。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// K size subarray
void findSubArray(vector<int> arr, int k)
{
    pair<int, int> ans;
    int i, sum = 0;

    // Check if the first K elements
    // forms a number which is
    // divisible by 3
    for (i = 0; i < k; i++) {
        sum += arr[i];
    }

    int found = 0;
    if (sum % 3 == 0) {
        ans = make_pair(0, i - 1);
        found = 1;
    }

    // Using Sliding window technique
    for (int j = i; j < arr.size(); j++) {

        if (found == 1)
            break;

        // Calculate sum of next K
        // size subarray
        sum = sum + arr[j] - arr[j - k];

        // Check if sum is divisible by 3
        if (sum % 3 == 0) {

            // Update the indices of
            // the subarray
            ans = make_pair(j - k + 1, j);
            found = 1;
        }
    }

    // If no such subarray is found
    if (found == 0)
        ans = make_pair(-1, 0);

    if (ans.first == -1) {
        cout << -1;
    }
    else {
        // Print the subarray
        for (i = ans.first; i <= ans.second;
             i++) {
            cout << arr[i] << " ";
        }
    }
}

// Driver's code
int main()
{
    // Given array and K
    vector<int> arr = { 84, 23, 45,
                        12, 56, 82 };
    int K = 3;

    // Function Call
    findSubArray(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.awt.Point;

class GFG{

// Function to find the
// K size subarray
public static void findSubArray(Vector<Integer> arr,
                                int k)
{
    Point ans = new Point(0, 0);
    int i, sum = 0;

    // Check if the first K elements
    // forms a number which is
    // divisible by 3
    for(i = 0; i < k; i++)
    {
        sum += arr.get(i);
    }

    int found = 0;
    if (sum % 3 == 0)
    {
        ans = new Point(0, i - 1);
        found = 1;
    }

    // Using Sliding window technique
    for(int j = i; j < arr.size(); j++)
    {
        if (found == 1)
            break;

        // Calculate sum of next K
        // size subarray
        sum = sum + arr.get(j) - arr.get(j - k);

        // Check if sum is divisible by 3
        if (sum % 3 == 0)
        {

            // Update the indices of
            // the subarray
            ans = new Point(j - k + 1, j);
            found = 1;
        }
    }

    // If no such subarray is found
    if (found == 0)
        ans = new Point(-1, 0);

    if (ans.x == -1)
    {
        System.out.print(-1);
    }
    else
    {

        // Print the subarray
        for(i = ans.x; i <= ans.y; i++)
        {
            System.out.print(arr.get(i) + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Given array and K
    Vector<Integer> arr = new Vector<Integer>();
    arr.add(84);
    arr.add(23);
    arr.add(45);
    arr.add(12);
    arr.add(56);
    arr.add(82);

    int K = 3;

    // Function call
    findSubArray(arr, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the
# K size subarray
def findSubArray(arr, k):

    ans = [(0, 0)]
    sm = 0
    i = 0

    found = 0

    # Check if the first K elements
    # forms a number which is
    # divisible by 3
    while (i < k):
        sm += arr[i]
        i += 1

    if (sm % 3 == 0):
        ans = [(0, i - 1)]
        found = 1

    # Using Sliding window technique
    for j in range(i, len(arr), 1):
        if (found == 1):
            break

        # Calculate sum of next K
        # size subarray
        sm = sm + arr[j] - arr[j - k]

        # Check if sum is divisible by 3
        if (sm % 3 == 0):

            # Update the indices of
            # the subarray
            ans = [(j - k + 1, j)]
            found = 1

    # If no such subarray is found
    if (found == 0):
        ans = [(-1, 0)]

    if (ans[0][0] == -1):
        print(-1)
    else:

        # Print the subarray
        for i in range(ans[0][0], 
                       ans[0][1] + 1, 1):
            print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':

    # Given array and K
    arr = [ 84, 23, 45, 12, 56, 82 ]
    K = 3

    # Function call
    findSubArray(arr, K)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
class GFG{

class Point
{
  public int x, y;
  public Point(int first,
               int second) 
  {
    this.x = first;
    this.y = second;
  }   
}

// Function to find the
// K size subarray
public static void findSubArray(List<int> arr,
                                int k)
{
  Point ans = new Point(0, 0);
  int i, sum = 0;

  // Check if the first K elements
  // forms a number which is
  // divisible by 3
  for(i = 0; i < k; i++)
  {
    sum += arr[i];
  }

  int found = 0;
  if (sum % 3 == 0)
  {
    ans = new Point(0, i - 1);
    found = 1;
  }

  // Using Sliding window technique
  for(int j = i; j < arr.Count; j++)
  {
    if (found == 1)
      break;

    // Calculate sum of next K
    // size subarray
    sum = sum + arr[j] -
          arr[j - k];

    // Check if sum is
    // divisible by 3
    if (sum % 3 == 0)
    {
      // Update the indices of
      // the subarray
      ans = new Point(j - k + 1, j);
      found = 1;
    }
  }

  // If no such subarray is found
  if (found == 0)
    ans = new Point(-1, 0);

  if (ans.x == -1)
  {
    Console.Write(-1);
  }
  else
  {
    // Print the subarray
    for(i = ans.x; i <= ans.y; i++)
    {
      Console.Write(arr[i] + " ");
    }
  }
}

// Driver code
public static void Main(String[] args)
{
  // Given array and K
  List<int> arr = new List<int>();
  arr.Add(84);
  arr.Add(23);
  arr.Add(45);
  arr.Add(12);
  arr.Add(56);
  arr.Add(82);

  int K = 3;

  // Function call
  findSubArray(arr, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the
// K size subarray
function findSubArray(arr, k)
{
    var ans = [];
    var i, sum = 0;

    // Check if the first K elements
    // forms a number which is
    // divisible by 3
    for(i = 0; i < k; i++)
    {
        sum += arr[i];
    }

    var found = 0;
    if (sum % 3 == 0)
    {
        ans = [0, i - 1];
        found = 1;
    }

    // Using Sliding window technique
    for(var j = i; j < arr.length; j++)
    {
        if (found == 1)
            break;

        // Calculate sum of next K
        // size subarray
        sum = sum + arr[j] - arr[j - k];

        // Check if sum is divisible by 3
        if (sum % 3 == 0)
        {

            // Update the indices of
            // the subarray
            ans = [j - k + 1, j];
            found = 1;
        }
    }

    // If no such subarray is found
    if (found == 0)
        ans = [-1, 0];

    if (ans.first == -1)
    {
        cout << -1;
    }
    else
    {

        // Print the subarray
        for(i = ans[0]; i <= ans[1]; i++)
        {
            document.write( arr[i] + " ");
        }
    }
}

// Driver code

// Given array and K
var arr = [ 84, 23, 45, 12, 56, 82 ];
var K = 3;

// Function Call
findSubArray(arr, K);

// This code is contributed by importantly

</script>
```

**Output:** 

```
12 56 82
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)