# 检查是否存在具有最大 X 和 Y 坐标的点

> 原文:[https://www . geesforgeks . org/check-a-point-with-maximum-x 和-y-坐标-存在与否/](https://www.geeksforgeeks.org/check-if-a-point-having-maximum-x-and-y-coordinates-exists-or-not/)

给定一个由表单 **(X，Y)** 的 **N** 坐标组成的 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定数组中找到一个坐标，使得该点的 **X 坐标**大于所有其他 **X 坐标**，该点的 **Y 坐标**大于所有其他 **Y 坐标**。如果不存在这样的点，打印 **-1** 。

**示例:**

> **输入:** arr[][] = {(1，2)，(2，1)，(3，4)，(4，3)，(5，5)}
> **输出:** (5，5)
> **解释:**
> 最大 X 坐标为 5，最大 Y 坐标为 5。
> 由于点(5，5)存在于数组中，打印(5，5)作为所需答案。
> 
> **输入:** arr[] = {(5，3)，(3，5)}
> **输出:** -1
> **说明:**
> 最大 X 坐标为 5，最大 Y 坐标为 5。因为+ (5，5)不存在。因此，打印-1。

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个点，检查是否是最大 **X** 和**Y**-坐标。如果不存在这样的点，打印 **-1** 。否则，将该点打印为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize INF as infinity
int INF = INT_MAX;

// Function to return the point having
// maximum X and Y coordinates
int* findMaxPoint(int arr[][2], int i, int n)
{

    // Base Case
    if (i == n)
    {
        arr[0][0] = INF;
        arr[0][1] = INF;
        return arr[0];
    }

    // Stores if valid point exists
    bool flag = true;

    // If point arr[i] is valid
    for(int j = 0; j < n; j++)
    {

        // Check for the same point
        if (j == i)
            continue;

        // Check for a valid point
        if (arr[j][0] >= arr[i][0] ||
            arr[j][1] >= arr[i][1])
        {
            flag = false;
            break;
        }
    }

    // If current point is the
    // required point
    if (flag)
        return arr[i];

    // Otherwise
    return findMaxPoint(arr, i + 1, n);
}

// Function to find the required point
void findMaxPoints(int arr[][2], int n)
{

    // Stores the point with maximum
    // X and Y-coordinates
    int ans[2];
    memcpy(ans, findMaxPoint(arr, 0, n),
           2 * sizeof(int));

    // If no required point exists
    if (ans[0] == INF)
    {
        cout << -1;
    }
    else
    {
        cout << "(" << ans[0] << " "
             << ans[1] << ")";
    }
}

// Driver Code
int main()
{

    // Given array of points
    int arr[][2] = { { 1, 2 }, { 2, 1 },
                     { 3, 4 }, { 4, 3 },
                     { 5, 5 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMaxPoints(arr, N);

    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Initialize INF as infinity
    static int INF = Integer.MAX_VALUE;

    // Function to return the point having
    // maximum X and Y coordinates
    static int[] findMaxPoint(
        int arr[][], int i, int n)
    {
        // Base Case
        if (i == n)
            return new int[] { INF, INF };

        // Stores if valid point exists
        boolean flag = true;

        // If point arr[i] is valid
        for (int j = 0; j < n; j++) {

            // Check for the same point
            if (j == i)
                continue;

            // Check for a valid point
            if (arr[j][0] >= arr[i][0]
                || arr[j][1] >= arr[i][1]) {
                flag = false;
                break;
            }
        }

        // If current point is the
        // required point
        if (flag)
            return arr[i];

        // Otherwise
        return findMaxPoint(arr, i + 1, n);
    }

    // Function to find the required point
    static void findMaxPoints(int arr[][],
                              int n)
    {
        // Stores the point with maximum
        // X and Y-coordinates
        int ans[] = findMaxPoint(arr, 0, n);

        // If no required point exists
        if (ans[0] == INF) {
            System.out.println(-1);
        }
        else {
            System.out.println(
                "(" + ans[0] + " "
                + ans[1] + ")");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array of points
        int arr[][] = new int[][] {{ 1, 2 }, { 2, 1 },
                                   { 3, 4 }, { 4, 3 },
                                   { 5, 5 }};

        int N = arr.length;

        // Function Call
        findMaxPoints(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import  sys

# Initialize INF as infinity
INF = sys.maxsize;

# Function to return the pohaving
# maximum X and Y coordinates
def findMaxPoint(arr, i, n):

    # Base Case
    if (i == n):
        return [INF, INF]

    # Stores if valid poexists
    flag = True;

    # If poarr[i] is valid
    for j in range(n):

        # Check for the same point
        if (j == i):
            continue;

        # Check for a valid point
        if (arr[j][0] >= arr[i][0] or arr[j][1] >= arr[i][1]):
            flag = False;
            break;

    # If current pois the
    # required point
    if (flag):
        return arr[i];

    # Otherwise
    return findMaxPoint(arr, i + 1, n);

# Function to find the required point
def findMaxPoints(arr, n):

    # Stores the powith maximum
    # X and Y-coordinates
    ans = findMaxPoint(arr, 0, n);

    # If no required poexists
    if (ans[0] == INF):
        print(-1);
    else:
        print("(" , ans[0] , " " , ans[1] , ")");

# Driver Code
if __name__ == '__main__':

    # Given array of points
    arr = [[1, 2],
           [2, 1],
           [3, 4],
           [4, 3],
           [5, 5]];

    N = len(arr);

    # Function Call
    findMaxPoints(arr, N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Initialize INF as infinity
static int INF = int.MaxValue;

// Function to return the point having
// maximum X and Y coordinates
static int[] findMaxPoint(int [,]arr, int i,
                          int n)
{

    // Base Case
    if (i == n)
        return new int[]{INF, INF};

    // Stores if valid point exists
    bool flag = true;

    // If point arr[i] is valid
    for(int j = 0; j < n; j++)
    {

        // Check for the same point
        if (j == i)
            continue;

        // Check for a valid point
        if (arr[j, 0] >= arr[i, 0] ||
            arr[j, 1] >= arr[i, 1])
        {
            flag = false;
            break;
        }
    }

    // If current point is the
    // required point
    int []ans  = new int[arr.GetLength(1)];
    if (flag)
    {
        for(int k = 0; k < ans.GetLength(0); k++)
            ans[k] = arr[i, k];

        return ans;
    }

    // Otherwise
    return findMaxPoint(arr, i + 1, n);
}

// Function to find the required point
static void findMaxPoints(int [,]arr,
                          int n)
{

    // Stores the point with maximum
    // X and Y-coordinates
    int []ans = findMaxPoint(arr, 0, n);

    // If no required point exists
    if (ans[0] == INF)
    {
        Console.WriteLine(-1);
    }
    else
    {
        Console.WriteLine("(" + ans[0] + " " +
                                ans[1] + ")");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array of points
    int [,]arr = new int[,]{ { 1, 2 }, { 2, 1 },
                             { 3, 4 }, { 4, 3 },
                             { 5, 5 } };

    int N = arr.GetLength(0);

    // Function Call
    findMaxPoints(arr, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Initialize INF as infinity
let INF = Number.MAX_VALUE;

// Function to return the point having
// maximum X and Y coordinates
function findMaxPoint(arr, i, n)
{

    // Base Case
    if (i == n)
        return [INF, INF];

    // Stores if valid point exists
    let flag = true;

    // If point arr[i] is valid
    for(let j = 0; j < n; j++)
    {

        // Check for the same point
        if (j == i)
            continue;

        // Check for a valid point
        if (arr[j][0] >= arr[i][0] ||
            arr[j][1] >= arr[i][1])
        {
            flag = false;
            break;
        }
    }

    // If current point is the
    // required point
    if (flag)
        return arr[i];

    // Otherwise
    return findMaxPoint(arr, i + 1, n);
}

// Function to find the required point
function findMaxPoints(arr, n)
{

    // Stores the point with maximum
    // X and Y-coordinates
    let ans = findMaxPoint(arr, 0, n);

    // If no required point exists
    if (ans[0] == INF)
    {
        document.write(-1);
    }
    else
    {
        document.write("(" + ans[0] + " " +
                             ans[1] + ")");
    }
}

// Driver code

// Given array of points
let arr = [ [ 1, 2 ], [ 2, 1 ],
            [ 3, 4 ], [ 4, 3 ],
            [ 5, 5 ] ];

let N = arr.length;

// Function Call
findMaxPoints(arr, N);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
(5 5)
```

***时间复杂度:** O(N <sup>2</sup> )其中 N 是给定数组的长度。*
***辅助空间:** O(N)*

**高效途径:**思路是寻找最大 **X** 和 **Y** 坐标。让他们成为 **maxX** 和 **maxY** 。再次遍历给定的数组，检查点( **maxX** 、 **maxY** )是否存在。按照以下步骤解决问题:

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，找到最大 **X** 和 **Y** 坐标。让他们成为 **maxX** 和 **maxY** 。
2.  再次遍历数组 **arr[]** 从 **i = 0 到 N-1** 检查 **(arr[i]。x，arr[i]。Y)** 等于 **(maxX，maxY)** 。
3.  如果阵列中存在 **(maxX，MaxY)****arr[]**，则打印 **(maxX，maxY)** 否则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 5
#define P 2

// Function to find the point having
// max X and Y coordinates
void findMaxPoint(int arr[N][P])
{

    // Initialize maxX and maxY
    int maxX = INT_MIN;
    int maxY = INT_MIN;

    // Length of the given array
    int n = N;

    // Get maximum X & Y coordinates
    for(int i = 0; i < n; i++)
    {
        maxX = max(maxX, arr[i][0]);
        maxY = max(maxY, arr[i][1]);
    }

    // Check if the required point
    // i.e., (maxX, maxY) is present
    for(int i = 0; i < n; i++)
    {

        // If point with maximum X and
        // Y coordinates is present
        if (maxX == arr[i][0] &&
            maxY == arr[i][1])
        {
            cout << "(" << maxX << ", "
                        << maxY << ")";

            return;
        }
    }

    // If no such point exists
    cout << (-1);
}

// Driver Code
int main()
{

    // Given array of points
    int arr[N][P] = { { 1, 2 }, { 2, 1 },
                      { 3, 4 }, { 4, 3 },
                      { 5, 5 } };

    // Print answer
    findMaxPoint(arr);
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to find the point having
    // max X and Y coordinates
    static void findMaxPoint(int arr[][])
    {
        // Initialize maxX and maxY
        int maxX = Integer.MIN_VALUE;
        int maxY = Integer.MIN_VALUE;

        // Length of the given array
        int n = arr.length;

        // Get maximum X & Y coordinates
        for (int i = 0; i < n; i++) {
            maxX = Math.max(maxX, arr[i][0]);
            maxY = Math.max(maxY, arr[i][1]);
        }

        // Check if the required point
        // i.e., (maxX, maxY) is present
        for (int i = 0; i < n; i++) {

            // If point with maximum X and
            // Y coordinates is present
            if (maxX == arr[i][0]
                && maxY == arr[i][1]) {

                System.out.println(
                    "(" + maxX + ", "
                    + maxY + ")");
                return;
            }
        }

        // If no such point exists
        System.out.println(-1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array of points
        int arr[][] = new int[][] {{ 1, 2 }, { 2, 1 },
                                   { 3, 4 }, { 4, 3 },
                                   { 5, 5 }};

        // Print answer
        findMaxPoint(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys;

# Function to find the pohaving
# max X and Y coordinates
def findMaxPoint(arr):

    # Initialize maxX and maxY
    maxX = -sys.maxsize;
    maxY = -sys.maxsize;

    # Length of the given array
    n = len(arr);

    # Get maximum X & Y coordinates
    for i in range(n):
        maxX = max(maxX, arr[i][0]);
        maxY = max(maxY, arr[i][1]);

    # Check if the required point
    # i.e., (maxX, maxY) is present
    for i in range(n):

        # If powith maximum X and
        # Y coordinates is present
        if (maxX == arr[i][0] and maxY == arr[i][1]):
            print("(" , maxX , ", " , maxY , ")");
            return;

    # If no such poexists
    print(-1);

# Driver Code
if __name__ == '__main__':

    # Given array of points
    arr = [[1, 2], [2, 1], [3, 4], [4, 3], [5, 5]];

    # Pranswer
    findMaxPoint(arr);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the point having
// max X and Y coordinates
static void findMaxPoint(int [,]arr)
{

    // Initialize maxX and maxY
    int maxX = int.MinValue;
    int maxY = int.MinValue;

    // Length of the given array
    int n = arr.GetLength(0);

    // Get maximum X & Y coordinates
    for(int i = 0; i < n; i++)
    {
        maxX = Math.Max(maxX, arr[i, 0]);
        maxY = Math.Max(maxY, arr[i, 1]);
    }

    // Check if the required point
    // i.e., (maxX, maxY) is present
    for(int i = 0; i < n; i++)
    {

        // If point with maximum X and
        // Y coordinates is present
        if (maxX == arr[i, 0] &&
            maxY == arr[i, 1])
        {
            Console.WriteLine("(" + maxX + ", " +
                                    maxY + ")");
            return;
        }
    }

    // If no such point exists
    Console.WriteLine(-1);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array of points
    int [,]arr = new int[,]{ { 1, 2 }, { 2, 1 },
                             { 3, 4 }, { 4, 3 },
                             { 5, 5 } };

    // Print answer
    findMaxPoint(arr);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
(5, 5)
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)