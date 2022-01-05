# 从给定的 N 堆中从索引最少的非空堆中移除任意数量的石头的游戏中找到赢家

> 原文:[https://www . geeksforgeeks . org/从给定的 n 堆中找出从索引最少的非空堆中移除任意数量石头的游戏赢家/](https://www.geeksforgeeks.org/find-the-winner-of-a-game-of-removing-any-number-of-stones-from-the-least-indexed-non-empty-pile-from-given-n-piles/)

给定一个数组**arr【】**由 **N** 个整数组成，每个整数代表一堆石头的大小。任务是当两个玩家 **A** 和 **B** 按照以下条件进行最佳游戏时，确定游戏的赢家:

*   玩家 **A** 总是开始游戏。
*   在一次移动中，玩家可以从第一个非空堆中移除任意数量的石头(至少 1 个)，并且索引最小。
*   第一个不能移动的玩家输掉游戏。

如果玩家 A 赢了比赛，打印“**A”**。否则，打印“**B”**。

**示例:**

> **输入:** arr[] = {1，1，1，1，1，1}
> **输出:** B
> **说明:**
> 这里，每堆只有一块石头，所以 A 和 B 会交替各拿一块石头。
> 甲从第一堆中移除 1 块石头，乙从第二堆中移除 1 块石头，以此类推。
> 第 6 堆最后一块石头被 B 移除
> 由于 A 没得选，所以 B 赢了比赛。
> 
> **输入:** arr[] = {1，1，2，1}
> **输出:** A
> **解释:**
> 在这里，
> A 从第一堆中移除 1 块石头，
> B 从第二堆中移除 1 块石头，
> A 从第三堆中仅移除 1 块石头，
> 现在 B 被迫从第三堆中移除 1 块石头。
> 第 4 堆最后一块石头被 A 移除
> 由于 B 没有选择余地，所以 A 赢了比赛。

**方法:**想法是找出玩家赢得游戏应该遵循的最佳方式。以下是优化游戏的两种方法:

*   对于除最后一堆之外的所有堆，如果堆上有 **K** 个石头，那么当前玩家将只选择(**K–1**)个石头(仅当 K > 1)个，这样另一个玩家将被迫选择剩余的 **1** 个石头。这保证了当前玩家有机会从下一堆石头中挑选石头并最终获胜。
*   最后一堆，如果有 **K** 的石头，那么所有 **K** 的石头都会被当前玩家挑中，这样对方就没有机会挑石头了。这最终保证了当前玩家获胜。

按照以下步骤解决此问题:

1.  最初，假设玩家将移除当前堆中的所有石头，如果阵的大小为**奇数**则 **A** 将成为赢家，如果大小为**偶数**则 **B** 将成为赢家。
2.  现在，迭代范围**【0，N–2】**并检查当前指数和当前牌堆上出现的石头数量，以决定哪个玩家会赢。
3.  穿越的时候，如果指数是偶数，A 就有机会挑石头。否则 B 会有机会捡石头。
4.  如果当前指数为偶数且石子数大于 **1** ，则胜者被设置为 **B** 。将胜者更新为 **A** 。
5.  如果当前指数为奇数，且石子数超过 **1** ，则胜者被设置为 **A** 。然后，将胜者更新为 **B** 。
6.  最后，打印游戏的赢家。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the winner
// of game between A and B
void findWinner(int a[], int n)
{
    // win = 1 means B is winner
    // win = 0 means A is winner
    int win = 0;

    // If size is even, winner is B
    if (n % 2 == 0)
        win = 1;

    // If size is odd, winner is A
    else
        win = 0;

    for (int i = n - 2; i >= 0; i--) {

        // Stone will be removed by B
        if (i % 2 == 1) {

            // If B wants to win

            // B will take n-1 stones
            // from current pile having
            // n stones and force A to
            // pick 1 stone
            if (win == 0 && a[i] > 1)
                win = 1;
        }

        // Stone will be removed by A
        else {

            // If A wants to win

            // A will take n-1 stones from
            // current pile having n stones
            // and force B to pick 1 stone
            if (win == 1 && a[i] > 1)
                win = 0;
        }
    }

    // Print the winner accordingly
    if (win == 0)
        cout << "A";
    else
        cout << "B";
}

// Driver Code
int main()
{
    // Given piles of stone
    int arr[] = { 1, 1, 1, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findWinner(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the winner
// of game between A and B
static void findWinner(int a[], int n)
{

    // win = 1 means B is winner
    // win = 0 means A is winner
    int win = 0;

    // If size is even, winner is B
    if (n % 2 == 0)
        win = 1;

    // If size is odd, winner is A
    else
        win = 0;

    for(int i = n - 2; i >= 0; i--)
    {

        // Stone will be removed by B
        if (i % 2 == 1)
        {

            // If B wants to win

            // B will take n-1 stones
            // from current pile having
            // n stones and force A to
            // pick 1 stone
            if (win == 0 && a[i] > 1)
                win = 1;
        }

        // Stone will be removed by A
        else
        {

            // If A wants to win

            // A will take n-1 stones from
            // current pile having n stones
            // and force B to pick 1 stone
            if (win == 1 && a[i] > 1)
                win = 0;
        }
    }

    // Print the winner accordingly
    if (win == 0)
        System.out.print("A");
    else
        System.out.print("B");
}

// Driver Code
public static void main(String[] args)
{

    // Given piles of stone
    int arr[] = { 1, 1, 1, 2 };

    int N = arr.length;

    // Function call
    findWinner(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the winner
# of game between A and B
def findWinner(a, n):

    # win = 1 means B is winner
    # win = 0 means A is winner
    win = 0

    # If size is even, winner is B
    if (n % 2 == 0):
        win = 1

    # If size is odd, winner is A
    else:
        win = 0

    for i in range(n - 2, -1, -1):

        # Stone will be removed by B
        if (i % 2 == 1):

            # If B wants to win

            # B will take n-1 stones
            # from current pile having
            # n stones and force A to
            # pick 1 stone
            if (win == 0 and a[i] > 1):
                win = 1

        # Stone will be removed by A
        else:

            # If A wants to win

            # A will take n-1 stones from
            # current pile having n stones
            # and force B to pick 1 stone
            if (win == 1 and a[i] > 1):
                win = 0

    # Print the winner accordingly
    if (win == 0):
        print("A")
    else:
        print("B")

# Driver Code
if __name__ == '__main__':

    # Given piles of stone
    arr = [ 1, 1, 1, 2 ]

    N = len(arr)

    # Function call
    findWinner(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the winner
// of game between A and B
static void findWinner(int []a,
                       int n)
{   
  // win = 1 means B is winner
  // win = 0 means A is winner
  int win = 0;

  // If size is even, winner is B
  if (n % 2 == 0)
    win = 1;

  // If size is odd, winner is A
  else
    win = 0;

  for(int i = n - 2; i >= 0; i--)
  {
    // Stone will be removed by B
    if (i % 2 == 1)
    {

      // If B wants to win

      // B will take n-1 stones
      // from current pile having
      // n stones and force A to
      // pick 1 stone
      if (win == 0 && a[i] > 1)
        win = 1;
    }

    // Stone will be removed by A
    else
    {
      // If A wants to win
      // A will take n-1 stones from
      // current pile having n stones
      // and force B to pick 1 stone
      if (win == 1 && a[i] > 1)
        win = 0;
    }
  }

  // Print the winner accordingly
  if (win == 0)
    Console.Write("A");
  else
    Console.Write("B");
}

// Driver Code
public static void Main(String[] args)
{
  // Given piles of stone
  int []arr = {1, 1, 1, 2};

  int N = arr.Length;

  // Function call
  findWinner(arr, N);
}
}

 // This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the winner
// of game between A and B
function findWinner(a, n)
{

    // win = 1 means B is winner
    // win = 0 means A is winner
    let win = 0;

    // If size is even, winner is B
    if (n % 2 == 0)
        win = 1;

    // If size is odd, winner is A
    else
        win = 0;

    for(let i = n - 2; i >= 0; i--)
    {

        // Stone will be removed by B
        if (i % 2 == 1)
        {

            // If B wants to win

            // B will take n-1 stones
            // from current pile having
            // n stones and force A to
            // pick 1 stone
            if (win == 0 && a[i] > 1)
                win = 1;
        }

        // Stone will be removed by A
        else
        {

            // If A wants to win

            // A will take n-1 stones from
            // current pile having n stones
            // and force B to pick 1 stone
            if (win == 1 && a[i] > 1)
                win = 0;
        }
    }

    // Print the winner accordingly
    if (win == 0)
        document.write("A");
    else
        document.write("B");
}

// Driver Code
// Given piles of stone
let arr=[1, 1, 1, 2];
let N = arr.length;

// Function call
findWinner(arr, N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
B
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*