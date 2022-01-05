# 从满足给定条件的数组中计算坐标数

> 原文:[https://www . geeksforgeeks . org/count-满足给定条件的数组坐标数/](https://www.geeksforgeeks.org/count-number-of-coordinates-from-an-array-satisfying-the-given-conditions/)

给定一个由[笛卡尔平面](https://www.geeksforgeeks.org/cartesian-plane/)中的 **N** 坐标组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到满足以下所有条件的坐标数，如 **(X，Y)** :

1.  所有可能的 **arr[i][0]** 必须小于 **X** ， **arr[i][1]** 必须等于 **Y** 。
2.  所有可能的 **arr[i][0]** 必须大于 **X** ， **arr[i][1]** 必须等于 **Y** 。
3.  所有可能的 **arr[i][0]** 必须小于 **Y** ， **arr[i][1]** 必须等于 **X** 。
4.  所有可能的 **arr[i][0]** 必须大于 **Y** ， **arr[i][1]** 必须等于 **X** 。

**示例:**

> **输入:** arr[][] = {{0，0}，{0，1}，{1，0}，{0，-1}，{-1，0}}
> **输出:** 1
> **说明:**基于以下条件，只存在一个满足给定条件的坐标，即 **(0，0)** :
> 
> 1.  arr[2] = {1，0}:由于 arr[2][0](= 1) > X(= 0)和 arr[2][1](= 0)= Y(= 0)，因此满足条件 1。
> 2.  arr[4] = {-1，0}:由于 arr[4][0](= -1) < 0 且 arr[4][1](= 0) == Y(= 0)，因此满足条件 2。
> 3.  arr[1] = {0，1}:由于 arr[1][0](= 0) == X(= 0)和 arr[1][1](= 1) > Y(= 0)，因此满足条件 3。
> 4.  arr[3] = {0，-1}:由于 arr[3][0](= 0) == X(= 0)和 arr[3][1](= -1) < Y(= 0)，因此满足条件 4。
> 
> 因此，总点数为 1。
> 
> **输入:** arr[][] = {{1，0}，{2，0}，{1，1}，{1，-1}}
> **输出:** 0

**逼近:**给定问题可以通过考虑每一个坐标来求解，比如说 **(arr[i][0]、arr[i][1])** 作为合成坐标，如果坐标 **(arr[i][0]、arr[i][1])** 满足所有给定条件，那么就统计当前坐标。检查所有坐标后，打印获得的总计数值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// coordinates from a given set
// that satisfies the given conditions
int centralPoints(int arr[][2], int N)
{
    // Stores the count of central points
    int count = 0;

    // Store the count of
    // each x and y coordinates
    int c1, c2, c3, c4;

    // Find all possible pairs
    for (int i = 0; i < N; i++) {

        // Initialize variables c1, c2,
        // c3, c4 to define the status
        // of conditions
        c1 = 0, c2 = 0, c3 = 0;
        c4 = 0;

        // Stores value of each point
        int x = arr[i][0];
        int y = arr[i][1];

        // Check the conditions for
        // each point by generating
        // all possible pairs
        for (int j = 0; j < N; j++) {

            // If arr[j][0] > x and
            // arr[j][1] == y
            if (arr[j][0] > x
                && arr[j][1] == y) {
                c1 = 1;
            }

            // If arr[j][0] < x and
            // arr[j][1] == y
            if (arr[j][1] > y
                && arr[j][0] == x) {
                c2 = 1;
            }

            // If arr[j][1] > y and
            // arr[j][0] == x
            if (arr[j][0] < x
                && arr[j][1] == y) {
                c3 = 1;
            }

            // If arr[j][1] < y and
            // arr[j][0] == x
            if (arr[j][1] < y
                && arr[j][0] == x) {
                c4 = 1;
            }
        }

        // If all conditions satisfy
        // then point is central point
        if (c1 + c2 + c3 + c4 == 4) {

            // Increment the count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int arr[4][2] = { { 1, 0 }, { 2, 0 },
                      { 1, 1 }, { 1, -1 } };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << centralPoints(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to count the number of
    // coordinates from a given set
    // that satisfies the given conditions
    static int centralPoints(int arr[][], int N)
    {

        // Stores the count of central points
        int count = 0;

        // Store the count of
        // each x and y coordinates
        int c1, c2, c3, c4;

        // Find all possible pairs
        for (int i = 0; i < N; i++) {

            // Initialize variables c1, c2,
            // c3, c4 to define the status
            // of conditions
            c1 = 0;
            c2 = 0;
            c3 = 0;
            c4 = 0;

            // Stores value of each point
            int x = arr[i][0];
            int y = arr[i][1];

            // Check the conditions for
            // each point by generating
            // all possible pairs
            for (int j = 0; j < N; j++) {

                // If arr[j][0] > x and
                // arr[j][1] == y
                if (arr[j][0] > x && arr[j][1] == y) {
                    c1 = 1;
                }

                // If arr[j][0] < x and
                // arr[j][1] == y
                if (arr[j][1] > y && arr[j][0] == x) {
                    c2 = 1;
                }

                // If arr[j][1] > y and
                // arr[j][0] == x
                if (arr[j][0] < x && arr[j][1] == y) {
                    c3 = 1;
                }

                // If arr[j][1] < y and
                // arr[j][0] == x
                if (arr[j][1] < y && arr[j][0] == x) {
                    c4 = 1;
                }
            }

            // If all conditions satisfy
            // then point is central point
            if (c1 + c2 + c3 + c4 == 4) {

                // Increment the count by 1
                count++;
            }
        }

        // Return the count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[][]
            = { { 1, 0 }, { 2, 0 }, { 1, 1 }, { 1, -1 } };
        int N = arr.length;
        System.out.println(centralPoints(arr, N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# coordinates from a given set
# that satisfies the given conditions
def centralPoints(arr, N):

    # Stores the count of central points
    count = 0

    # Find all possible pairs
    for i in range(N):

        # Initialize variables c1, c2,
        # c3, c4 to define the status
        # of conditions
        c1 = 0
        c2 = 0
        c3 = 0
        c4 = 0

        # Stores value of each point
        x = arr[i][0]
        y = arr[i][1]

        # Check the conditions for
        # each point by generating
        # all possible pairs
        for j in range(N):

            # If arr[j][0] > x and
            # arr[j][1] == y
            if (arr[j][0] > x and arr[j][1] == y):
                c1 = 1

            # If arr[j][0] < x and
            # arr[j][1] == y
            if (arr[j][1] > y and arr[j][0] == x):
                c2 = 1

            # If arr[j][1] > y and
            # arr[j][0] == x
            if (arr[j][0] < x and arr[j][1] == y):
                c3 = 1

            # If arr[j][1] < y and
            # arr[j][0] == x
            if (arr[j][1] < y and arr[j][0] == x):
                c4 = 1

        # If all conditions satisfy
        # then point is central point
        if (c1 + c2 + c3 + c4 == 4):

            # Increment the count by 1
            count += 1

    # Return the count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ [ 1, 0 ], [ 2, 0 ],
            [ 1, 1 ], [ 1, -1 ] ]
    N = len(arr)

    print(centralPoints(arr, N));

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// coordinates from a given set
// that satisfies the given conditions
static int centralPoints(int[,] arr, int N)
{

    // Stores the count of central points
    int count = 0;

    // Store the count of
    // each x and y coordinates
    int c1, c2, c3, c4;

    // Find all possible pairs
    for(int i = 0; i < N; i++)
    {

        // Initialize variables c1, c2,
        // c3, c4 to define the status
        // of conditions
        c1 = 0;
        c2 = 0;
        c3 = 0;
        c4 = 0;

        // Stores value of each point
        int x = arr[i, 0];
        int y = arr[i, 1];

        // Check the conditions for
        // each point by generating
        // all possible pairs
        for(int j = 0; j < N; j++)
        {

            // If arr[j][0] > x and
            // arr[j][1] == y
            if (arr[j, 0] > x && arr[j, 1] == y)
            {
                c1 = 1;
            }

            // If arr[j][0] < x and
            // arr[j][1] == y
            if (arr[j, 1] > y && arr[j, 0] == x)
            {
                c2 = 1;
            }

            // If arr[j][1] > y and
            // arr[j][0] == x
            if (arr[j, 0] < x && arr[j, 1] == y)
            {
                c3 = 1;
            }

            // If arr[j][1] < y and
            // arr[j][0] == x
            if (arr[j, 1] < y && arr[j, 0] == x)
            {
                c4 = 1;
            }
        }

        // If all conditions satisfy
        // then point is central point
        if (c1 + c2 + c3 + c4 == 4)
        {

            // Increment the count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void Main(string[] args)
{
    int[,] arr = { { 1, 0 }, { 2, 0 },
                   { 1, 1 }, { 1, -1 } };
    int N = arr.GetLength(0);

    Console.WriteLine(centralPoints(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach

    // Function to count the number of
    // coordinates from a given set
    // that satisfies the given conditions
    function centralPoints(arr, N)
    {

        // Stores the count of central points
        let count = 0;

        // Store the count of
        // each x and y coordinates
        let c1, c2, c3, c4;

        // Find all possible pairs
        for (let i = 0; i < N; i++) {

            // Initialize variables c1, c2,
            // c3, c4 to define the status
            // of conditions
            c1 = 0;
            c2 = 0;
            c3 = 0;
            c4 = 0;

            // Stores value of each point
            let x = arr[i][0];
            let y = arr[i][1];

            // Check the conditions for
            // each point by generating
            // all possible pairs
            for (let j = 0; j < N; j++) {

                // If arr[j][0] > x and
                // arr[j][1] == y
                if (arr[j][0] > x && arr[j][1] == y) {
                    c1 = 1;
                }

                // If arr[j][0] < x and
                // arr[j][1] == y
                if (arr[j][1] > y && arr[j][0] == x) {
                    c2 = 1;
                }

                // If arr[j][1] > y and
                // arr[j][0] == x
                if (arr[j][0] < x && arr[j][1] == y) {
                    c3 = 1;
                }

                // If arr[j][1] < y and
                // arr[j][0] == x
                if (arr[j][1] < y && arr[j][0] == x) {
                    c4 = 1;
                }
            }

            // If all conditions satisfy
            // then point is central point
            if (c1 + c2 + c3 + c4 == 4) {

                // Increment the count by 1
                count++;
            }
        }

        // Return the count
        return count;
    }

// Driver Code
    let arr = [[ 1, 0 ], [ 2, 0 ], [ 1, 1 ], [ 1, -1 ]];
    let N = arr.length;
   document.write(centralPoints(arr, N));

 // This code is contributed by splevel62.
</script>
```

**Output:** 

```
0
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*