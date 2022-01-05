# 用数组的和替换数组元素，将数组修改为另一个给定的数组

> 原文:[https://www . geeksforgeeks . org/通过用数组和替换将数组修改为另一个给定的数组/](https://www.geeksforgeeks.org/modify-array-to-another-given-array-by-replacing-with-the-sum-of-the-array/)

给定一个最初仅由 **1** s 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **输入[]** 和一个大小为 **N** 的数组**目标[]** ，任务是通过在每一步中用数组元素的和替换**输入【I】**来检查数组**输入[]** 是否可以转换为**目标[**。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**输入[] = { 1，1，1 }，目标[] = { 9，3，5 }
> **输出:**是
> **解释:**
> 将输入[1]替换为(输入[0] +输入[1] +输入[2])将输入[]修改为{ 1，3，1 }
> 将输入[2]替换为(输入[0] +输入[1] +输入[2])将输入[]修改为{ 1，3，5 } 【T10
> 
> **输入:**输入[] = { 1，1，1，1 }，目标[] = { 1，1，1，2 }
> **输出:**否

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是始终将**目标[]** 数组的最大元素减剩余数组元素之和，并检查**目标[]** 的最大元素。如果发现为真，则打印**“是”**。否则，打印**“否”**。以下是观察结果:

> 如果目标[] = { 9，3，5 }和输入[] = { 1，1，1 }
> 将目标[0]递减(目标[1] +目标[2])将目标[]修改为{ 1，3，5 }
> 将目标[2]递减(目标[0] +目标[1])将目标[]修改为{ 1，3，1 }
> 将目标[1]递减(目标[0] +目标[2])将目标[]修改为{ 1，1，1 }
> 自输入[]数组和

*   如果阵中[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **目标[]** 小于 **1** ，则打印**“否”**。
*   如果阵中[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **目标[]** 等于 **1** ，则打印**“是”**。
*   否则，将数组中最大的元素**target【】**减去数组中剩余元素的总和**target【】**而数组中最大的元素大于 **1** 。

下面是上述方法的实现:

## C++

```
// CPP program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the arr[] can be
// converted to target[] by replacing
// any element in arr[] by the sum of arr[]
bool isPossible(int target[], int n)
{

  // Store the maximum element
  int max = 0;

  // Store the index of
  // the maximum element
  int index = 0;

  // Traverse the array target[]
  for (int i = 0; i < n; i++) {

    // If current element is
    // greater than max
    if (max < target[i]) {
      max = target[i];
      index = i;
    }
  }

  // If max element is 1
  if (max == 1)
    return true;

  // Traverse the array, target[]
  for (int i = 0; i < n; i++) {

    // If current index is not equal to
    // maximum element index
    if (i != index) {

      // Update max
      max -= target[i];

      // If max is less than
      // or equal to 0,
      if (max <= 0)
        return false;
    }
  }

  // Update the maximum element
  target[index] = max;

  // Recursively call the function
  return isPossible(target,n);
}

// Driver Code
int main()
{
  int target[] = { 9, 3, 5 };

  // Size of the array
   int n = sizeof(target) / sizeof(target[0]);

  bool res = isPossible(target,n);

  if (res)
  {

    cout << "YES";
  }
  else
  {
    cout << "NO";
  }
  return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to check if the arr[] can be
    // converted to target[] by replacing
    // any element in arr[] by the sum of arr[]
    public static boolean isPossible(int[] target)
    {

        // Store the maximum element
        int max = 0;

        // Store the index of
        // the maximum element
        int index = 0;

        // Traverse the array target[]
        for (int i = 0; i < target.length; i++) {

            // If current element is
            // greater than max
            if (max < target[i]) {
                max = target[i];
                index = i;
            }
        }

        // If max element is 1
        if (max == 1)
            return true;

        // Traverse the array, target[]
        for (int i = 0; i < target.length; i++) {

            // If current index is not equal to
            // maximum element index
            if (i != index) {

                // Update max
                max -= target[i];

                // If max is less than
                // or equal to 0,
                if (max <= 0)
                    return false;
            }
        }

        // Update the maximum element
        target[index] = max;

        // Recursively call the function
        return isPossible(target);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] target = { 9, 3, 5 };

        boolean res = isPossible(target);

        if (res) {

            System.out.println("YES");
        }
        else {
            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python program to implement the above approach

# Function to check if the arr[] can be
# converted to target[] by replacing
# any element in arr[] by the sum of arr[]
def isPossible(target):

  # Store the maximum element
  max = 0

  # Store the index of
  # the maximum element
  index = 0

  # Traverse the array target[]
  for i in range(len(target)):

    # If current element is
    # greater than max
    if (max < target[i]):
      max = target[i]
      index = i

  # If max element is 1
  if (max == 1):
    return True

  # Traverse the array, target[]
  for i in range(len(target)):

    # If current index is not equal to
    # maximum element index
    if (i != index):

      # Update max
      max -= target[i]

      # If max is less than
      # or equal to 0,
      if (max <= 0):
        return False

  # Update the maximum element
  target[index] = max

  # Recursively call the function
  return isPossible(target)

# Driver Code
target = [ 9, 3, 5 ]
res = isPossible(target)
if (res):
  print("YES")
else:
  print("NO")

  # This code is contributed by RohitSingh07052.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to check if the arr[] can be
    // converted to target[] by replacing
    // any element in arr[] by the sum of arr[]
    public static bool isPossible(int[] target)
    {

        // Store the maximum element
        int max = 0;

        // Store the index of
        // the maximum element
        int index = 0;

        // Traverse the array target[]
        for (int i = 0; i < target.Length; i++) {

            // If current element is
            // greater than max
            if (max < target[i])
            {
                max = target[i];
                index = i;
            }
        }

        // If max element is 1
        if (max == 1)
            return true;

        // Traverse the array, target[]
        for (int i = 0; i < target.Length; i++) {

            // If current index is not equal to
            // maximum element index
            if (i != index) {

                // Update max
                max -= target[i];

                // If max is less than
                // or equal to 0,
                if (max <= 0)
                    return false;
            }
        }

        // Update the maximum element
        target[index] = max;

        // Recursively call the function
        return isPossible(target);
    }

// Driver Code
static public void Main()
{
        int[] target = { 9, 3, 5 };

        bool res = isPossible(target);

        if (res)
        {
            Console.WriteLine("YES");
        }
        else
        {
            Console.WriteLine("NO");
        }
    }
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to check if the arr can be
// converted to target by replacing
// any element in arr by the sum of arr
function isPossible(target)
{

    // Store the maximum element
    var max = 0;

    // Store the index of
    // the maximum element
    var index = 0;

    // Traverse the array target
    for (i = 0; i < target.length; i++) {

        // If current element is
        // greater than max
        if (max < target[i]) {
            max = target[i];
            index = i;
        }
    }

    // If max element is 1
    if (max == 1)
        return true;

    // Traverse the array, target
    for (i = 0; i < target.length; i++) {

        // If current index is not equal to
        // maximum element index
        if (i != index) {

            // Update max
            max -= target[i];

            // If max is less than
            // or equal to 0,
            if (max <= 0)
                return false;
        }
    }

    // Update the maximum element
    target[index] = max;

    // Recursively call the function
    return isPossible(target);
}

// Driver Code
var target = [ 9, 3, 5 ];

res = isPossible(target);

if (res) {

    document.write("YES");
}
else {
    document.write("NO");
}
// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*