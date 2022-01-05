# 21 火柴杆问题

> 原文:[https://www.geeksforgeeks.org/21-matchsticks-problem/](https://www.geeksforgeeks.org/21-matchsticks-problem/)

给定 21 个火柴杆和 2 个用户，A 和 B(分别是电脑和用户)。用户一次最多可以挑选四根火柴。被迫挑最后一根火柴杆的人输了。
给定一个数组 **arr[]** 其中包含了计算机的移动。任务是打印用户的移动，以便用户赢得游戏。
T4【示例】T5:

> **输入:** N = 4，arr=[ 3，4，2，2]
> **输出:** 2，1，3，3
> 当电脑选择 3 根棍子时，用户选择 2 根棍子
> 当电脑选择 4 根棍子时，用户选择 1 根棍子
> 当电脑选择 2 根棍子时，用户选择 3 根棍子
> 当电脑选择 2 根棍子时，用户选择 3 根棍子
> 现在只剩下 1 根棍子了，电脑被迫去挑那根棍子
> 于是
> **输入:** N = 4 arr=[ 1，1，4，3]
> **输出:** 4，4，1，2

**进场:**

*   想法是考虑 20 根火柴杆，因为选择最后一根的用户将输掉游戏。
*   将 20 分成四份，即每份 5 号。因此，如果计算机选择 **x** 火柴棍，那么用户应该选择 **(5-x)** 火柴棍，并且应该以相同的方式进行。
*   这样，将使用 20 根火柴杆，最后一根火柴杆将由计算机挑选。

![](img/903d4f98c84d2768d500f486b7fe11dd.png)

以下是上述方法的实施

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the optimal strategy
void TwentyoneMatchstick(int arr[], int N)
{

    // Removing matchsticks in blocks of five
    for (int i = 0; i < N; i += 1) {
        cout << 5 - arr[i] << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    TwentyoneMatchstick(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the optimal strategy
static void TwentyoneMatchstick(int arr[], int N)
{

    // Removing matchsticks in blocks of five
    for (int i = 0; i < N; i += 1)
    {
        System.out.print(5 - arr[i] + " ");
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {3, 4, 2, 2};

    int N = arr.length;

    TwentyoneMatchstick(arr, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the optimal strategy
def TwentyoneMatchstick(arr, N):

    # Removing matchsticks in blocks of five
    for i in range(N):
        print(5 - arr[i], end = " ")

# Driver code
arr = [3, 4, 2, 2 ]

N = len(arr)

TwentyoneMatchstick(arr, N)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the optimal strategy
static void TwentyoneMatchstick(int []arr, int N)
{

    // Removing matchsticks in blocks of five
    for (int i = 0; i < N; i += 1)
    {
        Console.Write(5 - arr[i] + " ");
    }
    Console.Write("\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {3, 4, 2, 2};

    int N = arr.Length;

    TwentyoneMatchstick(arr, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
// javascript implementation of the approach

// Function to return the optimal strategy
 function TwentyoneMatchstick(arr, N)
{

    // Removing matchsticks in blocks of five
    for (var i = 0; i < N; i += 1)
    {
        document.write(5 - arr[i] + " ");
    }
    document.write("<br>");
}

// Driver code
    var arr = [3, 4, 2, 2];
    var N = arr.length;
    TwentyoneMatchstick(arr, N);

// This code is contributed by bunnyram19.

```

**Output:** 

```
2 1 3 3
```

**时间复杂度:** O(N)