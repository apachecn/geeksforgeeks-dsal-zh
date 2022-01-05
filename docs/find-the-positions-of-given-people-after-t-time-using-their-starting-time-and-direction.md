# 利用给定的人的开始时间和方向

找到给定的人在 T 时间后的位置

> 原文:[https://www . geeksforgeeks . org/利用给定人员的起始时间和方向找到他们的位置/](https://www.geeksforgeeks.org/find-the-positions-of-given-people-after-t-time-using-their-starting-time-and-direction/)

有一个长度为 **N** 的圆形轨迹，给定两个大小为 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**start【】】**和**direct【】T7】和一个整数 **T，**其中**start【**I**】**代表**I<sup>th</sup>T19】人和**direct【**I**】 逆时针如果**直接【**I**】**是 **-1** ，任务是找到 **T** 时间单位后所有人的位置。******

> **注:**每个人在 **1** 时间单位内移动 **1** 单位距离。

**示例:**

> **输入:** N = 5，M = 2，T = 1，start[] = {2，3}，direct[] = {1，-1}
> **输出:** 3 2
> **解释:**给定的圆有 5 个从 1 到 5 的点，有两个人假设 A 和 b，A 从第 2 个点开始，顺时针移动为 direct[0] = 1，所以 1 分钟后他会在点 3。同样，B 从第 3 点开始逆时针移动，所以 1 分钟后他将在第 2 点。所以，ans 数组包含[3，2]排序后就变成了[2，3]。
> 
> **输入:** N = 4，M = 3，T = 2，start[] = {2，1，4}，direct[] = {-1，1，-1}
> **输出:** 4 3 2

**方法:**解决这个问题的思路是基于对利用拥有圆形轨迹的观察。找到 **T** 时间单位后的点，取模找到答案。按照以下步骤解决问题:

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，M)** ，并执行以下任务:
    *   将变量 **t_moves** 初始化为**直接[**I*** t .**
    *   将变量 **end_pos** 初始化为**(((start[I]+t _ moves)% N)+N)% N**。
    *   如果 **end_pos** 为 **0** ，则将**start【**I**】**的值设置为 **N** ，否则设置为 **end_pos** 。
*   执行上述步骤后，打印数组**开始[]** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <ctime>
#include <iostream>
using namespace std;

// Function to find the final position
// of men's after T minutes
int* positionAfterTMin(int N, int M, int T, int start[],
                       int direct[])
{
    // Find the location of the i-th
    // person after T minutes
    for (int i = 0; i < M; i++)
    {

        // Total points moved m by i-th
        // person in T minutes
        int t_moves = direct[i] * T;

        // As the path is circular then
        // there is a chance that the
        // person will traverse the same
        // points again
        int end_pos = (((start[i] + t_moves) % N) + N) % N;

        // Storing location of the
        // i-th person
        start[i] = (end_pos == 0) ? N : end_pos;
    }

    // Returning array which contains
    // location of every person moving
    // in time T units
    return start;
}

// Driver Code
int main()
{

    int N = 4;
    int M = 3;
    int T = 2;
    int start[] = { 2, 1, 4 };
    int direct[] = { -1, 1, -1 };
    int* ans = positionAfterTMin(N, M, T, start, direct);
    for (int i = 0; i < M; i++) {
        cout << *(ans + i) << " ";
    }
    return 0;
}

// This code is contributed by Kdheeraj.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the final position
    // of men's after T minutes
    public static int[] positionAfterTMin(
        int N, int M, int T,
        int[] start, int[] direct)
    {

        // Find the location of the i-th
        // person after T minutes
        for (int i = 0; i < M; i++) {

            // Total points moved m by i-th
            // person in T minutes
            int t_moves = direct[i] * T;

            // As the path is circular then
            // there is a chance that the
            // person will traverse the same
            // points again
            int end_pos
                = (((start[i] + t_moves)
                    % N)
                   + N)
                  % N;

            // Storing location of the
            // i-th person
            start[i] = (end_pos == 0) ? N : end_pos;
        }

        // Returning array which contains
        // location of every person moving
        // in time T units
        return start;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;
        int M = 3;
        int T = 2;
        int[] start = { 2, 1, 4 };
        int[] direct = { -1, 1, -1 };

        int[] ans = positionAfterTMin(
            N, M, T, start, direct);

        for (int i = 0; i < ans.length; i++) {
            System.out.print(ans[i] + " ");
        }
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the final position
# of men's after T minutes
def positionAfterTMin(N, M, T, start, direct):

    # Find the location of the i-th
    # person after T minutes
    for i in range(M):

        # Total points moved m by i-th
        # person in T minutes
        t_moves = direct[i] * T

        # As the path is circular then
        # there is a chance that the
        # person will traverse the same
        # points again
        end_pos = (((start[i] + t_moves) % N) + N) % N

        # Storing location of the
        # i-th person
        if end_pos == 0:
            start[i] = N
        else:
            start[i] = end_pos

    # Returning array which contains
    # location of every person moving
    # in time T units
    return start

# Driver Code
if __name__ == "__main__":
    N = 4
    M = 3
    T = 2
    start = [2, 1, 4]
    direct = [-1, 1, -1]
    ans = positionAfterTMin(N, M, T, start, direct)
    print(ans)

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the final position
    // of men's after T minutes
    public static int[] positionAfterTMin(
        int N, int M, int T,
        int[] start, int[] direct)
    {

        // Find the location of the i-th
        // person after T minutes
        for (int i = 0; i < M; i++) {

            // Total points moved m by i-th
            // person in T minutes
            int t_moves = direct[i] * T;

            // As the path is circular then
            // there is a chance that the
            // person will traverse the same
            // points again
            int end_pos
                = (((start[i] + t_moves)
                    % N)
                   + N)
                  % N;

            // Storing location of the
            // i-th person
            start[i] = (end_pos == 0) ? N : end_pos;
        }

        // Returning array which contains
        // location of every person moving
        // in time T units
        return start;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 4;
        int M = 3;
        int T = 2;
        int[] start = { 2, 1, 4 };
        int[] direct = { -1, 1, -1 };

        int[] ans = positionAfterTMin(
            N, M, T, start, direct);

        for (int i = 0; i < ans.Length; i++) {
            Console.Write(ans[i] + " ");
        }
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
// Javascript program for the above approach

// Function to find the final position
// of men's after T minutes
function positionAfterTMin(N, M, T, start, direct)
{

  // Find the location of the i-th
  // person after T minutes
  for (let i = 0; i < M; i++)
  {

    // Total points moved m by i-th
    // person in T minutes
    let t_moves = direct[i] * T;

    // As the path is circular then
    // there is a chance that the
    // person will traverse the same
    // points again
    let end_pos = (((start[i] + t_moves) % N) + N) % N;

    // Storing location of the
    // i-th person
    start[i] = end_pos == 0 ? N : end_pos;
  }

  // Returning array which contains
  // location of every person moving
  // in time T units
  return start;
}

// Driver Code
let N = 4;
let M = 3;
let T = 2;
let start = [2, 1, 4];
let direct = [-1, 1, -1];
let ans = positionAfterTMin(N, M, T, start, direct);
for (let i = 0; i < 3; i++) {
  document.write(ans[i] + " ");
}

// This code is contributed by _saaurabh_jaiswal.
```

**Output:** 

```
4 3 2
```

***时间复杂度:**O(M)*
T5**辅助空间:** O(1)