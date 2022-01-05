# 检查数组的和是否可以通过将数组元素重复减少它们的索引值

而减少到零

> 原文:[https://www . geeksforgeeks . org/check-if-sum-of-array-能够通过按索引值重复减少数组元素来减少到零/](https://www.geeksforgeeks.org/check-if-sum-of-array-can-be-reduced-to-zero-by-repetitively-reducing-array-element-by-their-index-value/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过多次执行以下操作来确定数组元素的[和是否可以减少到 **0** :](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   选择一个元素 **A[i]** 并通过 **i** ( *1 基索引*)减少 **A[i]** ，次数不限，可能为 **0** 。
*   如果总和可以减为 **0** ，打印“**是**”。否则，打印“ **No** ”。

**示例:**

> **输入:** arr[] = {2，3，1}
> **输出:**是
> **解释:**
> 选择 A[2] = 3
> 执行给定运算 3 次，得到如下结果:
> 3->(3-2)-(T14)【3–2–2】->(3–2–2–2)
> 修改后数组之和= 2 + (-3) + 1 = 0。
> 因此，所需答案为 0。
> 
> **输入:** arr[] = {-5，3}
> 输出:否

**方法:**这个问题可以根据以下观察来解决:

*   如果从另一个**正数**中重复减去一个**正数**，那么最终可以得到 **0** 。但是，从一个**负数**中反复减去一个**正数**，0 永远不会得到，因为它一直在负向递减。
*   通过从**A【I】**中减去 **i** 将总和减少到 **0** 的任务。
*   因此，在选择一个元素并将该元素的值减少 **i** 时，**和**将减少 **i** 。

> 设数组的和为 **S** 。
> S = A[1] + A[2] + …。+ A[N]
> 执行给定操作后，数组的和修改为
> S2 =(A[I]–(I))+(A[I+1]–(I+1))…。
> S2 = A[i] + A[i+1]…。–(I+I+1…)
> S2 = S –( I+I+1…..)
> 因此，每次运算后，原始和都减少。

*   因此，任务简化为检查数组的初始[和是否为正或 **0** 。如果发现属实，打印“**是**”。否则，打印“**否**”。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <iostream>
using namespace std;

// Function to check if an array
// sum can be reduced to zero or not
bool isPossible(int arr[], int n)
{
    // Stores the sum of the array
    int S = 0;

    for (int i = 0; i < n; i++) {

        // Update sum of the array
        S = S + arr[i];
    }

    // If the sum is positive
    if (S >= 0) {

        // Array sum can be
        // reduced to 0
        return true;
    }

    // Otherwise
    else {

        // Array sum cannot
        // be reduced to 0
        return false;
    }
}

// Driver Code
int main()
{
    int arr[] = { -5, 3 };

    int n = sizeof(arr) / sizeof(int);

    // Print the answer
    if (isPossible(arr, n)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to check if array sum
    // can be reduced to zero or not
    static boolean isPossible(int[] arr, int n)
    {
        // Stores the sum of the array
        int S = 0;

        for (int i = 0; i < n; i++) {
            S = S + arr[i];
        }

        // If array sum is positive
        if (S >= 0)

            // Array sum can be
            // reduced to 0
            return true;

        // Otherwise
        else

            // Array sum cannot
            // be reduced to 0
            return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { -5, 3 };
        int n = arr.length;

        // Function call
        if (isPossible(arr, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if an array
# sum can be reduced to zero or not
def isPossible(arr, n):

    # Stores sum of the array
    S = sum(arr)

    # If sum is positive
    if(S >= 0):
        return true

    # If sum is negative
    else:
        return false

# Driver Code
if __name__ == '__main__':

    arr = [-5, 3]
    n = len(arr)

    # Function call
    if (isPossible(arr, n)):
        print("Yes")
    else:
        print("No")
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check if array sum
// can be reduced to zero or not
static bool isPossible(int[] arr,
                       int n)
{
  // Stores the sum
  // of the array
  int S = 0;

  for (int i = 0; i < n; i++)
  {
    S = S + arr[i];
  }

  // If array sum is positive
  if (S >= 0)

    // Array sum can be
    // reduced to 0
    return true;

  // Otherwise
  else

    // Array sum cannot
    // be reduced to 0
    return false;
}

// Driver Code
public static void Main()
{
  int[] arr = {-5, 3};
  int n = arr.Length;

  // Function call
  if (isPossible(arr, n))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to check if array sum
    // can be reduced to zero or not
    function isPossible(arr , n)
    {

        // Stores the sum of the array
        var S = 0;

        for (i = 0; i < n; i++) {
            S = S + arr[i];
        }

        // If array sum is positive
        if (S >= 0)

            // Array sum can be
            // reduced to 0
            return true;

        // Otherwise
        else

            // Array sum cannot
            // be reduced to 0
            return false;
    }

    // Driver Code

        var arr = [ -5, 3 ];
        var n = arr.length;

        // Function call
        if (isPossible(arr, n))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)