# 统计到达城市前可以消灭的最大巨人数量

> 原文:[https://www . geeksforgeeks . org/count-到达城市前可摧毁的最大巨人数量/](https://www.geeksforgeeks.org/count-maximum-number-of-giants-that-can-be-destroyed-before-they-reach-the-city/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**dist【】**和**speed【】**由 **N** 个整数组成，其中**dist【I】**是 **i <sup>第</sup>个**巨人离城的初始距离，**speed【I】**是 **i <sup>第</sup>个**巨人的速度。每分钟可以淘汰一个巨人。因此，在任何时候 **t** ，最多 **t** 巨人都可以被杀死。如果有更多的巨人能够及时到达城市 **t** ，那么比赛就结束了。任务是找到输球前能被淘汰的最大巨人数，或者 **N** 如果所有的巨人在到达城市前都能被淘汰。

**示例:**

> **输入:** dist[] = [1，3，4]，速度[] = [1，1，1]
> **输出:** 3
> **说明:**0 分钟开始时，巨人的距离为[1，3，4]。第一个巨人被淘汰。
> 第 1 分钟开始，巨人的距离为[X，2，3]。没有巨人被淘汰。
> 第 2 分钟开始，巨人的距离为[X，1，2]。第二个巨人被淘汰了。
> 第 3 分钟开始，巨人的距离为[X，X，1]。第三巨头被淘汰。
> 3 巨头全部可以淘汰。
> 
> **输入:** dist[] = [1，1，2，3]，速度[] = [1，1，1，1]
> **输出:** 1

**方法:**思路是用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决问题。找准每个巨人进城的时间，尽量用最短的接近时间消灭巨人。按照以下步骤解决问题:

*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **时区[]** 来存储时间。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   [将**距离【I/速度【I】**的值推入](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **时区[]。**
*   [按升序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **时区[]** 。
*   将变量 **curr_time** 初始化为 **0** 存储当前时间， **killcount** 初始化为 **0** 存储杀死的巨人数量。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   如果**时区【I】**小于**当前时间**，则[中断](https://www.geeksforgeeks.org/break-statement-cc/)循环。
    *   否则，将 **curr_time** 和 **killcount** 的计数增加 **1。**
*   执行上述步骤后，返回 **killcount** 的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of giants that can be destroyed
int eliminateMaximum(int dist[], int N,
                     int speed[])
{
    // Make a vector of time and
    // store the time corresponding
    // to its distance and speed
    vector<double> timezone;

    for (int i = 0; i < N; i++) {

        timezone.push_back((double)dist[i]
                           / (double)speed[i]);
    }

    // Sort time in ascending order
    sort(timezone.begin(), timezone.end());

    // Stores the time at each instant
    int Curr_time = 0;

    // Stores count of giants killed
    int killcount = 0;

    for (auto i : timezone) {
        if (i <= Curr_time) {

            // Game is lost
            break;
        }
        else {
            Curr_time++;
            killcount++;
        }
    }
    return killcount;
}

// Driver Code
int main()
{
    // Given input
    int dist[] = { 1, 3, 4 };
    int N = sizeof(dist) / sizeof(dist[0]);

    int speed[] = { 1, 1, 1 };
    int M = sizeof(speed) / sizeof(speed[0]);

    // function call
    cout << eliminateMaximum(dist, N, speed);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the maximum number
// of giants that can be destroyed
static int eliminateMaximum(int dist[], int N,
                     int speed[])
{

    // Make a vector of time and
    // store the time corresponding
    // to its distance and speed
    Vector<Double> timezone = new Vector<Double>();

    for (int i = 0; i < N; i++) {

        timezone.add((double)dist[i]
                           / (double)speed[i]);
    }

    // Sort time in ascending order
    Collections.sort(timezone);

    // Stores the time at each instant
    int Curr_time = 0;

    // Stores count of giants killed
    int killcount = 0;

    for (Double i : timezone) {
        if (i <= Curr_time) {

            // Game is lost
            break;
        }
        else {
            Curr_time++;
            killcount++;
        }
    }
    return killcount;
}

// Driver Code
public static void main(String[] args)
{
    // Given input
    int dist[] = { 1, 3, 4 };
    int N = dist.length;

    int speed[] = { 1, 1, 1 };
    int M = speed.length;

    // function call
    System.out.print(eliminateMaximum(dist, N, speed));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the maximum number
# of giants that can be destroyed
def eliminateMaximum(dist, N, speed):

    # Make a vector of time and
    # store the time corresponding
    # to its distance and speed
    timezone = []

    for i in range(N):
        timezone.append(dist[i] / speed[i])

    # Sort time in ascending order
    timezone.sort()

    # Stores the time at each instant
    Curr_time = 0

    # Stores count of giants killed
    killcount = 0

    for i in timezone:
        if (i <= Curr_time) :
            # Game is lost
            break

        else:
            Curr_time += 1
            killcount += 1

    return killcount

# Driver Code

# Given input
dist = [1, 3, 4]
N = len(dist)

speed = [1, 1, 1]
M = len(speed)

# function call
print(eliminateMaximum(dist, N, speed))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{
// Function to count the maximum number
// of giants that can be destroyed
static int eliminateMaximum(int []dist, int N,
                     int []speed)
{
    // Make a vector of time and
    // store the time corresponding
    // to its distance and speed
    List<double> timezone = new List<double>();

    for (int i = 0; i < N; i++) {

        timezone.Add((double)dist[i]/speed[i]);
    }

    // Sort time in ascending order
    timezone.Sort();

    // Stores the time at each instant
    int Curr_time = 0;

    // Stores count of giants killed
    int killcount = 0;

    foreach(double i in timezone) {
        if (i <= Curr_time) {

            // Game is lost
            break;
        }
        else {
            Curr_time++;
            killcount++;
        }
    }
    return killcount;
}

// Driver Code
public static void Main()
{
    // Given input
    int []dist = { 1, 3, 4 };
    int N = dist.Length;

    int []speed = { 1, 1, 1 };
    int M = speed.Length;

    // function call
    Console.Write(eliminateMaximum(dist, N, speed));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to count the maximum number
        // of giants that can be destroyed
        function eliminateMaximum(dist, N, speed)
        {

            // Make a vector of time and
            // store the time corresponding
            // to its distance and speed
            let timezone = [];

            for (let i = 0; i < N; i++) {

                timezone.push(dist[i] / speed[i]);
            }

            // Sort time in ascending order
            timezone.sort(function (a, b) { return a - b; });

            // Stores the time at each instant
            let Curr_time = 0;

            // Stores count of giants killed
            let killcount = 0;

            for (let i of timezone) {
                if (i <= Curr_time) {

                    // Game is lost
                    break;
                }
                else {
                    Curr_time++;
                    killcount++;
                }
            }
            return killcount;
        }

        // Driver Code

        // Given input
        let dist = [1, 3, 4];
        let N = dist.length;

        let speed = [1, 1, 1];
        let M = speed.length;

        // function call
        document.write(eliminateMaximum(dist, N, speed));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*