# 使用数组中给出的距离检查是否有可能到达点(X，Y)

> 原文:[https://www . geeksforgeeks . org/check-如果有可能到达 x-y 点-使用阵列中给定的距离/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-the-point-x-y-using-distances-given-in-an-array/)

给定一个由 **N** 正整数和两个整数 **X** 和 **Y** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是检查是否有可能从 **(0，0)** 到达 **(X，Y)** ，从而从**移动到 **(X <sub>f</sub> ，Y <sub>f</sub> )** 如果可能，则打印**是**。否则，打印**否**。**

**注意:**阵中出现的每个距离**arr【】**最多可以使用**一次**。

**示例:**

> **输入:** arr[ ] = {2，5}，X = 5，Y= 4
> **输出:**是
> **说明:**
> 以下是从(0，0)到(5，4)需要达到的招式:
> 
> 1.  从点(0，0)移动到(2，0)。欧几里德距离是 sqrt((2–0)<sup>2</sup>+(0–0))= 2，它存在于数组中。
> 2.  从点(2，0)移动到(5，4)。欧几里德距离是 sqrt((5–2)<sup>2</sup>+(4–0)<sup>2</sup>)= 5，存在于数组中。
> 
> 完成以上一组动作后，可以到达点(5，4)。因此，打印“是”。
> 
> **输入:** arr[] = {4}，X = 3，Y= 4
> **输出:**否

**逼近:**通过考虑点 **(0，0)** 到 **(X，Y)** 之间的**欧几里德距离**作为 **Z = sqrt(X*X + Y*Y)** ，给定的问题可以用下面的观测值求解，那么问题可以分为 3 种情况:

*   如果阵元的[和小于 **Z** ，任何一套招式都不可能达到 **(X，Y)** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   如果阵元之和等于 **Z** ，则 **N** 移动后有可能到达 **(X，Y)** 。
*   否则，对于每个距离，检查以下情况:
    *   如果对于任何 **A[i]** 、 **A[i] > Z +(除了 A[i])** 之外的所有其他距离，则永远不可能到达 **(X，Y)** ，因为路径将是多边形，对于 N 多边形，每条可能的边的(N–1)条边的总和必须大于另一条边。
    *   否则，总是有可能到达点 **(X，Y)** 。

根据以上考虑三种情况的观察，相应地打印结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the point (X, Y)
// is reachable from (0, 0) or not
int isPossibleToReach(int A[], int N, int X, int Y)
{
    // Find the Euclidian Distance
    double distance = sqrt(double(X * X + Y * Y));

    // Calculate the maximum distance
    double mx = 0;
    for (int i = 0; i < N; i++) {
        mx += double(A[i]);
    }

    // Case 1.
    if (mx < distance) {
        cout << "NO";
        return 0;
    }

    // Case 2.
    if ((mx - distance) < 0.000001) {
        cout << "YES";
        return 0;
    }

    // Otherwise, check for the polygon
    // condition for each side
    for (int i = 0; i < N; i++) {

        if (distance + mx
            < double(2) * double(A[i])) {
            cout << "No";
            return 0;
        }
    }

    // Otherwise, print Yes
    cout << "Yes";

    return 0;
}

// Driver Code
int main()
{
    int A[] = { 2, 5 };
    int X = 5, Y = 4;
    int N = sizeof(A) / sizeof(A[0]);

    isPossibleToReach(A, N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C# program for the above approach
import java.io.*;

class GFG{

// Function to check if the point (X, Y)
// is reachable from (0, 0) or not
static int isPossibleToReach(int []A, int N,
                             int X, int Y)
{

    // Find the Euclidian Distance
    double distance = Math.sqrt((X * X + Y * Y));

    // Calculate the maximum distance
    double mx = 0;
    for(int i = 0; i < N; i++)
    {
        mx += (A[i]);
    }

    // Case 1.
    if (mx < distance)
    {
        System.out.print("NO");
        return 0;
    }

    // Case 2.
    if ((mx - distance) < 0.000001)
    {
        System.out.print("YES");
        return 0;
    }

    // Otherwise, check for the polygon
    // condition for each side
    for(int i = 0; i < N; i++)
    {
        if (distance + mx < 2 * A[i])
        {
            System.out.print("No");
            return 0;
        }
    }

    // Otherwise, print Yes
    System.out.print("Yes");

    return 0;
}

// Driver Code
public static void main (String[] args)
{
    int []A = { 2, 5 };
    int X = 5, Y = 4;
    int N = A.length;

    isPossibleToReach(A, N, X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to check if the po(X, Y)
# is reachable from (0, 0) or not
def isPossibleToReach(A, N, X, Y):

    # Find the Euclidian Distance
    distance = math.sqrt(X * X + Y * Y)

    # Calculate the maximum distance
    mx = 0
    for i in range(N):
        mx += A[i]

    # Case 1.
    if (mx < distance):
        print("NO")
        return 0

    # Case 2.
    if ((mx - distance) < 0.000001):
        print("YES")
        return 0

    # Otherwise, check for the polygon
    # condition for each side
    for i in range(N):
        if (distance + mx < (2) * (A[i])):
            print("No")
            return 0

    # Otherwise, prYes
    print("Yes")
    return 0

# Driver Code
A = [2, 5]
X = 5
Y = 4
N = len(A)

isPossibleToReach(A, N, X, Y)

# This code is contributed by shivani.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the point (X, Y)
// is reachable from (0, 0) or not
static int isPossibleToReach(int []A, int N,
                             int X, int Y)
{

    // Find the Euclidian Distance
    double distance = Math.Sqrt((X * X + Y * Y));

    // Calculate the maximum distance
    double mx = 0;
    for(int i = 0; i < N; i++)
    {
        mx += (A[i]);
    }

    // Case 1.
    if (mx < distance)
    {
        Console.Write("NO");
        return 0;
    }

    // Case 2.
    if ((mx - distance) < 0.000001)
    {
        Console.Write("YES");
        return 0;
    }

    // Otherwise, check for the polygon
    // condition for each side
    for(int i = 0; i < N; i++)
    {
        if (distance + mx < 2 * A[i])
        {
            Console.Write("No");
            return 0;
        }
    }

    // Otherwise, print Yes
    Console.Write("Yes");

    return 0;
}

// Driver Code
static public void Main ()
{
    int []A = { 2, 5 };
    int X = 5, Y = 4;
    int N = A.Length;

    isPossibleToReach(A, N, X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to check if the point (X, Y)
        // is reachable from (0, 0) or not
        function isPossibleToReach(A, N, X, Y)
        {

            // Find the Euclidian Distance
            let distance = Math.sqrt((X * X + Y * Y));

            // Calculate the maximum distance
            let mx = 0;
            for (let i = 0; i < N; i++) {
                mx += A[i];
            }

            // Case 1.
            if (mx < distance) {
                document.write("NO");
                return 0;
            }

            // Case 2.
            if ((mx - distance) < 0.000001) {
                document.write("YES");
                return 0;
            }

            // Otherwise, check for the polygon
            // condition for each side
            for (let i = 0; i < N; i++) {

                if (distance + mx
                    < 2 * A[i]) {
                    document.write("No");
                    return 0;
                }
            }

            // Otherwise, print Yes
            document.write("Yes");

            return 0;
        }

        // Driver Code

        let A = [2, 5];
        let X = 5, Y = 4;
        let N = A.length;

        isPossibleToReach(A, N, X, Y);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)