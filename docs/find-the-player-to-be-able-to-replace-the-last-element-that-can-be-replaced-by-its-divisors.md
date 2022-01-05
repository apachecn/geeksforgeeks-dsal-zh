# 找到能够替换其除数

可以替换的最后一个元素的玩家

> 原文:[https://www . geesforgeks . org/find-the-player-to-be-to-replace-the-the-player-to-the-the-player-to-the-to-the-player-to-the-to-the-to-the-player-to-the-to-the-the-to-the-the-the-the-the-the-the-the-the](https://www.geeksforgeeks.org/find-the-player-to-be-able-to-replace-the-last-element-that-can-be-replaced-by-its-divisors/)

给定一个由 **N** 个整数和两个玩家 **A** 和 **B** 组成的[阵](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**通过执行以下操作一起玩游戏:

*   从 **arr[]** 中选择一个整数，并用它的一个除数替换该数。
*   不能再次选择以前选择的整数。
*   由于 1 除了自身之外没有任何除数，玩家不能用任何其他数字代替 1。因此，当阵列仅由 **1** 组成时，不能移动的玩家输掉游戏。
*   两个玩家都将以最佳状态进行游戏，然后 **A** 开始游戏的第一步。

任务是找到游戏的赢家。

**示例:**

> **输入:** arr[] = {24，45，45，24}
> **输出:** B
> **说明:**
> 玩家 **A** 将第一个索引中的 24 替换为 1。因为，1 是 24 的除数。arr[] = {1，45，45，24}
> Player **B** 将最后一个索引中的 24 替换为 1。因为，1 是 24 的除数。arr[] = {1，45，45，1}
> Player **A** 将第二个索引中的 45 替换为 1。因为，1 是 45 的除数。arr[] = {1，1，45，24}
> Player **B** 将第三个索引中的 45 替换为 1。因为，1 是 45 的除数。arr[] = {1，1，1，1}
> 玩家 **A** 现在不能移动，因为所有元素都是 1。因此，玩家 B 赢得游戏。
> 
> **输入:** arr[] = {18，6 }
> T3】输出: B

**方法:**问题可以通过简单的观察来解决:

*   由于 1 是所有整数的除数，因此，在每个操作中，用 1 替换每个数组元素。
*   因此，如果数组由偶数个元素组成，那么玩家 B 获胜。
*   否则，玩家 A 获胜。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner
// of the game played based on
// given conditions
void winner(int arr[], int N)
{

    // A wins if size of array is odd
    if (N % 2 == 1) {
        cout << "A";
    }

    // Otherwise, B wins
    else {
        cout << "B";
    }
}

// Driver Code
int main()
{
    // Input array
    int arr[] = { 24, 45, 45, 24 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    winner(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the winner
// of the game played based on
// given conditions
static void winner(int arr[], int N)
{

    // A wins if size of array is odd
    if (N % 2 == 1)
    {
        System.out.print("A");
    }

    // Otherwise, B wins
    else
    {
        System.out.print("B");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input array
    int arr[] = { 24, 45, 45, 24 };

    // Size of the array
    int N = arr.length;

    winner(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the winner
# of the game played based on
# given conditions
def winner(arr, N):

    # A wins if size of array is odd
    if (N % 2 == 1):
        print ("A")

    # Otherwise, B wins
    else:
        print ("B")

# Driver Code
if __name__ == '__main__':

    # Input array
    arr = [24, 45, 45, 24]

    # Size of the array
    N = len(arr)
    winner(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to find the winner
// of the game played based on
// given conditions
static void winner(int []arr, int N)
{

    // A wins if size of array is odd
    if (N % 2 == 1)
    {
        Console.Write("A");
    }

    // Otherwise, B wins
    else
    {
        Console.Write("B");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Input array
    int []arr = { 24, 45, 45, 24 };

    // Size of the array
    int N = arr.Length;

    winner(arr, N);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the winner
      // of the game played based on
      // given conditions
      function winner(arr, N) {
        // A wins if size of array is odd
        if (N % 2 === 1) {
          document.write("A");
        }

        // Otherwise, B wins
        else {
          document.write("B");
        }
      }

      // Driver Code
      // Input array
      var arr = [24, 45, 45, 24];

      // Size of the array
      var N = arr.length;
      winner(arr, N);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
B
```

***时间复杂度:*** O(N)，其中 N 为阵的大小。
***辅助空间*** : O(1)