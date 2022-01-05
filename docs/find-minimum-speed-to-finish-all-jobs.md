# 找到完成所有作业的最小速度

> 原文:[https://www . geesforgeks . org/find-完成所有作业的最小速度/](https://www.geeksforgeeks.org/find-minimum-speed-to-finish-all-jobs/)

给定一个数组 **A** 和一个整数 **H** 其中![1\leq A[i] \leq 10^{9}  ](img/dd784586d96b11f427182f75ea3336e8.png "Rendered by QuickLaTeX.com")和![len(A) \leq H \leq 10^{9}  ](img/cf49e97d87f09da0bdba13cf53a2acfc.png "Rendered by QuickLaTeX.com")。每个元素**A【I】**代表剩余的待完成的未完成工作， **H** 代表完成所有工作的剩余**小时数。任务是找到每小时工作的最小速度，在此速度下，人需要在 **H** 小时内完成所有工作。
**注意:**如果 **A[i]** 要做的工作比**人的速度**少，那么他就完成了 A[i]的所有工作，在这一小时内不会去下一个元素。
**例** :** 

```
Input: A[] = [3, 6, 7, 11], H = 8
Output: 4

Input: A[] = [30, 11, 23, 4, 20], H = 5
Output: 30
```

**接近:**如果一个人能以 **K** 作业/小时的速度完成所有作业(在 **H** 小时内)，那么他也能以更大的速度完成所有作业。
如果我们让**为可能(K)** 为**真**当且仅当此人能以 **K** 的工作速度完成工作，那么就有一些 **X** 使得**为可能(K) =真**当且仅当 **K > = X** 。
比如**A =【3，6，7，11】**和 **H = 8** 有一些 **X = 4** 这样**是可能的(1) =是可能的(2) =是可能的(3) =假的，是可能的(4) =是可能的(5) = … =真的**。
我们可以做一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)关于**的值是可能的(K)** 找到第一个 **X** 这样**是可能的(X)就是真的**这将是我们的答案。
现在，由于即使作业完成也不允许在当前小时内从一个元素移动到另一个元素，因此 K 的最大可能值可以是数组 A[]中的最大元素。所以，要求**的值是可能的(K)** (即作业速度为 **K** 的人能否在 **H** 小时内完成所有作业)，做范围内的二分搜索法(1，max_element_of_array)。
同样，对于每一个 **A[i]** 的作业> 0，我们可以推导出此人在 **Math.ceil(A[i] / K)** 或 **((A[i]-1) / K) + 1** 小时内完成它，我们将这些对所有元素进行相加，找出完成所有作业的总时间，并与 H 进行比较，以检查是否有可能以 K 个作业/小时的速度完成所有作业。
以下是上述方法的实施:

## C++

```
// CPP program to find minimum speed
// to finish all jobs

#include <bits/stdc++.h>
using namespace std;

// Function to check if the person can do
// all jobs in H hours with speed K
bool isPossible(int A[], int n, int H, int K)
{
    int time = 0;

    for (int i = 0; i < n; ++i)
        time += (A[i] - 1) / K + 1;

    return time <= H;
}

// Function to return the minimum speed
// of person to complete all jobs
int minJobSpeed(int A[], int n, int H)
{
    // If H < N it is not possible to complete
    // all jobs as person can not move from
    // one element to another during current hour
    if (H < n)
        return -1;

    // Max element of array
    int* max = max_element(A, A + n);

    int lo = 1, hi = *max;

    // Use binary search to find smallest K
    while (lo < hi) {
        int mi = lo + (hi - lo) / 2;
        if (!isPossible(A, n, H, mi))
            lo = mi + 1;
        else
            hi = mi;
    }

    return lo;
}

// Driver program
int main()
{
    int A[] = { 3, 6, 7, 11 }, H = 8;

    int n = sizeof(A) / sizeof(A[0]);

    // Print required maxLenwer
    cout << minJobSpeed(A, n, H);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum speed
// to finish all jobs
class GFG
{

// Function To findmax value in Array
static int findmax(int[] A)
{
    int r = A[0];
    for(int i = 1; i < A.length; i++)
    r = Math.max(r, A[i]);
    return r;
}

// Function to check if the person can do
// all jobs in H hours with speed K
static boolean isPossible(int[] A, int n,
                          int H, int K)
{
    int time = 0;

    for (int i = 0; i < n; ++i)
        time += (A[i] - 1) / K + 1;

    return time <= H;
}

// Function to return the minimum speed
// of person to complete all jobs
static int minJobSpeed(int[] A,
                       int n, int H)
{
    // If H < N it is not possible to
    // complete all jobs as person can
    // not move from one element to
    // another during current hour
    if (H < n)
        return -1;

    // Max element of array
    int max = findmax(A);

    int lo = 1, hi = max;

    // Use binary search to find
    // smallest K
    while (lo < hi)
    {
        int mi = lo + (hi - lo) / 2;
        if (!isPossible(A, n, H, mi))
            lo = mi + 1;
        else
            hi = mi;
    }

    return lo;
}

// Driver Code
public static void main(String[] args)
{
    int[] A = { 3, 6, 7, 11 };
    int H = 8;

    int n = A.length;

    // Print required maxLenwer
    System.out.println(minJobSpeed(A, n, H));
}
}

// This code is contributed by mits
```

## C#

```
// C# program to find minimum speed
// to finish all jobs

using System;
using System.Linq;

class GFG{

// Function to check if the person can do
// all jobs in H hours with speed K
static bool isPossible(int[] A, int n, int H, int K)
{
    int time = 0;

    for (int i = 0; i < n; ++i)
        time += (A[i] - 1) / K + 1;

    return time <= H;
}

// Function to return the minimum speed
// of person to complete all jobs
static int minJobSpeed(int[] A, int n, int H)
{
    // If H < N it is not possible to complete
    // all jobs as person can not move from
    // one element to another during current hour
    if (H < n)
        return -1;

    // Max element of array
    int max = A.Max();

    int lo = 1, hi = max;

    // Use binary search to find smallest K
    while (lo < hi) {
        int mi = lo + (hi - lo) / 2;
        if (!isPossible(A, n, H, mi))
            lo = mi + 1;
        else
            hi = mi;
    }

    return lo;
}

// Driver program
public static void Main()
{
    int[] A = { 3, 6, 7, 11 };
    int H = 8;

    int n = A.Length;

    // Print required maxLenwer
    Console.WriteLine(minJobSpeed(A, n, H));
}
}
```

## 蟒蛇 3

```
# Python3 program to find minimum
# speed to finish all jobs

# Function to check if the person can do
# all jobs in H hours with speed K
def isPossible(A, n, H, K):

    time = 0

    for i in range(n):
        time += (A[i] - 1) // K + 1

    return time <= H

# Function to return the minimum speed
# of person to complete all jobs
def minJobSpeed(A, n, H):

    # If H < N it is not possible to complete
    # all jobs as person can not move from
    # one element to another during current hour
    if H < n:
        return -1

    # Max element of array
    Max = max(A)

    lo, hi = 1, Max

    # Use binary search to find smallest K
    while lo < hi: 
        mi = lo + (hi - lo) // 2
        if not isPossible(A, n, H, mi):
            lo = mi + 1
        else:
            hi = mi

    return lo

if __name__ == "__main__": 

    A =  [3, 6, 7, 11]
    H = 8

    n = len(A)

    # Print required maxLenwer
    print(minJobSpeed(A, n, H))

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>

// Javascript program to find minimum speed
// to finish all jobs

// Function to check if the person can do
// all jobs in H hours with speed K
function isPossible(A, n, H, K)
{
    var time = 0;

    for (var i = 0; i < n; ++i)
        time += parseInt((A[i] - 1) / K) + 1;

    return time <= H;
}

// Function to return the minimum speed
// of person to complete all jobs
function minJobSpeed(A, n, H)
{
    // If H < N it is not possible to complete
    // all jobs as person can not move from
    // one element to another during current hour
    if (H < n)
        return -1;

    // Max element of array
    var max = A.reduce((a,b)=> Math.max(a,b));

    var lo = 1, hi = max;

    // Use binary search to find smallest K
    while (lo < hi) {
        var mi = lo + parseInt((hi - lo) / 2);
        if (!isPossible(A, n, H, mi))
            lo = mi + 1;
        else
            hi = mi;
    }

    return lo;
}

// Driver program
var A = [3, 6, 7, 11], H = 8;
var n = A.length;

// Print required maxLenwer
document.write( minJobSpeed(A, n, H));

// This code is contributed by famously.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N*log(M))，其中 N 为数组长度，M 为 max(A)。