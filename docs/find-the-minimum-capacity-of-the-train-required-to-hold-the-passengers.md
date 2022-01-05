# 找到容纳乘客所需的列车最小载客量

> 原文:[https://www . geeksforgeeks . org/find-列车容纳乘客所需的最小容量/](https://www.geeksforgeeks.org/find-the-minimum-capacity-of-the-train-required-to-hold-the-passengers/)

给定进出列车的乘客数量，任务是找到列车的最小容量，以在整个旅程中保持所有乘客。
**例:**

> **输入:**进入[] = {3，5，2，0}，退出[] = {0，2，4，4}
> **输出:** 6
> 车站 1:列车通过能力= 3
> 车站 2:列车通过能力= 3+5–2 = 6
> 车站 3:列车通过能力= 6+2–4 = 4
> 车站 4:列车通过能力= 4–4 = 0
> 任何时刻
> 列车最多可容纳 6 名乘客。
> **输入:**输入[] = {5，2，2，0}，退出[] = {0，2，2，5}
> **输出:** 5

**进场:**某站列车当前通过能力可通过将列车进站人数相加，再减去出站人数计算得出。所需的最小容量将是所有站点当前容量的最大值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum capacity required
int minCapacity(int enter[], int exit[], int n)
{

    // To store the minimum capacity
    int minCap = 0;

    // To store the current capacity
    // of the train
    int currCap = 0;

    // For every station
    for (int i = 0; i < n; i++) {

        // Add the number of people entering the
        // train and subtract the number of people
        // exiting the train to get the
        // current capacity of the train
        currCap = currCap + enter[i] - exit[i];

        // Update the minimum capacity
        minCap = max(minCap, currCap);
    }

    return minCap;
}

// Driver code
int main()
{
    int enter[] = { 3, 5, 2, 0 };
    int exit[] = { 0, 2, 4, 4 };
    int n = sizeof(enter) / sizeof(enter[0]);

    cout << minCapacity(enter, exit, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum capacity required
static int minCapacity(int enter[],
                       int exit[], int n)
{

    // To store the minimum capacity
    int minCap = 0;

    // To store the current capacity
    // of the train
    int currCap = 0;

    // For every station
    for (int i = 0; i < n; i++)
    {

        // Add the number of people entering the
        // train and subtract the number of people
        // exiting the train to get the
        // current capacity of the train
        currCap = currCap + enter[i] - exit[i];

        // Update the minimum capacity
        minCap = Math.max(minCap, currCap);
    }
    return minCap;
}

// Driver code
public static void main(String[] args)
{
    int enter[] = { 3, 5, 2, 0 };
    int exit[] = { 0, 2, 4, 4 };
    int n = enter.length;

    System.out.println(minCapacity(enter, exit, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# minimum capacity required
def minCapacity(enter, exit, n):

    # To store the minimum capacity
    minCap = 0;

    # To store the current capacity
    # of the train
    currCap = 0;

    # For every station
    for i in range(n):

        # Add the number of people entering the
        # train and subtract the number of people
        # exiting the train to get the
        # current capacity of the train
        currCap = currCap + enter[i] - exit[i];

        # Update the minimum capacity
        minCap = max(minCap, currCap);
    return minCap;

# Driver code
if __name__ == '__main__':
    enter = [3, 5, 2, 0];
    exit = [0, 2, 4, 4];
    n = len(enter);

    print(minCapacity(enter, exit, n));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// capacity required
static int minCapacity(int []enter,
                       int []exit, int n)
{

    // To store the minimum capacity
    int minCap = 0;

    // To store the current capacity
    // of the train
    int currCap = 0;

    // For every station
    for (int i = 0; i < n; i++)
    {

        // Add the number of people entering the
        // train and subtract the number of people
        // exiting the train to get the
        // current capacity of the train
        currCap = currCap + enter[i] - exit[i];

        // Update the minimum capacity
        minCap = Math.Max(minCap, currCap);
    }
    return minCap;
}

// Driver code
public static void Main(String[] args)
{
    int []enter = { 3, 5, 2, 0 };
    int []exit = { 0, 2, 4, 4 };
    int n = enter.Length;

    Console.WriteLine(minCapacity(enter, exit, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum capacity required
function minCapacity(enter, exit, n) {

    // To store the minimum capacity
    let minCap = 0;

    // To store the current capacity
    // of the train
    let currCap = 0;

    // For every station
    for (let i = 0; i < n; i++) {

        // Add the number of people entering the
        // train and subtract the number of people
        // exiting the train to get the
        // current capacity of the train
        currCap = currCap + enter[i] - exit[i];

        // Update the minimum capacity
        minCap = Math.max(minCap, currCap);
    }

    return minCap;
}

// Driver code

let enter = [3, 5, 2, 0];
let exit = [0, 2, 4, 4];
let n = enter.length;

document.write(minCapacity(enter, exit, n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(n)