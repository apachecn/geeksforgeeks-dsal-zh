# 检查在曼哈顿距离 N 个给定点最多为 K 的平面中是否存在任何点

> 原文:[https://www . geeksforgeeks . org/检查飞机上是否存在任何点，其曼哈顿距离最多为 n 个给定点的 k 倍/](https://www.geeksforgeeks.org/check-if-any-point-exists-in-a-plane-whose-manhattan-distance-is-at-most-k-from-n-given-points/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**由平面内 **N** 个不同点的 **X** 和 **Y** 坐标以及正整数 **K** 组成，任务是检查平面内是否存在点 **P** ，使得该点与所有给定点之间的[曼哈顿距离](https://www.geeksforgeeks.org/find-the-integer-points-x-y-with-manhattan-distance-atleast-n/)至多为**K 如果存在这样的点 **P** ，则打印**“是”**。否则，打印**“否”**。**

**示例:**

> ***输入:*** A[] = {1，0，2，1，1}，B[] = {1，1，1，0，2}，K = 1
> ***输出:**是*
> ***解释:***
> *考虑一个点 P(1，1)，那么 P 与所有给定点之间的曼哈顿距离为:*
> 
> *   *P 与(A[0]，B[0])的距离为| 1–1 |+| 1–1 | = 0。*
> *   *P 与(A[1]，B[1])的距离为| 1–0 |+| 1–1 | = 1。*
> *   *P 与(A[2]，B[2])的距离为| 1–2 |+| 1–1 | = 1。*
> *   *P 与(A[3]，B[3])的距离为| 1–1 |+| 1–0 | = 1。*
> *   *P 与(A[4]，B[4])的距离为| 1–1 |+| 1–2 | = 1。*
> 
> 所有给定点和 P 之间的距离最多为 K(= 1)。因此，打印“是”。
> 
> ***输入:*** A[] = {0，3，1}，B[] = {0，3，1}，K = 2
> ***输出:*** 否

**方法:**给定的问题可以通过[求每对 **N** 给定点](https://www.geeksforgeeks.org/minimum-manhattan-distance-covered-by-visiting-every-coordinates-from-a-source-to-a-final-vertex/)之间的曼哈顿距离来解决。检查所有点对后，如果点对之间的距离计数最多为**K，**则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if there
// exists any point with at most
// K distance from N given points
string find(int a[], int b[], int N, int K)
{

    // Traverse the given N points
    for(int i = 0; i < N; i++)
    {

        // Stores the count of pairs
        // of coordinates having
        // Manhattan distance <= K
        int count = 0;

        for(int j = 0; j < N; j++)
        {

            // For the same coordinate
            if (i == j)
            {
                continue;
            }

            // Calculate Manhattan distance
            long long int dis = abs(a[i] - a[j]) +
                                abs(b[i] - b[j]);

            // If Manhattan distance <= K
            if (dis <= K)
            {
                count++;
            }

            // If all coordinates
            // can meet
            if (count == N - 1)
            {
                return "Yes";
            }
        }
    }

    // If all coordinates can't meet
    return "No";
}

// Driver Code
int main()
{
    int N = 5;
    int A[] = { 1, 0, 2, 1, 1 };
    int B[] = { 1, 1, 1, 0, 2 };
    int K = 1;

    cout << find(A, B, N, K) << endl;
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to check if there
    // exists any point with at most
    // K distance from N given points
    public static String find(
        int[] a, int[] b, int N, int K)
    {
        // Traverse the given N points
        for (int i = 0; i < N; i++) {

            // Stores the count of pairs
            // of coordinates having
            // Manhattan distance <= K
            int count = 0;

            for (int j = 0; j < N; j++) {

                // For the same coordinate
                if (i == j) {
                    continue;
                }

                // Calculate Manhattan distance
                long dis = Math.abs(a[i] - a[j])
                           + Math.abs(b[i] - b[j]);

                // If Manhattan distance <= K
                if (dis <= K) {

                    count++;
                }

                // If all coordinates
                // can meet
                if (count == N - 1) {
                    return "Yes";
                }
            }
        }

        // If all coordinates can't meet
        return "No";
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        int[] A = { 1, 0, 2, 1, 1 };
        int[] B = { 1, 1, 1, 0, 2 };
        int K = 1;

        System.out.println(
            find(A, B, N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there
# exists any point with at most
# K distance from N given points
def find(a, b, N, K):

    # Traverse the given n points
    for i in range(N):

        # Stores the count of pairs
        # of coordinates having
        # Manhattan distance <= K
        count = 0
        for j in range(N):

            # For the same coordinate
            if (i == j):
                continue

            # Calculate Manhattan distance
            dis = abs(a[i] - a[j]) + abs(b[i] - b[j])

            # If Manhattan distance <= K
            if (dis <= K):
                count = count + 1

            # If all coordinates
            # can meet
            if (count == N - 1):
                return "Yes"

        # If all coordinates can't meet
        return "No"

# Driver code
N = 5
A = [ 1, 0, 2, 1, 1 ]
B = [ 1, 1, 1, 0, 2 ]
K = 1

print(find(A, B, N, K))

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if there
// exists any point with at most
// K distance from N given points
public static String find(int[] a, int[] b,
                          int N, int K)
{

    // Traverse the given N points
    for(int i = 0; i < N; i++)
    {

        // Stores the count of pairs
        // of coordinates having
        // Manhattan distance <= K
        int count = 0;

        for(int j = 0; j < N; j++)
        {

            // For the same coordinate
            if (i == j)
            {
                continue;
            }

            // Calculate Manhattan distance
            long dis = Math.Abs(a[i] - a[j]) +
                       Math.Abs(b[i] - b[j]);

            // If Manhattan distance <= K
            if (dis <= K)
            {
                count++;
            }

            // If all coordinates
            // can meet
            if (count == N - 1)
            {
                return "Yes";
            }
        }
    }

    // If all coordinates can't meet
    return "No";
}

// Driver Code
public static void Main(string[] args)
{
    int N = 5;
    int[] A = { 1, 0, 2, 1, 1 };
    int[] B = { 1, 1, 1, 0, 2 };
    int K = 1;

    Console.WriteLine(find(A, B, N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
        // Javascript program for
        // the above approach

        // Function to check if there
        // exists any point with at most
        // K distance from N given points
        function find(a, b, N, K) {

            // Traverse the given N points
            for (let i = 0; i < N; i++) {

                // Stores the count of pairs
                // of coordinates having
                // Manhattan distance <= K
                let count = 0;

                for (let j = 0; j < N; j++) {

                    // For the same coordinate
                    if (i == j) {
                        continue;
                    }

                    // Calculate Manhattan distance
                    let dis = Math.abs(a[i] - a[j]) +
                        Math.abs(b[i] - b[j]);

                    // If Manhattan distance <= K
                    if (dis <= K) {
                        count++;
                    }

                    // If all coordinates
                    // can meet
                    if (count == N - 1) {
                        return "Yes";
                    }
                }
            }

            // If all coordinates can't meet
            return "No";
        }

        // Driver Code

        let N = 5;
        let A = [ 1, 0, 2, 1, 1 ];
        let B = [ 1, 1, 1, 0, 2 ];
        let K = 1;

        document.write(find(A, B, N, K));

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*