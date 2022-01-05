# 查询通过添加或相乘数组元素来更新数组，并打印指定索引处的元素

> 原文:[https://www . geesforgeks . org/query-to-update-array-by-add-or-乘-array-elements-and-print-element-present-at-specific-index/](https://www.geeksforgeeks.org/queries-to-update-array-by-adding-or-multiplying-array-elements-and-print-the-element-present-at-specified-index/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由 **M** [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**Q【】**表示类型为 **{X，Y}** 的查询，任务是执行以下类型的查询:

*   **查询(0，X):** 给每个数组元素添加整数 **X** 。
*   **查询(1，Y):** 将每个数组元素乘以 **Y** 。
*   **查询(2，i):** 打印索引 **i** 处的值。

**示例:**

> **输入:** arr[] = {5，1，2，3，9}，Q[][] = {{0，5}，{2，4}，{1，4}，{0，2}，{2，3 } }
> T3】输出:14 34
> T6】解释:T8】以下是执行每次查询后的结果:
> 
> 1.  **查询(0，5):** 向每个数组元素添加 5，将数组修改为 arr[] = {10，6，7，8，14}。
> 2.  **查询(2，4):** 打印索引 4 处的数组元素，即 arr[4] = 14。
> 3.  **查询(1，4):** 将每个数组元素乘以 4，将数组修改为 arr[] = {40，24，28，32，56}
> 4.  **查询(0，2):** 向每个数组元素添加 2，将数组修改为 arr[] = {42，26，30，34，58}
> 5.  **查询(2，3):** 打印索引 4 处的元素，即 arr[3] = 34。
> 
> **输入:** arr[] = {3，1，23，45，100}，Q[][] = {{1，2}，{0，10}，{2，3}，{1，5}，{2，4}}
> **输出:** 100 1050

**朴素方法:**解决给定问题最简单的方法是通过[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来执行每个查询，并为每个查询相应地打印结果。

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   假设 **A** 是一个元素，执行以下操作:
    *   将 **a1** 加到 **A** 上，则 **A** 的值变为 **A = A + a1** 。
    *   将 **A** 乘以 **b1** ，则 **A** 的值变为 **A = b1 * A + b1 * a1** 。
    *   将 **a2** 加到 **A** 上，则 **A** 的值变为 **A = b1 * A + b1 * a1 + a2** 。
    *   将 **A** 乘以 **b2** ，则 **A** 的值变为， **A = b1 * b2 * A + b1 * b2 * a1 + a2 * b2**
*   假设 **Mul** 是类型 **1** 和**相加的所有整数的乘积，存储了类型**0**和类型**1**的所有查询的值，按照给定的顺序执行，从 **0** 开始。然后从上面可以观察到任何数组元素 **arr[i]** 修改为 **(arr[i] * Mul + Add)** 。**

按照以下步骤解决问题:

*   初始化两个变量，比如说 **Mul** 为 **1** 和 **Add** 为 **0，**存储 **2** 类型查询中所有整数的乘积，并在一个数字 **0** 上按照给定的顺序存储执行 **1** 和 **2** 类型查询后得到的值。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q[]【2】**，并执行以下步骤:
    *   如果 **Q[i][0]** 是 **0** ，那么将**的值增加**到 **Q[i][1]** 。
    *   否则，如果 **Q[i][0]** 的值为 **1** ，则将 **Mul** 和**相加**得到 **Q[i][1]** 。
    *   否则，打印值 **(arr[Q[i][1]] * Mul + Add)** 作为查询**类型 2** 的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify the array
// by performing given queries
void Query(int arr[], int N,
           vector<vector<int> > Q)
{
    // Stores the multiplication
    // of all integers of type 1
    int mul = 1;

    // Stores the value obtained after
    // performing queries of type 1 & 2
    int add = 0;

    // Iterate over the queries
    for (int i = 0; i < Q.size(); i++) {

        // Query of type 0
        if (Q[i][0] == 0) {

            // Update the value of add
            add = add + Q[i][1];
        }

        // Query of type 1
        else if (Q[i][0] == 1) {

            // Update the value of mul
            mul = mul * Q[i][1];

            // Update the value of add
            add = add * Q[i][1];
        }

        // Otherwise
        else {

            // Store the element at index Q[i][1]
            int ans = arr[Q[i][1]] * mul + add;

            // Print the result for
            // the current query
            cout << ans << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 23, 45, 100 };
    int N = sizeof(arr) / sizeof(arr[0]);

    vector<vector<int> > Q = {
        { 1, 2 }, { 0, 10 },
        { 2, 3 }, { 1, 5 }, { 2, 4 }
    };
    Query(arr, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG
{

    // Function to modify the array
    // by performing given queries
    static void Query(int arr[], int N, int Q[][])
    {

        // Stores the multiplication
        // of all integers of type 1
        int mul = 1;

        // Stores the value obtained after
        // performing queries of type 1 & 2
        int add = 0;

        // Iterate over the queries
        for (int i = 0; i < Q.length; i++) {

            // Query of type 0
            if (Q[i][0] == 0) {

                // Update the value of add
                add = add + Q[i][1];
            }

            // Query of type 1
            else if (Q[i][0] == 1) {

                // Update the value of mul
                mul = mul * Q[i][1];

                // Update the value of add
                add = add * Q[i][1];
            }

            // Otherwise
            else {

                // Store the element at index Q[i][1]
                int ans = arr[Q[i][1]] * mul + add;

                // Print the result for
                // the current query
                System.out.print(ans + " ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 3, 1, 23, 45, 100 };
        int N = arr.length;

        int Q[][] = { { 1, 2 },
                      { 0, 10 },
                      { 2, 3 },
                      { 1, 5 },
                      { 2, 4 } };
        Query(arr, N, Q);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify the array
# by performing given queries
def Query(arr, N, Q):

    # Stores the multiplication
    # of all integers of type 1
    mul = 1

    # Stores the value obtained after
    # performing queries of type 1 & 2
    add = 0

    # Iterate over the queries
    for i in range(len(Q)):

        # Query of type 0
        if (Q[i][0] == 0):

            # Update the value of add
            add = add + Q[i][1]

        # Query of type 1
        elif (Q[i][0] == 1):

            # Update the value of mul
            mul = mul * Q[i][1]

            # Update the value of add
            add = add * Q[i][1]
        # Otherwise
        else:

            # Store the element at index Q[i][1]
            ans = arr[Q[i][1]] * mul + add

            # Prthe result for
            # the current query
            print(ans,end=" ")

# Driver Code
if __name__ == '__main__':

    arr = [3, 1, 23, 45, 100]
    N = len(arr)
    Q = [
        [ 1, 2 ], [ 0, 10 ],
        [ 2, 3 ], [ 1, 5 ], [ 2, 4 ]
    ]
    Query(arr, N, Q)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to modify the array
  // by performing given queries
  static void Query(int[] arr, int N, int[, ] Q)
  {
    // Stores the multiplication
    // of all integers of type 1
    int mul = 1;

    // Stores the value obtained after
    // performing queries of type 1 & 2
    int add = 0;

    // Iterate over the queries
    for (int i = 0; i < Q.GetLength(0); i++) {

      // Query of type 0
      if (Q[i, 0] == 0) {

        // Update the value of add
        add = add + Q[i, 1];
      }

      // Query of type 1
      else if (Q[i, 0] == 1) {

        // Update the value of mul
        mul = mul * Q[i, 1];

        // Update the value of add
        add = add * Q[i, 1];
      }

      // Otherwise
      else {

        // Store the element at index Q[i][1]
        int ans = arr[Q[i, 1]] * mul + add;

        // Print the result for
        // the current query
        Console.Write(ans + " ");
      }
    }
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 3, 1, 23, 45, 100 };
    int N = arr.Length;

    int[, ] Q = { { 1, 2 },
                 { 0, 10 },
                 { 2, 3 },
                 { 1, 5 },
                 { 2, 4 } };
    Query(arr, N, Q);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to modify the array
    // by performing given queries
    function Query(arr, N, Q)
    {

        // Stores the multiplication
        // of all integers of type 1
        let mul = 1;

        // Stores the value obtained after
        // performing queries of type 1 & 2
        let add = 0;

        // Iterate over the queries
        for (let i = 0; i < Q.length; i++) {

            // Query of type 0
            if (Q[i][0] == 0) {

                // Update the value of add
                add = add + Q[i][1];
            }

            // Query of type 1
            else if (Q[i][0] == 1) {

                // Update the value of mul
                mul = mul * Q[i][1];

                // Update the value of add
                add = add * Q[i][1];
            }

            // Otherwise
            else {

                // Store the element at index Q[i][1]
                let ans = arr[Q[i][1]] * mul + add;

                // Print the result for
                // the current query
                document.write(ans + " ");
            }
        }
    }

  // Driver Code

     let arr = [ 3, 1, 23, 45, 100 ];
        let N = arr.length;

        let Q = [[ 1, 2 ],
                      [ 0, 10 ],
                      [ 2, 3 ],
                      [ 1, 5 ],
                      [ 2, 4 ]];
        Query(arr, N, Q);

</script>

```

**Output:** 

```
100 1050
```

***时间复杂度:**O(M)*
T5**辅助空间:** O(1)