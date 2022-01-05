# 检查给定点是否位于任何给定塔的范围内

> 原文:[https://www . geesforgeks . org/检查给定点是否位于任何给定塔的范围内/](https://www.geeksforgeeks.org/check-if-given-point-lies-in-range-of-any-of-the-given-towers/)

给定由形式为 **{X <sub>i</sub> 、Y <sub>i</sub> 、R <sub>i</sub> }** 的 **N** 行组成的 [2D 阵**arr【】【】【**使得 **(X <sub>i</sub> 、Y <sub>i</sub> )** 代表塔的位置而**R<sub>I</sub>T23 给定两个整数 **X** 和 **Y** ，任务是检查点 **(X，Y)** 是否在塔的网络范围内。**](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)

**示例:**

> **输入:** arr[][] = { {1，1，3}，{10，10，5}，{15，15，15} }，X = 5，Y = 5
> **输出:**真
> **说明:**
> 点(5，5)与(arr[0][0]，arr[0][1])的距离= 5.65685，第一塔的范围为 3。因此，点(X，Y)不在第一个塔的网络范围内。
> 点(5，5)与(arr[1][0]，arr[1][1])的距离= 7.07107，二塔范围为 5。因此，点(X，Y)不在第二塔的网络范围内。
> 点(5，5)与(arr[2][0]，arr[2][1])的距离= 14.1421，三塔范围为 15。因此，点(X，Y)位于第三塔的网络范围内。
> 由于，点(X，Y)位于第三塔范围内。因此，所需的输出为真。
> 
> **输入:** arr[][] = { {1，1，3}，{10，10，3}，{15，15，3} }，X = 5，Y = 5
> T3】输出:假

**方法:**按照下面给出的步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于遍历的每一行(塔)，检查**sqrt((arr[I][0]–x)<sup>2</sup>+(arr[I][1]–Y)<sup>2</sup>)**的值是否大于 **arr[i][2]** 。如果发现为真，则打印**真**。
*   否则，打印**假**。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the point (X, Y)
// exists in the towers network-range or not
bool checkPointRange(int arr[][3], int X,
                     int Y, int N)
{

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores distance of the
        // point (X, Y) from i-th tower
        double dist
            = sqrt((arr[i][0] - X) * (arr[i][0] - X)
                   + (arr[i][1] - Y) * (arr[i][1] - Y));

        // If dist lies within the
        // range of the i-th tower
        if (dist <= arr[i][2]) {
            return true;
        }
    }

    // If the point (X, Y) does not lie
    // in the range of any of the towers
    return false;
}

// Driver Code
int main()
{

    int arr[][3] = { { 1, 1, 3 },
                     { 10, 10, 3 },
                     { 15, 15, 15 } };
    int X = 5, Y = 5;

    int N = sizeof(arr) / sizeof(arr[0]);

    // If point (X, Y) lies in the
    // range of any of the towers
    if (checkPointRange(arr, X, Y, N)) {
        cout << "True";
    }
    // Otherwise
    else {
        cout << "False";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if the point (X, Y)
// exists in the towers network-range or not
static boolean checkPointRange(int arr[][], int X,
                               int Y, int N)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Stores distance of the
        // point (X, Y) from i-th tower
        double dist = Math.sqrt((arr[i][0] - X) *
                                (arr[i][0] - X) +
                                (arr[i][1] - Y) *
                                (arr[i][1] - Y));

        // If dist lies within the
        // range of the i-th tower
        if (dist <= arr[i][2])
        {
            return true;
        }
    }

    // If the point (X, Y) does not lie
    // in the range of any of the towers
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[][] = { { 1, 1, 3 },
                    { 10, 10, 3 },
                    { 15, 15, 15 } };
    int X = 5, Y = 5;

    int N = arr.length;

    // If point (X, Y) lies in the
    // range of any of the towers
    if (checkPointRange(arr, X, Y, N))
    {
        System.out.print("True");
    }

    // Otherwise
    else
    {
        System.out.print("False");
    }
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import sqrt

# Function to check if the point (X, Y)
# exists in the towers network-range or not
def checkPointRange(arr, X, Y, N):

    # Traverse the array arr[]
    for i in range(N):

        # Stores distance of the
        # point (X, Y) from i-th tower
        dist = sqrt((arr[i][0] - X) *
                    (arr[i][0] - X) +
                    (arr[i][1] - Y) *
                    (arr[i][1] - Y))

        # If dist lies within the
        # range of the i-th tower
        if (dist <= arr[i][2]):
            return True

    # If the point (X, Y) does not lie
    # in the range of any of the towers
    return False

# Driver Code
if __name__ == '__main__':

    arr = [ [ 1, 1, 3 ],
            [ 10, 10, 3 ],
            [ 15, 15, 15 ] ]
    X = 5
    Y = 5

    N =  len(arr)

    # If point (X, Y) lies in the
    # range of any of the towers
    if (checkPointRange(arr, X, Y, N)):
        print("True")

    # Otherwise
    else:
        print("False")

# This code is contributed by bgangwar59
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to check if the point (X, Y)
// exists in the towers network-range or not
static bool checkPointRange(int[,] arr, int X,
                            int Y, int N)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Stores distance of the
        // point (X, Y) from i-th tower
        double dist = Math.Sqrt((arr[i, 0] - X) *
                                (arr[i, 0] - X) +
                                (arr[i, 1] - Y) *
                                (arr[i, 1] - Y));

        // If dist lies within the
        // range of the i-th tower
        if (dist <= arr[i, 2])
        {
            return true;
        }
    }

    // If the point (X, Y) does not lie
    // in the range of any of the towers
    return false;
}

// Driver Code
public static void Main()
{
    int[,] arr = { { 1, 1, 3 },
                   { 10, 10, 3 },
                   { 15, 15, 15 } };

    int X = 5, Y = 5;

    int N = arr.Length;

    // If point (X, Y) lies in the
    // range of any of the towers
    if (checkPointRange(arr, X, Y, N))
    {
        Console.Write("True");
    }

    // Otherwise
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if the point (X, Y)
// exists in the towers network-range or not
function checkPointRange(arr, X, Y, N)
{

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // Stores distance of the
        // point (X, Y) from i-th tower
        let dist = Math.sqrt((arr[i][0] - X) *
                                (arr[i][0] - X) +
                                (arr[i][1] - Y) *
                                (arr[i][1] - Y));

        // If dist lies within the
        // range of the i-th tower
        if (dist <= arr[i][2])
        {
            return true;
        }
    }

    // If the point (X, Y) does not lie
    // in the range of any of the towers
    return false;
}

// Driver Code

    let arr = [[ 1, 1, 3 ],
               [ 10, 10, 3 ],
              [ 15, 15, 15 ]];
    let X = 5, Y = 5;

    let N = arr.length;

    // If point (X, Y) lies in the
    // range of any of the towers
    if (checkPointRange(arr, X, Y, N))
    {
        document.write("True");
    }

    // Otherwise
    else
    {
        document.write("False");
    }

</script>
```

**Output:** 

```
True
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)