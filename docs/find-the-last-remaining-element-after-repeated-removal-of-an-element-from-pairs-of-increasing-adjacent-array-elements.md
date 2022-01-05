# 从成对增加的相邻数组元素中重复移除一个元素后，找到最后剩余的元素

> 原文:[https://www . geeksforgeeks . org/find-从递增相邻数组元素对中重复移除元素后最后剩余的元素/](https://www.geeksforgeeks.org/find-the-last-remaining-element-after-repeated-removal-of-an-element-from-pairs-of-increasing-adjacent-array-elements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在重复选择递增的相邻元素对 **(arr[i]，arr[i + 1])** 并移除对中的任何元素后，打印最后剩余的数组元素。如果无法将数组缩减为单个元素，则打印**“不可能”**。

**示例:**

> **输入:** arr[] = {3，1，2，4}
> **输出:** 4
> **解释:**
> 第一步:选择一对(1，2)，从中去掉 2。现在数组变成了[3，1，4]。
> 第二步:选择配对(1，4)并从中移除 1。现在数组变成了[3，4]。
> 第三步:选择配对(3，4)并从中移除 3。现在数组变成了[4]。
> 因此，剩余元素为 4。
> 
> **输入:** arr[] = {2，3，1}
> **输出:**不可能

**方法:**给定的问题可以通过观察这样一个事实来解决:如果第一个数组元素小于最后一个数组元素，那么它们之间的所有元素都可以通过执行给定的操作来移除。因此，只需检查**是否 arr[0]<arr[N–1]**。如果发现为真，打印第一个或最后一个数组元素。否则，打印 **-1** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the last remaining
// array element after after performing
// given operations
void canArrayBeReduced(int arr[], int N)
{
    // If size of the array is 1
    if (N == 1) {
        cout << arr[0];
        return;
    }

    // Check for the condition
    if (arr[0] < arr[N - 1]) {
        cout << arr[N - 1];
    }

    // If condition is not satisfied
    else
        cout << "Not Possible";
}

// Driver Code
int main()
{
    int arr[] = { 6, 5, 2, 4, 1, 3, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    canArrayBeReduced(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to print the last remaining
  // array element after after performing
  // given operations
  static void canArrayBeReduced(int[] arr, int N)
  {

    // If size of the array is 1
    if (N == 1)
    {
      System.out.print(arr[0]);
      return;
    }

    // Check for the condition
    if (arr[0] < arr[N - 1])
    {
      System.out.print(arr[N - 1]);
    }

    // If condition is not satisfied
    else
      System.out.print("Not Possible");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 6, 5, 2, 4, 1, 3, 7 };
    int N = arr.length;

    // Function Call
    canArrayBeReduced(arr, N);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to print the last remaining
# array element after after performing
# given operations
def canArrayBeReduced(arr,  N):

    # If size of the array is 1
    if (N == 1):
        print(arr[0])
        return

    # Check for the condition
    if (arr[0] < arr[N - 1]):
        print(arr[N - 1])

    # If condition is not satisfied
    else:
        print("Not Possible")

# Driver Code
if __name__ == "__main__":

    arr = [6, 5, 2, 4, 1, 3, 7]
    N = len(arr)

    # Function Call
    canArrayBeReduced(arr, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

  // Function to print the last remaining
  // array element after after performing
  // given operations
  static void canArrayBeReduced(int[] arr, int N)
  {

    // If size of the array is 1
    if (N == 1)
    {
      Console.Write(arr[0]);
      return;
    }

    // Check for the condition
    if (arr[0] < arr[N - 1])
    {
      Console.Write(arr[N - 1]);
    }

    // If condition is not satisfied
    else
      Console.Write("Not Possible");
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = { 6, 5, 2, 4, 1, 3, 7 };
    int N = arr.Length;

    // Function Call
    canArrayBeReduced(arr, N);
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to print the last remaining
// array element after after performing
// given operations
function canArrayBeReduced(arr, N)
{

    // If size of the array is 1
    if (N == 1)
    {
        document.write(arr[0]);
        return;
    }

    // Check for the condition
    if (arr[0] < arr[N - 1])
    {
        document.write(arr[N - 1]);
    }

    // If condition is not satisfied
    else
        document.write("Not Possible");
}

// Driver Code

    let arr = [ 6, 5, 2, 4, 1, 3, 7 ];
    let N = arr.length;

    // Function Call
    canArrayBeReduced(arr, N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)