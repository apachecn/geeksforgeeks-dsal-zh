# 使用 N 个管道注满水箱所需的最短时间

> 原文:[https://www . geeksforgeeks . org/使用 n 管向水箱注水所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-fill-a-cistern-using-n-pipes/)

给定总共 N+1 个管道所需的时间，其中 N 个管道用于填充水箱，单个管道用于排空水箱。任务是计算如果所有 N+1 个管道一起打开，水箱将被注满的时间。

**示例**:

```
Input: n = 2, 
pipe1 = 12 hours, pipe2 = 14 hours,
emptypipe = 30 hours
Output: 8 hours

Input: n = 1, 
pipe1 = 12 hours
emptypipe = 18 hours
Output: 36 hours 
```

**进场:**

*   如果管道 1 能在“n”小时内注满水箱，那么在 1 小时内，管道 1 就能注满“1/n”水箱。
*   同样，如果管道 2 可以在“米”小时内充满水箱，那么在一小时内，管道 2 将能够充满“1/米”水箱。
*   所以在…对于其他管道。

**所以，用 N 根管子在 1 小时内填充水箱所做的总功为**

> 1/n + 1/m + 1/p…… + 1/z
> 其中 n，m，p…..，z 分别是每个管道花费的小时数。
> 
> 上述表达式的结果将是所有管道在 1 小时内共同完成的那部分工作，假设 **a / b** 。
> 计算加满水箱的时间为 **b / a** 。

**考虑两个管道的例子:**

> 第一根管子注满水箱所需的时间= 12 小时
> 第二根管子注满水箱所需的时间= 14 小时
> 第三根管子排空水箱所需的时间= 30 小时
> 第一根管子在 1 小时内完成的功= 1/12
> 第二根管子在 1 小时内完成的功= 1/14
> 第三根管子在 1 小时内完成的功=–(1/30)因为它排空了管子。
> 因此，所有管道在 1 小时内完成的总功为
> =>(1/12+1/14)–(1/30)
> =>((7+6)/(84))–(1/30)
> =>((13)/(84))–(1/30)
> =>51/420
> 因此，注满水箱所需时间为 420

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the time
float Time(float arr[], int n, int Emptypipe)
{

    float fill = 0;
    for (int i = 0; i < n; i++)
        fill += 1 / arr[i];

    fill = fill - (1 / (float)Emptypipe);

    return 1 / fill;
}

// Driver Code
int main()
{
    float arr[] = { 12, 14 };
    float Emptypipe = 30;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << floor(Time(arr, n, Emptypipe)) << " Hours";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;

class GFG
{

// Function to calculate the time
static float Time(float arr[], int n,
                  float Emptypipe)
{
    float fill = 0;
    for (int i = 0; i < n; i++)
        fill += 1 / arr[i];

    fill = fill - (1 / (float)Emptypipe);

    return 1 / fill;
}

// Driver Code
public static void main (String[] args)
{
    float arr[] = { 12, 14 };
    float Emptypipe = 30;
    int n = arr.length;

    System.out.println((int)(Time(arr, n,
                        Emptypipe)) + " Hours");
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to calculate the time
def Time(arr, n, Emptypipe) :

    fill = 0
    for i in range(0,n) :
        fill += (1 / arr[i])

    fill = fill - (1 / float(Emptypipe))

    return int(1 / fill)

# Driver Code
if __name__=='__main__':
    arr = [ 12, 14 ]
    Emptypipe = 30
    n = len(arr)
    print((Time(arr, n, Emptypipe))
          , "Hours")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Function to calculate the time
static float Time(float []arr, int n,
                  float Emptypipe)
{
    float fill = 0;
    for (int i = 0; i < n; i++)
        fill += 1 / arr[i];

    fill = fill - (1 / (float)Emptypipe);

    return 1 / fill;
}

// Driver Code
public static void Main ()
{
    float []arr = { 12, 14 };
    float Emptypipe = 30;
    int n = arr.Length;

    Console.WriteLine((int)(Time(arr, n,
                             Emptypipe)) +
                                " Hours");
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to calculate the time
function T_ime($arr, $n, $Emptypipe)
{
    $fill = 0;
    for ($i = 0; $i < $n; $i++)
        $fill += 1 / $arr[$i];

    $fill = $fill - (1 / $Emptypipe);

    return 1 / $fill;
}

// Driver Code
$arr = array( 12, 14 );
$Emptypipe = 30;
$n = count($arr);

echo (int)T_ime($arr, $n,
                $Emptypipe) . " Hours";

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to calculate the time
function Time(arr, n, Emptypipe)
{
    var fill = 0;
    for(var i = 0; i < n; i++)
        fill += 1 / arr[i];

    fill = fill - (1 / Emptypipe);

    return 1 / fill;
}

// Driver Code
var arr = [ 12, 14 ];
var Emptypipe = 30;
var n = arr.length;

document.write(Math.floor(
    Time(arr, n, Emptypipe)) + " Hours");

// This code is contributed by itsok

</script>
```

**Output:** 

```
8 Hours
```