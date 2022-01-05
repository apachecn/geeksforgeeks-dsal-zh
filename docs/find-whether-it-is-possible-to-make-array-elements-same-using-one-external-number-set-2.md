# 查找是否可以用一个外部数字使数组元素相同|设置 2

> 原文:[https://www . geesforgeks . org/find-是否有可能制作数组元素-相同使用一个外部数字-set-2/](https://www.geeksforgeeks.org/find-whether-it-is-possible-to-make-array-elements-same-using-one-external-number-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，以下是可以使用任何外部数字 **X** 执行的三个操作:

1.  将 **X** 添加到数组元素中一次。
2.  从一个数组元素中减去 **X** 一次。
3.  不对数组元素执行任何操作。

任务是检查是否存在数字 **X** ，这样如果用数字 **X** 执行上述操作，数组元素就变得相等。如果有，打印**“是”**和 **X** 的值。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {2，3，3，4，2}
> **输出:**是 1
> **解释:**
> 将 X 的值视为 1，将数组元素 **arr[0](= 2)** 和 **arr[4](= 2)** 递增 1，将 **arr[3](= 4)** 递减 1 将数组修改为{3，3，3，3
> 因此，打印“是”，数值 X 为 1。
> 
> **输入:** arr[] = {4，3，2，1}
> **输出:**否

**方法:**给定的问题可以基于以下观察来解决:

*   如果所有数字相等，答案是“**是**”。
*   如果数组中有两个不同的数字，答案是“**是**，因为每个不同的数字都可以在运算后转换成另一个整数。
*   如果数组中至少有四个不同的数字，由于加法的性质，答案是“**否**”。
*   在其他情况下，如果有三个不同的数字 **A < B < C** ，则可以通过将所有的 **A** 增加**B–A**并将所有的 **C** 减少**C–A**来使所有的数组元素相等。因此，只有当 **2 * B** 等于 **(C + A) / 2** 时，答案才会是“**是**”。

按照以下步骤解决问题:

*   初始化 **3** 变量，比如说， **X，Y** ，和 **Z** 为 **-1** ，以存储数组 **arr[]的所有 **3** 不同整数。**
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   如果 **X，Y** 和 **Z** 中的任何一个是 **-1** ，那么将**arr【I】**分配给该变量。
    *   否则，如果 **X、Y** 、 **Z** 都不等于**arr【I】**，则打印“ **NO** ”并返回。
*   如果 **X、Y** 、 **Z** 中的任意一个等于 **-1** ，则打印“ **YES** ”。
*   将最小的元素存储在 **X** 中，将次大的元素存储在 **Y** 中，将最大的元素存储在**z**中
*   现在，如果 **Z-Y** 等于**(Y–X)**，则打印“**是**”。否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find whether it is possible
// to make array elements equal using
// one external number
void isPossMakeThemEqual(int arr[],
                         int N)
{

    int X = -1;
    int Y = -1;
    int Z = -1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If X is equal to -1
        if (X == -1) {

            // Update the value of X
            X = arr[i];
        }

        // Otherwise, if X is not
        // equal to arr[i]
        else if (X != arr[i]) {

            // If Y is equal to -1
            if (Y == -1) {
                // Update Y
                Y = arr[i];
            }

            // Otherwise, if Y is not
            // equal to arr[i]
            else if (Y != arr[i]) {

                // If  Z is equal to -1
                if (Z == -1) {

                    // Update the value
                    // of Z
                    Z = arr[i];
                }

                // Otherwise If Z is not
                // equal to arr[i], then
                // there are at least four
                // distinct numbers in array
                else if (Z != arr[i]) {
                    cout << "NO";
                    return;
                }
            }
        }
    }

    // If Y is equal to -1, then all
    // the array elements are equal
    if (Y == -1) {
        cout << "YES 0";
        return;
    }

    // If Z is equal to -1, then there
    // are only two distinct elements
    if (Z == -1) {
        cout << "YES " << abs(X - Y);
        return;
    }

    int a = X, b = Y, c = Z;

    X = min(a, min(b, c));
    Z = max(a, max(b, c));
    Y = a + b + c - X - Z;

    // If Y - X is not equal to Z - Y
    if (Y - X != Z - Y) {
        cout << "NO";
        return;
    }

    // Finally print "Yes"
    cout << "Yes " << (Y - X);
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 3, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    isPossMakeThemEqual(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

  // Function to find whether it is possible
  // to make array elements equal using
  // one external number
  static void isPossMakeThemEqual(int arr[],
                                  int N)
  {

    int X = -1;
    int Y = -1;
    int Z = -1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

      // If X is equal to -1
      if (X == -1) {

        // Update the value of X
        X = arr[i];
      }

      // Otherwise, if X is not
      // equal to arr[i]
      else if (X != arr[i]) {

        // If Y is equal to -1
        if (Y == -1)
        {

          // Update Y
          Y = arr[i];
        }

        // Otherwise, if Y is not
        // equal to arr[i]
        else if (Y != arr[i]) {

          // If  Z is equal to -1
          if (Z == -1) {

            // Update the value
            // of Z
            Z = arr[i];
          }

          // Otherwise If Z is not
          // equal to arr[i], then
          // there are at least four
          // distinct numbers in array
          else if (Z != arr[i]) {
            System.out.println("NO");
            return;
          }
        }
      }
    }

    // If Y is equal to -1, then all
    // the array elements are equal
    if (Y == -1) {
      System.out.println("YES 0");
      return;
    }

    // If Z is equal to -1, then there
    // are only two distinct elements
    if (Z == -1) {
      System.out.println("YES "+ Math.abs(X - Y));
      return;
    }

    int a = X, b = Y, c = Z;

    X = Math.min(a, Math.min(b, c));
    Z = Math.max(a, Math.max(b, c));
    Y = a + b + c - X - Z;

    // If Y - X is not equal to Z - Y
    if (Y - X != Z - Y) {
      System.out.println("NO");
      return;
    }

    // Finally print "Yes"
    System.out.println("Yes "+(Y - X));
  }

  // Driver Code
  public static void main (String[] args)
  {
    int arr[] = { 2, 3, 3, 4, 2 };
    int N =arr.length;
    isPossMakeThemEqual(arr, N);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find whether it is possible
# to make array elements equal using
# one external number
def isPossMakeThemEqual(arr, N):
    X = -1
    Y = -1
    Z = -1

    # Traverse the array arr[]
    for i in range(N):

        # If X is equal to -1
        if (X == -1):

            # Update the value of X
            X = arr[i]

        # Otherwise, if X is not
        # equal to arr[i]
        elif (X != arr[i]):

            # If Y is equal to -1
            if (Y == -1):

                # Update Y
                Y = arr[i]

            # Otherwise, if Y is not
            # equal to arr[i]
            elif (Y != arr[i]):

                # If  Z is equal to -1
                if (Z == -1):

                    # Update the value
                    # of Z
                    Z = arr[i]

                # Otherwise If Z is not
                # equal to arr[i], then
                # there are at least four
                # distinct numbers in array
                elif (Z != arr[i]):
                    print("NO")
                    return

    # If Y is equal to -1, then all
    # the array elements are equal
    if (Y == -1):
        print("YES 0")
        return

    # If Z is equal to -1, then there
    # are only two distinct elements
    if (Z == -1):
        print("YES ",abs(X - Y))
        return

    a = X
    b = Y
    c = Z
    X = min(a, min(b, c))
    Z = max(a, max(b, c))
    Y = a + b + c - X - Z

    # If Y - X is not equal to Z - Y
    if (Y - X != Z - Y):
        print("NO")
        return

    # Finally print "Yes"
    print("Yes ",(Y - X))

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 3, 4, 2]
    N = len(arr)
    isPossMakeThemEqual(arr, N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for above approach
using System;

class GFG{

  // Function to find whether it is possible
  // to make array elements equal using
  // one external number
  static void isPossMakeThemEqual(int[] arr,
                                  int N)
  {

    int X = -1;
    int Y = -1;
    int Z = -1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

      // If X is equal to -1
      if (X == -1) {

        // Update the value of X
        X = arr[i];
      }

      // Otherwise, if X is not
      // equal to arr[i]
      else if (X != arr[i]) {

        // If Y is equal to -1
        if (Y == -1)
        {

          // Update Y
          Y = arr[i];
        }

        // Otherwise, if Y is not
        // equal to arr[i]
        else if (Y != arr[i]) {

          // If  Z is equal to -1
          if (Z == -1) {

            // Update the value
            // of Z
            Z = arr[i];
          }

          // Otherwise If Z is not
          // equal to arr[i], then
          // there are at least four
          // distinct numbers in array
          else if (Z != arr[i]) {
                Console.Write("NO");
            return;
          }
        }
      }
    }

    // If Y is equal to -1, then all
    // the array elements are equal
    if (Y == -1) {
      Console.Write("YES 0");
      return;
    }

    // If Z is equal to -1, then there
    // are only two distinct elements
    if (Z == -1) {
      Console.Write("YES "+ Math.Abs(X - Y));
      return;
    }

    int a = X, b = Y, c = Z;

    X = Math.Min(a, Math.Min(b, c));
    Z = Math.Max(a, Math.Max(b, c));
    Y = a + b + c - X - Z;

    // If Y - X is not equal to Z - Y
    if (Y - X != Z - Y) {
      Console.Write("NO");
      return;
    }

    // Finally print "Yes"
    Console.Write("Yes "+(Y - X));
  }

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 2, 3, 3, 4, 2 };
    int N =arr.Length;
    isPossMakeThemEqual(arr, N);
}
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // JavaScript Program for the above approach

  // Function to find whether it is possible
  // to make array elements equal using
  // one external number
  function isPossMakeThemEqual(arr, N)
  {

    let X = -1;
    let Y = -1;
    let Z = -1;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

      // If X is equal to -1
      if (X == -1) {

        // Update the value of X
        X = arr[i];
      }

      // Otherwise, if X is not
      // equal to arr[i]
      else if (X != arr[i]) {

        // If Y is equal to -1
        if (Y == -1)
        {

          // Update Y
          Y = arr[i];
        }

        // Otherwise, if Y is not
        // equal to arr[i]
        else if (Y != arr[i]) {

          // If  Z is equal to -1
          if (Z == -1) {

            // Update the value
            // of Z
            Z = arr[i];
          }

          // Otherwise If Z is not
          // equal to arr[i], then
          // there are at least four
          // distinct numbers in array
          else if (Z != arr[i]) {
            document.write("NO");
            return;
          }
        }
      }
    }

    // If Y is equal to -1, then all
    // the array elements are equal
    if (Y == -1) {
      document.write("YES 0");
      return;
    }

    // If Z is equal to -1, then there
    // are only two distinct elements
    if (Z == -1) {
      document.write("YES "+ Math.abs(X - Y));
      return;
    }

    let a = X, b = Y, c = Z;

    X = Math.min(a, Math.min(b, c));
    Z = Math.max(a, Math.max(b, c));
    Y = a + b + c - X - Z;

    // If Y - X is not equal to Z - Y
    if (Y - X != Z - Y) {
      document.write("NO");
      return;
    }

    // Finally print "Yes"
    document.write("Yes "+(Y - X));
  }

    // Driver Code

    let arr = [ 2, 3, 3, 4, 2 ];
    let N =arr.length;
    isPossMakeThemEqual(arr, N);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
Yes 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)