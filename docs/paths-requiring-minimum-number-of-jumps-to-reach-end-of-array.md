# 到达数组末尾需要最小跳跃次数的路径

> 原文:[https://www . geesforgeks . org/path-需要最小数量的跳转才能到达阵列末端/](https://www.geeksforgeeks.org/paths-requiring-minimum-number-of-jumps-to-reach-end-of-array/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]，**，其中每个元素代表从该元素向前的最大步数，任务是打印所有可能的路径，这些路径需要[最小跳数才能从第一个数组元素开始到达给定数组的末尾](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/)。

**注意:**如果一个元素为 0，则该元素不允许移动。

**示例:**

> **输入:** arr[] = {1，1，1，1，1}
> **输出:**
> 0**⇾**1**⇾**2**⇾**3**⇾**4
> t15】说明:
> 每一步只允许跳一次。
> 因此，只有一条可能的路径可以到达阵列的末端。
> 
> **输入:**arr[]=【3，3，0，2，1，2，4，2，0，0】
> **输出:**
> 【0】****【5】****

****方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。按照以下步骤解决问题:**

*   **初始化一个大小为 **N** 的数组 **dp[]** ，其中 **dp[i]** 存储从索引 ***i*** 到达数组末尾**arr【N–1】**所需的最小跳转次数**
*   **通过迭代索引**N–2**到 **1** ，计算每个索引到达数组末尾所需的最小步数。对于每个索引，尝试可以从该索引中采取的所有可能步骤，即 **[1，arr[i]]** 。**
*   **当通过迭代**【1，arr[I]】**来尝试所有可能的步骤时，对于每个索引，更新并存储 **dp[i + j]** 的最小值。**
*   **初始化 [Pair 类](https://www.geeksforgeeks.org/pair-class-in-java/)实例的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，该队列存储当前位置的索引和到达该索引所经过的路径。**
*   **不断更新所需的最小步数，最后，打印与所需步数相对应的路径。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Pair Struct
struct Pair
{

    // Stores the current index
    int idx;

    // Stores the path
    // travelled so far
    string psf;

    // Stores the minimum jumps
    // required to reach the
    // last index from current index
    int jmps;
};

// Minimum jumps required to reach
// end of the array
void minJumps(int arr[], int dp[], int n)
{
    for(int i = 0; i < n; i++)
        dp[i] = INT_MAX;

    dp[n - 1] = 0;

    for(int i = n - 2; i >= 0; i--)
    {

        // Stores the maximum number
        // of steps that can be taken
        // from the current index
        int steps = arr[i];
        int min = INT_MAX;

        for(int j = 1;
                j <= steps && i + j < n;
                j++)
        {

            // Checking if index stays
            // within bounds
            if (dp[i + j] != INT_MAX &&
                dp[i + j] < min)
            {

                // Stores the minimum
                // number of jumps
                // required to jump
                // from (i + j)-th index
                min = dp[i + j];
            }
        }

        if (min != INT_MAX)
            dp[i] = min + 1;
    }
}

// Function to find all possible
// paths to reach end of array
// requiring minimum number of steps
void possiblePath(int arr[], int dp[], int n)
{
    queue<Pair> Queue;
    Pair p1 = { 0, "0", dp[0] };
    Queue.push(p1);

    while (Queue.size() > 0)
    {
        Pair tmp = Queue.front();
        Queue.pop();

        if (tmp.jmps == 0)
        {
            cout << tmp.psf << "\n";
            continue;
        }

        for(int step = 1;
                step <= arr[tmp.idx];
                step++)
        {
            if (tmp.idx + step < n &&
                tmp.jmps - 1 == dp[tmp.idx + step])
            {

                // Storing the neighbours
                // of current index element
                string s1 = tmp.psf + " -> " +
                 to_string((tmp.idx + step));

                Pair p2 = { tmp.idx + step, s1,
                           tmp.jmps - 1 };

                Queue.push(p2);
            }
        }
    }
}

// Function to find the minimum steps
// and corresponding paths to reach
// end of an array
void Solution(int arr[], int dp[], int size)
{

    // dp[] array stores the minimum jumps
    // from each position to last position
    minJumps(arr, dp, size);

    possiblePath(arr, dp, size);
}

// Driver Code
int main()
{
    int arr[] = { 3, 3, 0, 2, 1,
                  2, 4, 2, 0, 0 };

    int size = sizeof(arr) / sizeof(arr[0]);
    int dp[size];

    Solution(arr, dp, size);
}

// This code is contributed by akhilsaini
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement the
// above approach

import java.util.*;
class GFG {

    // Pair Class instance
    public static class Pair {
        // Stores the current index
        int idx;

        // Stores the path
        // travelled so far
        String psf;

        // Stores the minimum jumps
        // required to reach the
        // last index from current index
        int jmps;

        // Constructor
        Pair(int idx, String psf, int jmps)
        {
            this.idx = idx;
            this.psf = psf;
            this.jmps = jmps;
        }
    }

    // Minimum jumps required to reach
    // end of the array
    public static int[] minJumps(int[] arr)
    {
        int dp[] = new int[arr.length];

        Arrays.fill(dp, Integer.MAX_VALUE);

        int n = dp.length;

        dp[n - 1] = 0;

        for (int i = n - 2; i >= 0; i--) {
            // Stores the maximum number
            // of steps that can be taken
            // from the current index
            int steps = arr[i];
            int min = Integer.MAX_VALUE;

            for (int j = 1; j <= steps && i + j < n; j++) {
                // Checking if index stays
                // within bounds
                if (dp[i + j] != Integer.MAX_VALUE
                    && dp[i + j] < min) {
                    // Stores the minimum
                    // number of jumps
                    // required to jump
                    // from (i + j)-th index
                    min = dp[i + j];
                }
            }

            if (min != Integer.MAX_VALUE)
                dp[i] = min + 1;
        }
        return dp;
    }

    // Function to find all possible
    // paths to reach end of array
    // requiring minimum number of steps
    public static void possiblePath(
        int[] arr, int[] dp)
    {

        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(0, "" + 0, dp[0]));

        while (queue.size() > 0) {
            Pair tmp = queue.remove();

            if (tmp.jmps == 0) {
                System.out.println(tmp.psf);
                continue;
            }

            for (int step = 1;
                 step <= arr[tmp.idx];
                 step++) {

                if (tmp.idx + step < arr.length
                    && tmp.jmps - 1 == dp[tmp.idx + step]) {
                    // Storing the neighbours
                    // of current index element
                    queue.add(new Pair(
                        tmp.idx + step,
                        tmp.psf + " -> " + (tmp.idx + step),
                        tmp.jmps - 1));
                }
            }
        }
    }

    // Function to find the minimum steps
    // and corresponding paths to reach
    // end of an array
    public static void Solution(int arr[])
    {
        // Stores the minimum jumps from
        // each position to last position
        int dp[] = minJumps(arr);

        possiblePath(arr, dp);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 3, 0, 2, 1,
                      2, 4, 2, 0, 0 };
        int size = arr.length;
        Solution(arr);
    }
}
```

## **蟒蛇 3**

```
# Python3 program to implement the
# above approach
from queue import Queue
import sys

# Pair Class instance
class Pair(object):

    # Stores the current index
    idx = 0

    # Stores the path
    # travelled so far
    psf = ""

    # Stores the minimum jumps
    # required to reach the
    # last index from current index
    jmps = 0

    # Constructor
    def __init__(self, idx, psf, jmps):

        self.idx = idx
        self.psf = psf
        self.jmps = jmps

# Minimum jumps required to reach
# end of the array
def minJumps(arr):

    MAX_VALUE = sys.maxsize
    dp = [MAX_VALUE for i in range(len(arr))]

    n = len(dp)

    dp[n - 1] = 0

    for i in range(n - 2, -1, -1):

        # Stores the maximum number
        # of steps that can be taken
        # from the current index
        steps = arr[i]
        minimum = MAX_VALUE

        for j in range(1, steps + 1, 1):
            if i + j >= n:
                break

            # Checking if index stays
            # within bounds
            if ((dp[i + j] != MAX_VALUE) and
                (dp[i + j] < minimum)):

                # Stores the minimum
                # number of jumps
                # required to jump
                # from (i + j)-th index
                minimum = dp[i + j]

        if minimum != MAX_VALUE:
            dp[i] = minimum + 1

    return dp

# Function to find all possible
# paths to reach end of array
# requiring minimum number of steps
def possiblePath(arr, dp):

    queue = Queue(maxsize = 0)
    p1 = Pair(0, "0", dp[0])
    queue.put(p1)

    while queue.qsize() > 0:
        tmp = queue.get()

        if tmp.jmps == 0:
            print(tmp.psf)
            continue

        for step in range(1, arr[tmp.idx] + 1, 1):
            if ((tmp.idx + step < len(arr)) and
               (tmp.jmps - 1 == dp[tmp.idx + step])):

                # Storing the neighbours
                # of current index element
                p2 = Pair(tmp.idx + step, tmp.psf +
                           " -> " + str((tmp.idx + step)),
                         tmp.jmps - 1)

                queue.put(p2)

# Function to find the minimum steps
# and corresponding paths to reach
# end of an array
def Solution(arr):

    # Stores the minimum jumps from
    # each position to last position
    dp = minJumps(arr)

    possiblePath(arr, dp)

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 3, 0, 2, 1,
            2, 4, 2, 0, 0 ]
    size = len(arr)

    Solution(arr)

# This code is contributed by akhilsaini
```

## **C#**

```
// C# program to implement the
// above approach
using System;
using System.Collections;

// Pair Struct
public struct Pair
{

    // Stores the current index
    public int idx;

    // Stores the path
    // travelled so far
    public string psf;

    // Stores the minimum jumps
    // required to reach the
    // last index from current index
    public int jmps;

    // Constructor
    public Pair(int idx, String psf, int jmps)
    {
        this.idx = idx;
        this.psf = psf;
        this.jmps = jmps;
    }
}

class GFG{

// Minimum jumps required to reach
// end of the array
public static int[] minJumps(int[] arr)
{
    int[] dp = new int[arr.Length];
    int n = dp.Length;

    for(int i = 0; i < n; i++)
        dp[i] = int.MaxValue;

    dp[n - 1] = 0;

    for(int i = n - 2; i >= 0; i--)
    {

        // Stores the maximum number
        // of steps that can be taken
        // from the current index
        int steps = arr[i];
        int min = int.MaxValue;

        for(int j = 1;
                j <= steps && i + j < n;
                j++)
        {

            // Checking if index stays
            // within bounds
            if (dp[i + j] != int.MaxValue &&
                dp[i + j] < min)
            {

                // Stores the minimum
                // number of jumps
                // required to jump
                // from (i + j)-th index
                min = dp[i + j];
            }
        }

        if (min != int.MaxValue)
            dp[i] = min + 1;
    }
    return dp;
}

// Function to find all possible
// paths to reach end of array
// requiring minimum number of steps
public static void possiblePath(int[] arr,
                                int[] dp)
{
    Queue queue = new Queue();
    queue.Enqueue(new Pair(0, "0", dp[0]));

    while (queue.Count > 0)
    {
        Pair tmp = (Pair)queue.Dequeue();

        if (tmp.jmps == 0)
        {
            Console.WriteLine(tmp.psf);
            continue;
        }

        for(int step = 1;
                step <= arr[tmp.idx];
                step++)
        {
            if (tmp.idx + step < arr.Length &&
               tmp.jmps - 1 == dp[tmp.idx + step])
            {

                // Storing the neighbours
                // of current index element

                queue.Enqueue(new Pair(
                    tmp.idx + step,
                    tmp.psf + " -> " +
                   (tmp.idx + step),
                   tmp.jmps - 1));
            }
        }
    }
}

// Function to find the minimum steps
// and corresponding paths to reach
// end of an array
public static void Solution(int[] arr)
{

    // Stores the minimum jumps from
    // each position to last position
    int[] dp = minJumps(arr);

    possiblePath(arr, dp);
}

// Driver Code
static public void Main()
{
    int[] arr = { 3, 3, 0, 2, 1,
                  2, 4, 2, 0, 0 };
    int size = arr.Length;

    Solution(arr);
}
}

// This code is contributed by akhilsaini
```

****Output:** 

```
0 -> 3 -> 5 -> 6 -> 9
0 -> 3 -> 5 -> 7 -> 9

```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)***