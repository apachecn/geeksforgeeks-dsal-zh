# 具有整数交点的线对数量

> 原文:[https://www . geesforgeks . org/有整数交点的线对数/](https://www.geeksforgeeks.org/number-of-pairs-of-lines-having-integer-intersection-points/)

给定两个整数数组 **P[]** 和 **Q[]** ，其中*T5】P<sub>I</sub>T9】和***Q<sub>j</sub>**T15】对于每个 *0 < = i <尺寸(P)* 和 *0 < = j <尺寸(Q)* 表示直线方程 ***x 任务是从有整数交点的 **P[]** 和 **Q[]** 中找出对的个数。*****

**示例:**

> **输入:** P[] = {1，3，2}，Q[] = {3，0}
> **输出:** 3
> 具有整数交点的线对(P，Q)为(1，3)、(2，0)和(3，3)。这里 P 是 P[]的线参数，Q 是 Q[]的线参数。
> 
> **输入:** P[] = {1，4，3，2}，Q[] = {3，6，10，11 }
> T3】输出: 8

**进场:**

*   通过求解这两个方程，分析整数交点的条件，可以很容易地解决这个问题。
*   这两个方程是***x–y =-p***和 ***x + y = q*** 。
*   求解 **x** 和 **y** 我们得到， **x = (q-p)/2** 和 **y = (p+q)/2** 。
*   很明显，当且仅当 **p** 和 **q** 具有相同的奇偶性时，整数交点是可能的。
*   让 **p <sub>0</sub>** 和 **p <sub>1</sub>** 分别为偶数和奇数 **p <sub>i</sub>** 的个数。
*   同理，偶数和奇数的数量分别为**q<sub>0</sub>T3**q<sub>1</sub>T7**q<sub>I</sub>T11】。******
*   所以需要的答案是**p<sub>0</sub>T3】***q<sub>0</sub>T7】+**p<sub>1</sub>T11】***q<sub>1</sub>T15】。********

下面是上述方法的实现:

## C++

```
// C++ program to Number of pairs of lines
// having integer intersection points

#include <bits/stdc++.h>
using namespace std;

// Count number of pairs of lines
// having integer intersection point
int countPairs(int* P, int* Q, int N, int M)
{
    // Initialize arrays to store counts
    int A[2] = { 0 }, B[2] = { 0 };

    // Count number of odd and even Pi
    for (int i = 0; i < N; i++)
        A[P[i] % 2]++;

    // Count number of odd and even Qi
    for (int i = 0; i < M; i++)
        B[Q[i] % 2]++;

    // Return the count of pairs
    return (A[0] * B[0] + A[1] * B[1]);
}

// Driver code
int main()
{
    int P[] = { 1, 3, 2 }, Q[] = { 3, 0 };
    int N = sizeof(P) / sizeof(P[0]);
    int M = sizeof(Q) / sizeof(Q[0]);

    cout << countPairs(P, Q, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Number of pairs of lines
// having integer intersection points
class GFG
{

// Count number of pairs of lines
// having integer intersection point
static int countPairs(int []P, int []Q,
                      int N, int M)
{
    // Initialize arrays to store counts
    int []A = new int[2], B = new int[2];

    // Count number of odd and even Pi
    for (int i = 0; i < N; i++)
        A[P[i] % 2]++;

    // Count number of odd and even Qi
    for (int i = 0; i < M; i++)
        B[Q[i] % 2]++;

    // Return the count of pairs
    return (A[0] * B[0] + A[1] * B[1]);
}

// Driver code
public static void main(String[] args)
{
    int []P = { 1, 3, 2 };
    int []Q = { 3, 0 };
    int N = P.length;
    int M = Q.length;

    System.out.print(countPairs(P, Q, N, M));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to Number of pairs of lines
# having eger ersection pos

# Count number of pairs of lines
# having eger ersection po
def countPairs(P, Q, N, M):

    # Initialize arrays to store counts
    A = [0] * 2
    B = [0] * 2

    # Count number of odd and even Pi
    for i in range(N):
        A[P[i] % 2] += 1

    # Count number of odd and even Qi
    for i in range(M):
        B[Q[i] % 2] += 1

    # Return the count of pairs
    return (A[0] * B[0] + A[1] * B[1])

# Driver code

P = [1, 3, 2]
Q = [3, 0]
N = len(P)
M = len(Q)

print(countPairs(P, Q, N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to Number of pairs of lines
// having integer intersection points
using System;

class GFG
{

    // Count number of pairs of lines
    // having integer intersection point
    static int countPairs(int []P, int []Q,
                        int N, int M)
    {
        // Initialize arrays to store counts
        int []A = new int[2];
        int []B = new int[2];

        // Count number of odd and even Pi
        for (int i = 0; i < N; i++)
            A[P[i] % 2]++;

        // Count number of odd and even Qi
        for (int i = 0; i < M; i++)
            B[Q[i] % 2]++;

        // Return the count of pairs
        return (A[0] * B[0] + A[1] * B[1]);
    }

    // Driver code
    public static void Main()
    {
        int []P = { 1, 3, 2 };
        int []Q = { 3, 0 };
        int N = P.Length;
        int M = Q.Length;

        Console.Write(countPairs(P, Q, N, M));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to Number of
// pairs of lines having integer
// intersection points

// Count number of pairs of lines
// having integer intersection point
function countPairs(P, Q, N, M)
{

    // Initialize arrays to store counts
    var A = [0, 0], B = [0, 0];

    // Count number of odd and even Pi
    for(var i = 0; i < N; i++)
        A[P[i] % 2]++;

    // Count number of odd and even Qi
    for(var i = 0; i < M; i++)
        B[Q[i] % 2]++;

    // Return the count of pairs
    return(A[0] * B[0] + A[1] * B[1]);
}

// Driver code
var P = [ 1, 3, 2 ], Q = [ 3, 0 ];
var N = P.length;
var M = Q.length;

document.write(countPairs(P, Q, N, M));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(P + Q)