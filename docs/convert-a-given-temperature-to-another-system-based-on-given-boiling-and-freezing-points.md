# 根据给定的沸点和冰点将给定的温度转换成另一个系统

> 原文:[https://www . geeksforgeeks . org/convert-基于给定沸点和冰点将给定温度转换为另一个系统/](https://www.geeksforgeeks.org/convert-a-given-temperature-to-another-system-based-on-given-boiling-and-freezing-points/)

有两个温度计，给定五个整数 **F1** 、 **B1** 、 **F2** 、 **B2** 和 **T** ，其中 **F1** 和 **B1** 是**温度计 1** 上的水的冰点和沸点， **F2** 和 **B2** 是**上的水的冰点和沸点任务是在温度计 **2** 上找到温度。**

**示例:**

> **输入:** F1 = 0，B1 = 10，F2 = 100，B2 = 200，T = 4
> T3】输出: 140.00
> 
> **输入:** F1 = 0，B1 = 100，F2 = 32，B2 = 212，T = 37
> T3】输出: 98.60

**方式:**考虑第一个温度计采用 **U1** 单位制，第二个温度计采用 **U2** 单位制。

*   这个想法是在每个温度计上得到水的沸点和冰点之间的差值。
*   两个温度计的冰点和沸点之间的单位数显示了相同的温差。

> 所以，**(B1–F1)U1 = =(B2–F2)U2**
> 用一元法，U1 =(B2–F2)/(B1–F1)U2
> 的相对值 **U2** 为**T–F1**， **U1** 为**T–F2**
> 因此，T = F2+((B2–F2)/(B1–F1))*(T–F1)

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Function to return temperature
// in the second thermometer
double temp_convert(int F1, int B1, int F2,
                    int B2, int T)
{
    float t2;

    // Calculate the temperature
    t2 = F2 + (float)(B2 - F2) /
                     (B1 - F1) *
                     (T - F1);

    return t2;
}

// Driver Code
int main()
{
    int F1 = 0, B1 = 100;
    int F2 = 32, B2 = 212;
    int T = 37;
    float t2;

    cout << temp_convert(F1, B1, F2, B2, T);
    return 0;
}

// This code is contributed by kirti
```

## C

```
// C program for above approach

#include <stdio.h>

// Function to return temperature
// in the second thermometer
double temp_convert(int F1, int B1, int F2,
                    int B2, int T)
{
    float t2;

    // Calculate the temperature
    t2 = F2
         + (float)(B2 - F2)
               / (B1 - F1) * (T - F1);

    return t2;
}

// Driver Code
int main()
{
    int F1 = 0, B1 = 100;
    int F2 = 32, B2 = 212;
    int T = 37;
    float t2;

    printf("%.2f",
           temp_convert(F1, B1, F2, B2, T));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG{

// Function to return temperature
// in the second thermometer
static double temp_convert(int F1, int B1, int F2,
                           int B2, int T)
{
    float t2;

    // Calculate the temperature
    t2 = F2 + (float)(B2 - F2) /
                     (B1 - F1) *
                      (T - F1);

    return t2;
}

// Driver Code
public static void main(String[] args)
{
    int F1 = 0, B1 = 100;
    int F2 = 32, B2 = 212;
    int T = 37;
    float t2;

    System.out.printf("%.2f",
                      temp_convert(F1, B1, F2, B2, T));
}
}

// This code is contributed by rishavmahato348
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to return temperature
# in the second thermometer
def temp_convert(F1, B1, F2, B2, T):

    # Calculate the temperature
    t2 = F2 + ((float)(B2 - F2) /
                      (B1 - F1) *
                       (T - F1))

    return t2

# Driver Code
F1 = 0
B1 = 100
F2 = 32
B2 = 212
T = 37

print(temp_convert(F1, B1, F2, B2, T))

# This code is contributed by Ankita Saini
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to return temperature
// in the second thermometer
static double temp_convert(int F1, int B1, int F2,
                           int B2, int T)
{
    float t2;

    // Calculate the temperature
    t2 = F2 + (float)(B2 - F2) /
                     (B1 - F1) *
                      (T - F1);

    return t2;
}

// Driver Code
public static void Main()
{
    int F1 = 0, B1 = 100;
    int F2 = 32, B2 = 212;
    int T = 37;
    //float t2;

    Console.Write(String.Format("{0:0.##}",
    temp_convert(F1, B1, F2, B2, T)));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to return temperature
// in the second thermometer
function temp_convert(F1, B1, F2, B2, T)
{
    var t2;

    // Calculate the temperature
    t2 = F2 + (B2 - F2) /
              (B1 - F1) *
               (T - F1);

    return t2;
}

// Driver Code
var F1 = 0, B1 = 100;
var F2 = 32, B2 = 212;
var T = 37;
var t2;

document.write(temp_convert(
    F1, B1, F2, B2, T).toFixed(2));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
98.60
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*