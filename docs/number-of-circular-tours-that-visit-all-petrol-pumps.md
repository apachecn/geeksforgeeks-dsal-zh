# 参观所有汽油泵的循环游次数

> 原文:[https://www . geesforgeks . org/参观所有汽油泵的循环参观次数/](https://www.geeksforgeeks.org/number-of-circular-tours-that-visit-all-petrol-pumps/)

假设有一条环形路。那条路上有 **n** 个汽油泵。给你两个数组， **a[]** 和 **b[]** ，一个正整数 **c** 。其中 a[i]表示我们到达第 i <sup>个</sup>汽油泵时获得的燃油量，b[i]表示从第 i <sup>个</sup>汽油泵行驶到第(i + 1) <sup>个</sup>汽油泵所使用的燃油量，c 表示车辆中油箱的容量。任务是计算汽油泵的数量，从那里车辆将能够完成循环并回到起点。
本帖不同于[找第一个参观所有汽油车的循环游](https://www.geeksforgeeks.org/find-a-tour-that-visits-all-stations/)。
**举例:**

> 输入:n = 3，c = 3
> a[] = { 3，1，2 }
> b[] = { 2，2，2 }
> 输出:2
> 说明:
> 如果我们从 0 <sup>th</sup> 汽油泵开始，我们将获得
> 3 (a[0])升汽油，并损失 2 升(b[0])以行驶
> 至 1 <sup>st</sup> 汽油泵。在 1 <sup>st</sup> 汽油泵上加油 1 升(a[1])
> 汽油时，我们将损失 2
> 升(b[0])汽油到达 2 <sup>nd</sup> 汽油泵。
> 现在油箱空了。在 2 号<sup>和 2 号</sup>汽油泵处加油 2 升(a[2])汽油时，我们可以返回 0 号<sup>和 2 号</sup>
> 汽油泵。
> 如果我们从 1 <sup>st</sup> 汽油泵开始，我们将获得 1
> 升汽油，但要行驶到 2 <sup>nd</sup> 汽油泵
> 我们需要 2 升汽油，而我们没有。所以，我们不能
> 从 1 <sup>st</sup> 汽油泵开始。
> 如果我们从 2 <sup>和</sup>号汽油泵开始，我们将获得 2
> 升汽油，并通过
> 号损失 2 升汽油行驶到 0 <sup>和</sup>号汽油泵。在 1 号<sup>ST</sup>T43】汽油泵上加油 3 升时，我们可以通过损失 2 升汽油来到达 1 号 <sup>st</sup> 汽油
> 泵。在加油 1 升汽油时，我们
> 将剩下 2 升汽油，我们可以通过行驶至
> 2 <sup>和</sup>汽油泵使用。
> 输入:n = 3，c = 3
> a[] = { 3，1，2 }
> b[] = { 2，2，1 }
> 输出:2

**做法:**
问题涉及两个部分，首先涉及是否存在有效的启动汽油泵，其次，如果存在这样的汽油泵，检查汽油泵是否还可以作为启动汽油泵使用。
首先，让我们从一个汽油车 **s** 开始，行驶到汽油车， **s + 1，s + 2，s + 3 直到 s + j** ，假设我们在去汽油车 **s + j + 1** 之前没有油了，那么在 **s** 和 **s + j** 之间没有汽油车可以作为启动汽油车。因此，我们以 **s + j + 1** 作为启动汽油泵重新开始。如果在所有的汽油泵都用完之后没有这样的汽油泵，答案是 0。这一步需要 0(n)。
其次，让我们参观一个这样有效的汽油泵(姑且称之为 s)。s，即 s–1 之前的汽油泵也可以是起动汽油泵，前提是车辆可以在**s–1**起动并达到 **s** 。
如果 **a[i]** 是从汽油泵 **i** 获取可用燃油，而 **c** 是油箱的容量，而 **b[i]** 是车辆从汽油泵 **i** 行驶到 **i + 1** 所需的燃油量，那么让我们定义**需要【I】**如下:

```
need[i] = max(0, need[i + 1] + b[i] - min(c, a[i]))
```

**需要的【I】**是额外的燃油，如果在旅程开始时出现在车辆的汽油泵处 **i** (不包括 a【I】_，它可以是有效的汽油泵。
如果需要[i] = 0，那么汽油泵 **i** 是有效的启动汽油泵。我们从步骤 1 中知道需要[s] = 0。我们可以评估**s–1、s–2、…** 是否启动汽油泵。这一步也需要 O(n)。

## C++

```
// C++ Program to find the number of
// circular tour that visits all petrol pump
#include <bits/stdc++.h>
using namespace std;
#define N 100

// Return the number of pumps from where we
// can start the journey.
int count(int n, int c, int a[], int b[])
{
    int need[N];

    // Making Circular Array.
    for (int i = 0; i < n; i++) {
        a[i + n] = a[i];
        b[i + n] = b[i];
    }

    int s = 0;
    int tank = 0;

    // for each of the petrol pump.
    for (int i = 0; i < 2 * n; i++) {
        tank += a[i];
        tank = min(tank, c);
        tank -= b[i];

        // If tank is less than 0.
        if (tank < 0) {
            tank = 0;
            s = i + 1;
        }
    }

    // If starting pump is greater than n,
    // return ans as 0.
    if (s >= n)
        return 0;

    int ans = 1;
    need[s + n] = 0;

    // For each of the petrol pump
    for (int i = 1; i < n; i++) {
        int id = s + n - i;

        // Finding the need array
        need[id] = max(0, need[id + 1] + b[id]
                              - min(a[id], c));

        // If need is 0, increment the count.
        if (need[id] == 0)
            ans++;
    }

    return ans;
}

// Drivers code
int main()
{
    int n = 3;
    int c = 3;
    int a[2 * N] = { 3, 1, 2 };
    int b[2 * N] = { 2, 2, 2 };

    cout << count(n, c, a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the number of
// circular tour that visits all petrol pump
import java.io.*;

class GFG
{
    static int N = 100;

    // Return the number of pumps from where we
    // can start the journey.
    public static int count(int n, int c, int a[], int b[])
    {
        int need[] = new int[N];

        // Making Circular Array.
        for (int i = 0; i < n; i++)
        {
            a[i + n] = a[i];
            b[i + n] = b[i];
        }

        int s = 0;
        int tank = 0;

        // for each of the petrol pump.
        for (int i = 0; i < 2 * n; i++)
        {
            tank += a[i];
            tank = Math.min(tank, c);
            tank -= b[i];

            // If tank is less than 0.
            if (tank < 0)
            {
                tank = 0;
                s = i + 1;
            }
        }

        // If starting pump is greater
        //  than n, return ans as 0.
        if (s >= n)
            return 0;

        int ans = 1;
        need[s + n] = 0;

        // For each of the petrol pump
        for (int i = 1; i < n; i++)

        {
            int id = s + n - i;

            // Finding the need array
            need[id] = Math.max(0, need[id + 1] + b[id]
                                - Math.min(a[id], c));

            // If need is 0, increment the count.
            if (need[id] == 0)
                ans++;
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 3;
        int c = 3;
        int[] a = new int[]{ 3, 1, 2, 0, 0, 0 };
        int[] b = new int[]{ 2, 2, 2, 0, 0, 0 };

        System.out.print(count(n, c, a, b) + "\n");
    }
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 Program to find the number of
# circular tour that visits all petrol pump
N = 100

# Return the number of pumps from
# where we can start the journey.
def count(n, c, a, b):
    need = [0 for i in range(N)]

    # Making Circular Array.
    for i in range(0, n, 1):
        a[i + n] = a[i]
        b[i + n] = b[i]

    s = 0
    tank = 0

    # for each of the petrol pump.
    for i in range(0, 2 * n, 1):
        tank += a[i]
        tank = min(tank, c)
        tank -= b[i]

        # If tank is less than 0.
        if (tank < 0):
            tank = 0
            s = i + 1

    # If starting pump is greater
    # than n, return ans as 0.
    if (s >= n):
        return 0

    ans = 1
    need[s + n] = 0

    # For each of the petrol pump
    for i in range(1, n, 1):
        id = s + n - i

        # Finding the need array
        need[id] = max(0, need[id + 1] +
                     b[id] - min(a[id], c))

        # If need is 0, increment the count.
        if (need[id] == 0):
            ans += 1

    return ans

# Driver Code
if __name__ == '__main__':
    n = 3
    c = 3
    a = [3, 1, 2, 0, 0, 0]
    b = [2, 2, 2, 0, 0, 0]

    print(count(n, c, a, b))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# Program to find the number of
// circular tour that visits all petrol pump
using System;

class GFG
{
    static int N = 100;

    // Return the number of pumps from where we
    // can start the journey.
    public static int count(int n, int c, int[] a, int[] b)
    {
        int[] need = new int[N];

        // Making Circular Array.
        for (int i = 0; i < n; i++) {
            a[i + n] = a[i];
            b[i + n] = b[i];
        }

        int s = 0;
        int tank = 0;

        // for each of the petrol pump.
        for (int i = 0; i < 2 * n; i++) {
            tank += a[i];
            tank = Math.Min(tank, c);
            tank -= b[i];

            // If tank is less than 0.
            if (tank < 0) {
                tank = 0;
                s = i + 1;
            }
        }

        // If starting pump is greater than n,
        // return ans as 0.
        if (s >= n)
            return 0;

        int ans = 1;
        need[s + n] = 0;

        // For each of the petrol pump
        for (int i = 1; i < n; i++) {
            int id = s + n - i;

            // Finding the need array
            need[id] = Math.Max(0, need[id + 1] + b[id]
                                  - Math.Min(a[id], c));

            // If need is 0, increment the count.
            if (need[id] == 0)
                ans++;
        }

        return ans;
    }

    // Drivers code
    static void Main()
    {
        int n = 3;
        int c = 3;
        int[] a = new int[6]{ 3, 1, 2, 0, 0, 0 };
        int[] b = new int[6]{ 2, 2, 2, 0, 0, 0 };

        Console.Write(count(n, c, a, b) + "\n");
    }
    //This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>

// Javascript Program to find the number of
// circular tour that visits all petrol pump
var N = 100;

// Return the number of pumps from where we
// can start the journey.
function count(n, c, a, b)
{
    var need = Array(N).fill(0);

    // Making Circular Array.
    for (var i = 0; i < n; i++) {
        a[i + n] = a[i];
        b[i + n] = b[i];
    }

    var s = 0;
    var tank = 0;

    // for each of the petrol pump.
    for (var i = 0; i < 2 * n; i++) {
        tank += a[i];
        tank = Math.min(tank, c);
        tank -= b[i];

        // If tank is less than 0.
        if (tank < 0) {
            tank = 0;
            s = i + 1;
        }
    }

    // If starting pump is greater than n,
    // return ans as 0.
    if (s >= n)
        return 0;

    var ans = 1;
    need[s + n] = 0;

    // For each of the petrol pump
    for (var i = 1; i < n; i++) {
        var id = s + n - i;

        // Finding the need array
        need[id] = Math.max(0, need[id + 1] + b[id]
                              - Math.min(a[id], c));

        // If need is 0, increment the count.
        if (need[id] == 0)
            ans++;
    }

    return ans;
}

// Drivers code
var n = 3;
var c = 3;
var a = [ 3, 1, 2 ];
var b = [ 2, 2, 2 ];
document.write( count(n, c, a, b));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n)
参考:
[https://stackoverflow . com/questions/24408371/动态编程-寻找到达目的地的可能途径](https://stackoverflow.com/questions/24408371/dynamic-programming-find-possible-ways-to-reach-destination)