# 通过从给定的二进制数组中选择一个或两个连续的数组元素，玩家可以获得的最小分数

> 原文:[https://www . geesforgeks . org/玩家通过从给定的二进制数组中选择一个或两个连续的数组元素来获得最小可能分数/](https://www.geeksforgeeks.org/minimum-score-possible-for-a-player-by-selecting-one-or-two-consecutive-array-elements-from-given-binary-array/)

给定一个二进制[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】大小 **N** 和两个玩家 **A** 和 **B** 。任务是通过根据给定的约束选择玩家的分数来最小化玩家的分数 **A** :

*   每个玩家可以依次从数组中移除一个或两个连续的数字，元素按从左到右的顺序移除。
*   玩家将有交替的回合，从玩家 **A** 开始。
*   最初的惩罚是 **0** 并且数字递增，玩家 **A** 移除。

**示例:**

> **输入:** arr[] = {1，1，1，1，0，0，1}
> **输出:** 2
> **说明:**元素可以移除如下:
> 回合 1:玩家 A 移除索引 0 处的元素。因此，惩罚是 0 + 1 = 1。
> 回合 2:玩家 B 移除指数 1 和 2 的元素。尽管如此，惩罚是 1。
> 回合 3:玩家 A 移除索引 3 处的元素。所以，罚 1 + 1 = 2。
> 回合 4:玩家 B 移除索引 4 处的元素。不过，处罚是 2。
> 回合 5:玩家 A 移除索引 5 处的元素。不过，惩罚是 2 + 0 = 2。
> 回合 6:玩家 B 移除索引 6 处的元素。不过，处罚是 2。
> 因此，玩家 A 的最低分数= 2。
> 
> **输入:** arr[] = {1，0，1，1，0，1，1}
> **输出:** 2
> **说明:**元素可以移除如下:
> 回合 1:玩家 A 移除指数 0 和 1 的元素。因此，惩罚是 0 + 1 + 0 = 1。
> 回合 2:玩家 B 移除指数 2 和 3 的元素。尽管如此，惩罚是 1。
> 回合 3:玩家 A 移除索引 4 处的元素。所以，罚 1 + 0 = 1。
> 第四回合:玩家 B 移除索引 5 和 6 的元素。尽管如此，惩罚是 1。
> 回合 5:玩家 A 移除索引 7 处的元素。所以，罚 2 + 1 = 2。
> 因此，玩家 A 的最低分数= 2。

**天真方法:**最简单的方法是尝试所有可能的组合，从给定数组中移除元素。每次都有两个可能的选项，即可以删除一个或两个连续的元素。每个位置，从 **1** 到**N–1**，都有 **2** 的选择。因此，可以进行 **2 <sup>N</sup>** 的可能组合。每个组合的处罚可以找到，其中，打印最低处罚。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。可以通过以下 **dp** 转换来解决，其中**DP【I】【0】**存储从 **i** 到**N–1**的最小惩罚。如果玩家 **A** 从索引 **i** 开始选择。同样，可以为玩家 **B** 定义 **dp[i][1]** 。

> 轮到玩家 A 时:
> **dp[i][0] = min(dp(i+1，1)+arr[i]，dp(i+2，1)+arr[i+1]+arr[i+2])**
> 其中，
> i 表示当前位置。
> 1 表示下一个状态是 B 的开启。
> 
> 轮到玩家 B 时:
> **dp[i][1] = min(dp(i+1，0)，dp(i+2，0))**
> 其中，
> i 表示当前位置。
> 0 表示是 A 的下一个接通状态。

按照以下步骤解决问题:

*   [带记忆的递归](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)可以使用。对于基础条件，检查当前位置是否超过或变成 **N** ，返回 **0**
*   根据玩家的回合应用上面定义的转场，并返回最小答案。
*   用**玩家 A 的**回合和惩罚初始化递归函数为 **0** 。
*   对于每个递归调用，将计算出的最小惩罚存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中，以避免为[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)计算。
*   在上述递归调用结束后，打印玩家 **A** 的**最低分数**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the minimum score for each
// states as map<pair<pos, myturn>, ans>
map<pair<int, int>, int> m;

// Function to find the minimum score
// after choosing element from array
int findMinimum(int a[], int n, int pos,
                int myturn)
{
    // Return the stored state
    if (m.find({ pos, myturn }) != m.end()) {
        return m[{ pos, myturn }];
    }

    // Base Case
    if (pos >= n) {
        return 0;
    }

    // Player A's turn
    if (!myturn) {

        // Find the minimum score
        int ans = min(
            findMinimum(a, n, pos + 1, !myturn)
                + a[pos],
            findMinimum(a, n, pos + 2, !myturn)
                + a[pos] + a[pos + 1]);

        // Store the current state
        m[{ pos, myturn }] = ans;

        // Return the result
        return ans;
    }

    // Player B's turn
    if (myturn) {

        // Find minimum score
        int ans = min(
            findMinimum(a, n, pos + 1, !myturn),
            findMinimum(a, n, pos + 2, !myturn));

        // Store the current state
        m[{ pos, myturn }] = ans;

        // Return the result
        return ans;
    }
    return 0;
}

// Function that finds the minimum
// penality after choosing element
// from the given binary array
int countPenality(int arr[], int N)
{
    // Starting position of choosing
    // element from array
    int pos = 0;

    // 0 denotes player A turn
    // 1 denotes player B turn
    int turn = 0;

    // Function Call
    return findMinimum(arr, N, pos, turn);
}

// Print the answer for player A and B
void printAnswer(int* arr, int N)
{

    // Minimum penalty
    int a = countPenality(arr, N);

    // Calculate sum of all arr elements
    int sum = 0;
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // Print the minimum score
    cout << a;
}
// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 0, 1, 1, 0, 1, 1, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printAnswer(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

static class R
{
    int x, y;

    public R(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Stores the minimum score for each
// states as map<pair<pos, myturn>, ans>
static HashMap<R, Integer> m = new HashMap<>();

// Function to find the minimum score
// after choosing element from array
public static int findMinimum(int[] arr, int N,
                              int pos, int turn)
{

    // Return the stored state
    R x = new R(pos, turn);

    if (m.containsKey(x))
    {
        return m.get(x);
    }

    // Base Case
    if (pos >= N - 1)
    {
        return 0;
    }

    // Player A's turn
    if (turn == 0)
    {

        // Find the minimum score
        int ans = Math.min(
            findMinimum(arr, N, pos + 1, 1) + arr[pos],
            findMinimum(arr, N, pos + 2, 1) + arr[pos] +
                            arr[pos + 1]);

        // Store the current state
        R v = new R(pos, turn);
        m.put(v, ans);

        // Return the result
        return ans;
    }

    // Player B's turn
    if (turn != 0)
    {

        // Find minimum score
        int ans = Math.min(
            findMinimum(arr, N, pos + 1, 0),
            findMinimum(arr, N, pos + 2, 0));

        // Store the current state
        R v = new R(pos, turn);
        m.put(v, ans);

        // Return the result
        return ans;
    }
    return 0;
}

// Function that finds the minimum
// penality after choosing element
// from the given binary array
public static int countPenality(int[] arr, int N)
{

    // Starting position of choosing
    // element from array
    int pos = 0;

    // 0 denotes player A turn
    // 1 denotes player B turn
    int turn = 0;

    // Function Call
    return findMinimum(arr, N, pos, turn) + 1;
}

// Function to print the answer
public static void printAnswer(int[] arr, int N)
{

    // Minimum penalty
    int a = countPenality(arr, N);

    // Calculate sum of all arr elements
    int sum = 0;
    for(int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Print the minimum score
    System.out.println(a);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 1, 1, 0, 1, 1, 1 };
    int N = 8;

    // Function Call
    printAnswer(arr, N);
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the minimum score for each
# states as map<pair<pos, myturn>, ans>
m = dict()

# Function to find the minimum score
# after choosing element from array
def findMinimum(a, n, pos, myturn):

    # Return the stored state
    if (pos, myturn) in m:
        return m[( pos, myturn )];

    # Base Case
    if (pos >= n - 1):
        return 0;

    # Player A's turn
    if (not myturn):

        # Find the minimum score
        ans = min( findMinimum(a, n, pos + 1, not myturn) + a[pos],
                     findMinimum(a, n, pos + 2, not myturn) + a[pos] + a[pos + 1]);

        # Store the current state
        m[( pos, myturn )] = ans;

        # Return the result
        return ans;

    # Player B's turn
    if (myturn):

        # Find minimum score
        ans = min( findMinimum(a, n, pos + 1, not myturn),
                    findMinimum(a, n, pos + 2, not myturn));

        # Store the current state
        m[( pos, myturn )] = ans;

        # Return the result
        return ans;

    return 0;

# Function that finds the minimum
# penality after choosing element
# from the given binary array
def countPenality(arr, N):

    # Starting position of choosing
    # element from array
    pos = 0;

    # 0 denotes player A turn
    # 1 denotes player B turn
    turn = False;

    # Function Call
    return findMinimum(arr, N, pos, turn) + 1;

# Print the answer for player A and B
def printAnswer(arr, N):

    # Minimum penalty
    a = countPenality(arr, N);

    # Calculate sum of all arr elements
    sum = 0;

    for i in range(N):

        sum += arr[i];

    # Print the minimum score
    print(a)

# Driver Code
if __name__=='__main__':

    # Given array arr[]
    arr = [ 1, 0, 1, 1, 0, 1, 1, 1 ]

    N = len(arr)

    # Function Call
    printAnswer(arr, N);

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Stores the minimum score for each
    // states as map<pair<pos, myturn>, ans>
    static Dictionary<Tuple<int,int>, int> m = new Dictionary<Tuple<int,int>, int>();

    // Function to find the minimum score
    // after choosing element from array
    static int findMinimum(int[] arr, int N, int pos, int turn)
    {

        // Return the stored state
        Tuple<int,int> x = new Tuple<int,int>(pos, turn);

        if (m.ContainsKey(x))
        {
            return m[x];
        }

        // Base Case
        if (pos >= N - 1)
        {
            return 0;
        }

        // Player A's turn
        if (turn == 0)
        {

            // Find the minimum score
            int ans = Math.Min(
                findMinimum(arr, N, pos + 1, 1) + arr[pos],
                findMinimum(arr, N, pos + 2, 1) + arr[pos] +
                                arr[pos + 1]);

            // Store the current state
            Tuple<int,int> v = new Tuple<int,int>(pos, turn);
            m[v] = ans;

            // Return the result
            return ans;
        }

        // Player B's turn
        if (turn != 0)
        {

            // Find minimum score
            int ans = Math.Min(
                findMinimum(arr, N, pos + 1, 0),
                findMinimum(arr, N, pos + 2, 0));

            // Store the current state
            Tuple<int,int> v = new Tuple<int,int>(pos, turn);
            m[v] = ans;

            // Return the result
            return ans;
        }
        return 0;
    }

    // Function that finds the minimum
    // penality after choosing element
    // from the given binary array
    static int countPenality(int[] arr, int N)
    {

        // Starting position of choosing
        // element from array
        int pos = 0;

        // 0 denotes player A turn
        // 1 denotes player B turn
        int turn = 0;

        // Function Call
        return findMinimum(arr, N, pos, turn) + 1;
    }

    // Function to print the answer
    static void printAnswer(int[] arr, int N)
    {

        // Minimum penalty
        int a = countPenality(arr, N);

        // Calculate sum of all arr elements
        int sum = 0;
        for(int i = 0; i < N; i++)
        {
            sum += arr[i];
        }

        // Print the minimum score
        Console.WriteLine(a);
    }

  static void Main() {
    int[] arr = { 1, 0, 1, 1, 0, 1, 1, 1 };
    int N = 8;

    // Function Call
    printAnswer(arr, N);
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Stores the minimum score for each
    // states as map<pair<pos, myturn>, ans>
    let m = new Map();

    // Function to find the minimum score
    // after choosing element from array
    function findMinimum(arr, N, pos, turn)
    {

        // Return the stored state
        let x = [pos, turn];

        if (m.has(x))
        {
            return m[x];
        }

        // Base Case
        if (pos >= N - 1)
        {
            return 0;
        }

        // Player A's turn
        if (turn == 0)
        {

            // Find the minimum score
            let ans = Math.min(
                findMinimum(arr, N, pos + 1, 1) + arr[pos],
                findMinimum(arr, N, pos + 2, 1) + arr[pos] +
                                arr[pos + 1]);

            // Store the current state
            let v = [pos, turn];
            m[v] = ans;

            // Return the result
            return ans;
        }

        // Player B's turn
        if (turn != 0)
        {

            // Find minimum score
            let ans = Math.min(
                findMinimum(arr, N, pos + 1, 0),
                findMinimum(arr, N, pos + 2, 0));

            // Store the current state
            let v = [pos, turn];
            m[v] = ans;

            // Return the result
            return ans;
        }
        return 0;
    }

    // Function that finds the minimum
    // penality after choosing element
    // from the given binary array
    function countPenality(arr, N)
    {

        // Starting position of choosing
        // element from array
        let pos = 0;

        // 0 denotes player A turn
        // 1 denotes player B turn
        let turn = 0;

        // Function Call
        return findMinimum(arr, N, pos, turn) + 1;
    }

    // Function to print the answer
    function printAnswer(arr, N)
    {

        // Minimum penalty
        let a = countPenality(arr, N);

        // Calculate sum of all arr elements
        let sum = 0;
        for(let i = 0; i < N; i++)
        {
            sum += arr[i];
        }

        // Print the minimum score
        document.write(a);
    }

    let arr = [ 1, 0, 1, 1, 0, 1, 1, 1 ];
    let N = 8;

    // Function Call
    printAnswer(arr, N);

 // This code is contributed by suresh07
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)