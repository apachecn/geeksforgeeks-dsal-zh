# 如果第二个人以给定的速度行进，第二个人移动到第一个人之前的小时数

> 原文:[https://www . geeksforgeeks . org/第二个人以给定速度行驶时，第二个人移动的小时数领先于第一个人/](https://www.geeksforgeeks.org/number-of-hours-after-which-the-second-person-moves-ahead-of-the-first-person-if-they-travel-at-a-given-speed/)

给定三个整数 **A** 、 **B** 和 **K** 。最初，第一个人领先第二个人 **K** 公里。每小时第一人前进 **A** 公里，第二人前进 **B** 公里。任务是打印第二个人越过第一个人的小时数。如果无法做到，则打印 **-1** 。

**示例:**

> **输入:** A = 4，B = 5，K = 1
> **输出:** 2
> 最初第一人领先 1 公里。
> 1 小时后，第一个人和第二个人在同一个地方。
> 2 小时后，第一个人领先第一个人 1 公里。
> 
> **输入:** A = 6，B = 5，K = 1
> **输出:** -1

一种**天真的做法**是线性检查每一个小时，当第二个人移动到第一个人之前时打印第 n 个小时。
一种高效的****方法**就是用数学方法解决问题。当第二个人移动到第一个人之前时，小时数将为**K/(B–A)+1**。由于您需要行驶 **K** 公里，因此所花费的时间将是**K/(B–A)**，其中**B–A**是第二个人相对于第一个人的速度。如果 **A ≥ B** 那么第二个人不可能穿越第一个人。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// hours for the second person to move ahead
int findHours(int a, int b, int k)
{
    if (a >= b)
        return -1;

    // Time taken to equalize
    int time = k / (b - a);

    // Time taken to move ahead
    time = time + 1;

    return time;
}

// Driver code
int main()
{
    int a = 4, b = 5, k = 1;
    cout << findHours(a, b, k);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function to return the number of
// hours for the second person to move ahead
static int findHours(int a, int b, int k)
{
    if (a >= b)
        return -1;

    // Time taken to equalize
    int time = k / (b - a);

    // Time taken to move ahead
    time = time + 1;

    return time;
}

// Driver code
public static void main (String[] args)
{

        int a = 4, b = 5, k = 1;
        System.out.println (findHours(a, b, k));
}
}

// The code is contributed by ajit..@23
```

## **蟒蛇 3**

```
# Python3 implementation of the above approach

# Function to return the number of
# hours for the second person to move ahead
def findHours(a, b, k):
    if (a >= b):
        return -1

    # Time taken to equalize
    time = k // (b - a)

    # Time taken to move ahead
    time = time + 1

    return time

# Driver code

a = 4
b = 5
k = 1
print(findHours(a, b, k))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the number of
// hours for the second person to move ahead
static int findHours(int a, int b, int k)
{
    if (a >= b)
        return -1;

    // Time taken to equalize
    int time = k / (b - a);

    // Time taken to move ahead
    time = time + 1;

    return time;
}

// Driver code
static public void Main ()
{
    int a = 4, b = 5, k = 1;
    Console.Write(findHours(a, b, k));
}
}

// The code is contributed by ajit.
```

## **java 描述语言**

```
<script>

// Javascript implementation of the above approach

// Function to return the number of hours
// for the second person to move ahead
function findHours(a, b, k)
{
    if (a >= b)
        return -1;

    // Time taken to equalize
    let time = k / (b - a);

    // Time taken to move ahead
    time = time + 1;

    return time;
}

// Driver code
let a = 4, b = 5, k = 1;

document.write(findHours(a, b, k));

// This code is contributed by Mayank Tyagi

</script>
```

****Output:** 

```
2
```**