# 每小时停车所用时间

> 原文:[https://www . geeksforgeeks . org/每小时停工时间/](https://www.geeksforgeeks.org/time-taken-per-hour-for-stoppage-of-car/)

一辆汽车以平均速度 **S** km/h 行驶而不发生任何故障，故障后汽车的速度降低到平均速度 **S1** km/h。任务是找出每小时因故障而浪费的时间。
**例:**

> **输入:** S = 50，S1 = 30
> **输出:** 24 分钟
> **输入:** S = 30，S1 = 10
> **输出:** 40 分钟

**进场:**举第一个例子，

> 无任何停止的车速= 50 公里每小时，即 60 分钟内行驶 50 公里。
> 停车时的车速= 30 公里每小时，即 60 分钟内行驶 30 公里。
> 现在，如果没有停工，那么 30 公里可以在 36 分钟内完成。
> 50 公里–>60 分钟
> 30 公里–>(60/50)* 30 = 36 分钟
> 但需要 60 分钟。
> 因此，每小时停工时间为 60 分钟–36 分钟= 24 分钟。

这可以使用以下公式计算:

![](img/79947f5aa8481ce1cc81fe1c77eb36df.png)

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the time taken
// per hour for stoppage
int numberOfMinutes(int S, int S1)
{

    int Min = 0;

    Min = ((S - S1) / floor(S)) * 60;

    return Min;
}

// Driver code
int main()
{
    int S = 30, S1 = 10;

    cout << numberOfMinutes(S, S1) << " min";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the time taken
// per hour for stoppage
static int numberOfMinutes(int S, int S1)
{
    int Min = 0;

    Min = (int) (((S - S1) / Math.floor(S)) * 60);

    return Min;
}

// Driver code
public static void main(String[] args)
{
    int S = 30, S1 = 10;

    System.out.println(numberOfMinutes(S, S1) + " min");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the time taken
# per hour for stoppage
def numberOfMinutes(S, S1):

    Min = 0;

    Min = ((S - S1) / math.floor(S)) * 60;

    return int(Min);

# Driver code
if __name__ == '__main__':
    S, S1 = 30, 10;

    print(numberOfMinutes(S, S1), "min");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the time taken
// per hour for stoppage
static int numberOfMinutes(int S, int S1)
{
    int Min = 0;

    Min = (int) (((S - S1) /
                   Math.Floor((double)S)) * 60);

    return Min;
}

// Driver code
public static void Main()
{
    int S = 30, S1 = 10;

    Console.WriteLine(numberOfMinutes(S, S1) +
                                      " min");
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the time taken
// per hour for stoppage
function numberOfMinutes(S, S1)
{

    let Min = 0;

    Min = ((S - S1) / Math.floor(S)) * 60;

    return Min;
}

// Driver code

    let S = 30, S1 = 10;

    document.write(numberOfMinutes(S, S1) + " min");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
40 min
```

**时间复杂度:** O(1)

**辅助空间:** O(1)