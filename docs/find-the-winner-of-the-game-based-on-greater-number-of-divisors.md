# 根据更大的除数找到游戏的赢家

> 原文:[https://www . geeksforgeeks . org/基于更大的除数找到游戏赢家/](https://www.geeksforgeeks.org/find-the-winner-of-the-game-based-on-greater-number-of-divisors/)

给定两个数组**arr 1【】**和**arr 2【】**，玩家 **A** 从**arr 1【】**中选取一个元素，玩家 **B** 从**arr 2【】**中选取一个元素，拥有除数较多元素的玩家获胜。如果两者都有相同除数的元素，那么玩家 **A** 将赢得该回合。任务是找出玩家 **A** 赢局概率更大还是玩家 **B** 赢局概率更大。

**示例:**

> **输入:** arr1[] = {4，12，24}，arr2[] = {25，28，13，45}
> **输出:**A
> A 赢的对子为(3，2)，(3，3)，(6，2)，(6，3)，(6，3)，(6，6)，(8，2)，(8，3)，(8，6)和(8，6)。
> 合计= 10。
> B 赢 2 例。
> 因此，A 赢得比赛的概率更大。
> 
> **输入:** arr1[] = {7，3，4}，arr2[] = {5，4，12，10 }
> T3】输出: B

**进场:**

*   对于这两个数组，存储元素的除数来代替元素。
*   [按照递增的顺序排序](https://www.geeksforgeeks.org/merge-sort/)两个数组。
*   找到所有可能的配对选择 **(X，Y)** ，其中 **A** 赢得比赛。
*   假设， **A** 从**arr 1【】**中选择一个元素。现在可以用二分搜索法来求**arr 2【】**中的元素个数，其除数小于**arr 1【】**中所选的元素。这将被添加到 **A** 获胜的配对数中。对 **arr1[]** 的每个元素都这样做。
*   **N * M** 是可能的总对。 **A** 获胜的对数表示 **X** ，而 **B** 获胜的对数表示 **Y** 。
    *   如果 **X > Y** 那么 **A** 赢得比赛的概率更大。
    *   如果 **Y > X** 那么 **B** 获胜的概率更大。
    *   如果 **X = Y** 那么平局的概率更大。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to return the count
// of divisors of elem
int divisorcount(int elem)
{
    int ans = 0;
    for (int i = 1; i <= sqrt(elem); i++) {
        if (elem % i == 0) {
            if (i * i == elem)
                ans++;
            else
                ans += 2;
        }
    }

    return ans;
}

// Function to return the winner of the game
string findwinner(int A[], int B[], int N, int M)
{
    // Convert every element of A[]
    // to their divisor count
    for (int i = 0; i < N; i++) {
        A[i] = divisorcount(A[i]);
    }

    // Convert every element of B[]
    // to their divisor count
    for (int i = 0; i < M; i++) {
        B[i] = divisorcount(B[i]);
    }

    // Sort both the arrays
    sort(A, A + N);
    sort(B, B + M);

    int winA = 0;
    for (int i = 0; i < N; i++) {
        int val = A[i];
        int start = 0;
        int end = M - 1;
        int index = -1;

        // For every element of A apply Binary Search
        // to find number of pairs where A wins
        while (start <= end) {
            int mid = (start + end) / 2;
            if (B[mid] <= val) {
                index = mid;
                start = mid + 1;
            }
            else {
                end = mid - 1;
            }
        }

        winA += (index + 1);
    }

    // B wins if A doesnot win
    int winB = N * M - winA;

    if (winA > winB) {
        return "A";
    }
    else if (winB > winA) {
        return "B";
    }

    return "Draw";
}

// Driver code
int main()
{
    int A[] = { 4, 12, 24 };
    int N = sizeof(A) / sizeof(A[0]);

    int B[] = { 25, 28, 13, 45 };
    int M = sizeof(B) / sizeof(B[0]);

    cout << findwinner(A, B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG{

// Function to return the count
// of divisors of elem
static int divisorcount(int elem)
{
  int ans = 0;
  for (int i = 1;
           i <= Math.sqrt(elem); i++)
  {
    if (elem % i == 0)
    {
      if (i * i == elem)
        ans++;
      else
        ans += 2;
    }
  }

  return ans;
}

// Function to return the
// winner of the game
static String findwinner(int A[], int B[],
                         int N, int M)
{
  // Convert every element of A[]
  // to their divisor count
  for (int i = 0; i < N; i++)
  {
    A[i] = divisorcount(A[i]);
  }

  // Convert every element of B[]
  // to their divisor count
  for (int i = 0; i < M; i++)
  {
    B[i] = divisorcount(B[i]);
  }

  // Sort both the arrays
  Arrays.sort(A);
  Arrays.sort(B);

  int winA = 0;
  for (int i = 0; i < N; i++)
  {
    int val = A[i];
    int start = 0;
    int end = M - 1;
    int index = -1;

    // For every element of A
    // apply Binary Search to
    // find number of pairs
    // where A wins
    while (start <= end)
    {
      int mid = (start +
                 end) / 2;
      if (B[mid] <= val)
      {
        index = mid;
        start = mid + 1;
      }
      else
      {
        end = mid - 1;
      }
    }

    winA += (index + 1);
  }

  // B wins if A doesnot
  // win
  int winB = N * M - winA;

  if (winA > winB)
  {
    return "A";
  }
  else if (winB > winA)
  {
    return "B";
  }

  return "Draw";
}

// Driver code
public static void main(String[] args)
{
  int A[] = {4, 12, 24};
  int N = A.length;

  int B[] = {25, 28, 13, 45};
  int M = B.length;

  System.out.print(findwinner(A, B, N, M));
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import *

# Function to return the count
# of divisors of elem
def divisorcount(elem):

    ans = 0
    for i in range(1, int(sqrt(elem)) + 1):
        if (elem % i == 0):
            if (i * i == elem):
                ans += 1
            else:
                ans += 2

    return ans

# Function to return the winner of the game
def findwinner(A, B, N, M):

    # Convert every element of A[]
    # to their divisor count
    for i in range(N):
        A[i] = divisorcount(A[i])

    # Convert every element of B[]
    # to their divisor count
    for i in range(M):
        B[i] = divisorcount(B[i])

    # Sort both the arrays
    A.sort()
    B.sort()

    winA = 0
    for i in range(N):
        val = A[i]
        start = 0
        end = M - 1
        index = -1

        # For every element of A[] apply
        # binary search to find number
        # of pairs where A wins
        while (start <= end):
            mid = (start + end) // 2

            if (B[mid] <= val):
                index = mid
                start = mid + 1

            else:
                end = mid - 1

        winA += (index + 1)

    # B wins if A doesnot win
    winB = N * M - winA

    if (winA > winB):
        return "A"
    elif (winB > winA):
        return "B"

    return "Draw"

# Driver code
if __name__ == '__main__':

    A = [ 4, 12, 24 ]
    N = len(A)

    B = [ 25, 28, 13, 45 ]
    M = len(B)

    print(findwinner(A, B, N, M))

# This code is contributed by himanshu77
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the count
// of divisors of elem
static int divisorcount(int elem)
{
    int ans = 0;
    for(int i = 1; i <= Math.Sqrt(elem); i++)
    {
        if (elem % i == 0)
        {
            if (i * i == elem)
                ans++;
            else
                ans += 2;
        }
    }
    return ans;
}

// Function to return the
// winner of the game
static string findwinner(int[] A, int[] B,
                         int N, int M)
{

    // Convert every element of A[]
    // to their divisor count
    for(int i = 0; i < N; i++)
    {
        A[i] = divisorcount(A[i]);
    }

    // Convert every element of B[]
    // to their divisor count
    for(int i = 0; i < M; i++)
    {
        B[i] = divisorcount(B[i]);
    }

    // Sort both the arrays
    Array.Sort(A);
    Array.Sort(B);

    int winA = 0;
    for(int i = 0; i < N; i++)
    {
        int val = A[i];
        int start = 0;
        int end = M - 1;
        int index = -1;

        // For every element of A
        // apply Binary Search to
        // find number of pairs
        // where A wins
        while (start <= end)
        {
            int mid = (start + end) / 2;
            if (B[mid] <= val)
            {
                index = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }
        winA += (index + 1);
    }

    // B wins if A doesnot
    // win
    int winB = N * M - winA;

    if (winA > winB)
    {
        return "A";
    }
    else if (winB > winA)
    {
        return "B";
    }
    return "Draw";
}

// Driver code
public static void Main()
{
    int[] A = { 4, 12, 24 };
    int N = A.Length;

    int[] B = { 25, 28, 13, 45 };
    int M = B.Length;

    Console.Write(findwinner(A, B, N, M));
}
}

// This code is contributed by rishavmahato348
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to return the count
// of divisors of elem
function divisorcount(elem)
{
    let ans = 0;
  for (let i = 1;
           i <= Math.sqrt(elem); i++)
  {
    if (elem % i == 0)
    {
      if (i * i == elem)
        ans++;
      else
        ans += 2;
    }
  }

  return ans;
}

// Function to return the
// winner of the game
function findwinner(A,B,N,M)
{
    // Convert every element of A[]
  // to their divisor count
  for (let i = 0; i < N; i++)
  {
    A[i] = divisorcount(A[i]);
  }

  // Convert every element of B[]
  // to their divisor count
  for (let i = 0; i < M; i++)
  {
    B[i] = divisorcount(B[i]);
  }

  // Sort both the arrays
  A.sort(function(a,b){return a-b;});
  B.sort(function(a,b){return a-b;});

  let winA = 0;
  for (let i = 0; i < N; i++)
  {
    let val = A[i];
    let start = 0;
    let end = M - 1;
    let index = -1;

    // For every element of A
    // apply Binary Search to
    // find number of pairs
    // where A wins
    while (start <= end)
    {
      let mid = Math.floor((start +
                 end) / 2);
      if (B[mid] <= val)
      {
        index = mid;
        start = mid + 1;
      }
      else
      {
        end = mid - 1;
      }
    }

    winA += (index + 1);
  }

  // B wins if A doesnot
  // win
  let winB = N * M - winA;

  if (winA > winB)
  {
    return "A";
  }
  else if (winB > winA)
  {
    return "B";
  }

  return "Draw";
}

// Driver code

let A=[4, 12, 24];
let N = A.length;

let B=[25, 28, 13, 45];
let M = B.length;
document.write(findwinner(A, B, N, M));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
A
```