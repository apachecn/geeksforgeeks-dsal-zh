# 程序查找当天完成的剩余时间

> 原文:[https://www . geesforgeks . org/program-to-find-当日剩余完成时间/](https://www.geeksforgeeks.org/program-to-find-the-time-remaining-for-the-day-to-complete/)

以 **HH::MM、**的形式给出当前时间，其中 H 代表小时，M 代表 24 小时时间格式中的分钟。任务是将当天剩余的完成时间计算为 **HH::MM** 。
**例:**

```
Input: HH::MM = 00::01
Output: 23::01

Input: HH::MM = 23::55
Output: 00::05
```

**进场:**

1.  由于一天 24 小时的总分钟数为 **24 * 60 = 1440 分钟**
2.  计算以分钟为单位的完成时间
3.  以分钟的形式计算剩余时间为**总分钟–完成时间**
4.  将剩余时间转换为 HH::MM 格式

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the remaining time
void remainingTime(int h, int m)
{
    int totalMin, hoursRemaining, minRemaining;

    // Formula for total remaining minutes
    // = 1440 - 60h - m
    totalMin = 1440 - 60 * h - m;

    // Remaining hours
    hoursRemaining = totalMin / 60;

    // Remaining minutes
    minRemaining = totalMin % 60;

    cout << hoursRemaining << "::"
         << minRemaining << endl;
}

// Driver code
int main()
{

    // Current time
    int h = 0, m = 1;

    // Get the remaining time
    remainingTime(h, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

// Function to find the remaining time
static void remainingTime(int h, int m)
{
    int totalMin, hoursRemaining, minRemaining;

    // Formula for total remaining minutes
    // = 1440 - 60h - m
    totalMin = 1440 - 60 * h - m;

    // Remaining hours
    hoursRemaining = totalMin / 60;

    // Remaining minutes
    minRemaining = totalMin % 60;

    System.out.print(hoursRemaining+ "::"
        + minRemaining +"\n");
}

// Driver code
public static void main(String[] args)
{

    // Current time
    int h = 0, m = 1;

    // Get the remaining time
    remainingTime(h, m);
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Function to find the remaining time
def remainingTime(h, m):

    # Formula for total remaining minutes
    # = 1440 - 60h - m
    totalMin = 1440 - 60 * h - m

    # Remaining hours
    hoursRemaining = totalMin // 60

    # Remaining minutes
    minRemaining = totalMin % 60

    print(hoursRemaining,"::",minRemaining)

# Driver code

# Current time
h = 0
m = 1

# Get the remaining time
remainingTime(h, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to Number of pairs of lines
// having integer intersection points
using System;

class GFG
{

    // Function to find the remaining time
    static void remainingTime(int h, int m)
    {
        int totalMin, hoursRemaining, minRemaining;

        // Formula for total remaining minutes
        // = 1440 - 60h - m
        totalMin = 1440 - 60 * h - m;

        // Remaining hours
        hoursRemaining = totalMin / 60;

        // Remaining minutes
        minRemaining = totalMin % 60;

        Console.WriteLine(hoursRemaining+ "::"
                            + minRemaining);
    }

    // Driver code
    public static void Main()
    {

        // Current time
        int h = 0, m = 1;

        // Get the remaining time
        remainingTime(h, m);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to Number of pairs of lines
// having integer intersection points

    // Function to find the remaining time
    function remainingTime(h, m)
    {
        var totalMin, hoursRemaining, minRemaining;

        // Formula for total remaining minutes
        // = 1440 - 60h - m

        totalMin = 1440 - 60 * h - m;

        // Remaining hours

        hoursRemaining = totalMin / 60;

        // Remaining minutes

        minRemaining = totalMin % 60;

        document.write(Math.trunc(hoursRemaining)+
        "::" + minRemaining);
    }

    // Driver code

        // Current time
        var h = 0, m = 1;

        // Get the remaining time
        remainingTime(h, m);

</script>
```

**Output:** 

```
23::59
```