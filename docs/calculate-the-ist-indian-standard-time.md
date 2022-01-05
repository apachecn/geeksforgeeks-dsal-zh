# 计算 IST:印度标准时间

> 原文:[https://www . geesforgeks . org/compute-the-ist-Indian-standard-time/](https://www.geeksforgeeks.org/calculate-the-ist-indian-standard-time/)

给定两个整数 **H** 和 **R** ，其中 **H** 是一个地点**X****的小时时间，R** 是从地点 **X** 到**印度**的度数距离，任务是在 [IST](https://en.wikipedia.org/wiki/Indian_Standard_Time) 找到当前时间。
[UTC(协调世界时)](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)是一种 24 小时时间标准，用于同步世界时钟。
**例:**

> **输入:** H = 24，R = 82.50
> **输出:**IST = 5:30
> IST =(24/360)* 82.50
> = 5.5
> = 0.5 * 60(即 60 分钟= 360 度旋转和 1 分钟= 6 度 so，0.5 小时* 60 = 30)
> IST = 5:30
> **输入:【T11**

**进场:**

*   已知 **1 小时= 60 分钟= 360 度旋转**。
*   1 度旋转= (1 / 360)小时。
*   2 度旋转= (1 / 360) * 2 小时。
*   因此，广义公式将是:

```
IST = UTC + (H / 360) * R (UTC = 0 for IST)
IST = ( H / 360 ) * R
```

答案将以 0:00 的形式转换，因此 IST 的整数部分(小时)和浮点部分是分开的，浮点部分乘以 60 将其转换为分钟。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <cmath>
#include <iostream>
using namespace std;

// Function to calculate Indian Standard Time
void cal_IST(int h, float r)
{
    float IST = (h * r * 1.0) / 360;

    // Separate integer part
    int int_IST = (int)IST;

    // Separate float part and return ceil value
    int float_IST = ceil((IST - int_IST) * 60);

    cout << int_IST << ":" << float_IST;
}

// Driver code
int main()
{

    // Number of hours (1 - 24)
    int h = 20;

    // Rotations in degrees
    float r = 150;

    cal_IST(h, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.math.*;

class GFG
{
    // Function to calculate Indian Standard Time
    public static void cal_IST(int h, double r)
    {
        double IST = (h * r * 1.0) / 360;

        // Separate integer part
        int int_IST = (int)IST;

        // Separate float part and return ceil value
        int float_IST = (int)Math.ceil((int)((IST - int_IST) * 60));

        System.out.println(int_IST + ":" + float_IST);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Number of hours (1 - 24)
        int h = 20;

        // Rotations in degrees
        double r = 150;

        cal_IST(h, r);
    }
}

// This code is contributed by Naman_Garg
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil

# Function to calculate Indian Standard Time
def cal_IST(h, r) :

    IST = round((h * r * 1.0) / 360, 3);

    # Separate integer part
    int_IST = int(IST);

    # Separate float part and return ceil value
    float_IST = ceil((IST - int_IST) * 60);

    print(int_IST, ":", float_IST);

# Driver code
if __name__ == "__main__" :

    # Number of hours (1 - 24)
    h = 20;

    # Rotations in degrees
    r = 150;

    cal_IST(h, r);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to calculate Indian Standard Time
    public static void cal_IST(int h, double r)
    {
        double IST = (h * r * 1.0) / 360;

        // Separate integer part
        int int_IST = (int)IST;

        // Separate float part and return ceil value
        int float_IST = (int)Math.Floor((
                         double)(IST - int_IST) * 60);

        Console.WriteLine(int_IST + ":" + float_IST);
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Number of hours (1 - 24)
        int h = 20;

        // Rotations in degrees
        double r = 150;

        cal_IST(h, r);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to calculate Indian Standard Time
function cal_IST(h, r)
{
    let IST = (h * r * 1.0) / 360;

    // Separate integer part
    let int_IST = parseInt(IST);

    // Separate float part and return ceil value
    let float_IST = Math.ceil(parseInt((IST - int_IST) * 60));

    document.write(int_IST + ":" + float_IST);
}

// Driver code

    // Number of hours (1 - 24)
    let h = 20;

    // Rotations in degrees
    let r = 150;

    cal_IST(h, r);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
8:20
```