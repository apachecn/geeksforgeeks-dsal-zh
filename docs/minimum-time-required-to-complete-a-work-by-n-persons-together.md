# N 人一起完成一项工作所需的最短时间

> 原文:[https://www . geesforgeks . org/n 人共同完成一项工作所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-complete-a-work-by-n-persons-together/)

给定 N 个人完成某项工作的工作小时数。任务是找出他们一起工作的小时数。
**例:**

```
Input: n = 2, a = 6.0, b = 3.0
Output: 2 Hours

Input: n = 3, a = 6.0, b = 3.0, c = 4.0
Output: 1.33333 Hours
```

**解决方案:**

*   如果一个人能在‘n’天内完成一件工作，那么在一天内，这个人就会做‘1/n’的工作。
*   同样，如果一个人可以在 m 天内完成一件工作，那么在一天内，这个人将完成 1/m 的工作。
*   所以在…对其他人来说。

**所以，N 个人在 1 天内完成的总工作量为**

> 1/n + 1/m + 1/p…… + 1/z
> 其中 n，m，p…..，z 分别是每个人花费的天数。
> 以上表达式的结果将是 1 天内所有人一起完成的部分工作，假设 **a / b** 。
> 计算完成整个工作所需的时间为 **b / a** 。

**举两个人的例子:**

```
Time taken by 1st person to complete a work = 6 hours
Time taken by 2nd person to complete the same work = 2 hours

Work done by 1st person in 1 hour = 1/6
Work done by 2nd person in 1 hour = 1/2
So, total work done by them in 1 hour is
=> 1 / 6 + 1/ 2 
=> (2 + 6) / (2 * 6)
=> 8 / 12

So, to complete the whole work, the time taken will be 12/8.
```

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the time
float calTime(float arr[], int n)
{

    float work = 0;
    for (int i = 0; i < n; i++)
        work += 1 / arr[i];

    return 1 / work;
}

// Driver Code
int main()
{
    float arr[] = { 6.0, 3.0, 4.0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << calTime(arr, n) << " Hours";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.io.*;

class GFG
{

// Function to calculate the time
static double calTime(double arr[], int n)
{
    double work = 0;
    for (int i = 0; i < n; i++)
        work += 1 / arr[i];

    return 1 / work;
}

// Driver Code
public static void main (String[] args)
{
    double arr[] = { 6.0, 3.0, 4.0 };
    int n = arr.length;

    System.out.println(calTime(arr, n) +
                              " Hours");
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
def calTime(arr, n):

    work = 0
    for i in range(n):
        work += 1 / arr[i]

    return 1 / work

# Driver Code
arr = [ 6.0, 3.0, 4.0 ]
n = len(arr)

print(calTime(arr, n), "Hours")

# This code is contributed
# by Sanjit_Prasad
```

## C#

```
// C# implementation
// of above approach
using System;
class GFG
{

// Function to calculate the time
static double calTime(double []arr,
                      int n)
{
    double work = 0;
    for (int i = 0; i < n; i++)
        work += 1 / arr[i];

    return Math.Round(1 / work, 5);
}

// Driver Code
public static void Main ()
{
    double []arr = { 6.0, 3.0, 4.0 };
    int n = arr.Length;

    Console.Write(calTime(arr, n) +
                         " Hours");
}
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to calculate the time
function calTime(&$arr, $n)
{
    $work = 0;
    for ($i = 0; $i < $n; $i++)
        $work += 1 / $arr[$i];

    return 1 / $work;
}

// Driver Code
$arr = array(6.0, 3.0, 4.0);
$n = sizeof($arr);

echo calTime($arr, $n);
echo " Hours";

// This code is contribuuted
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript implementation
// of above approach

    // Function to calculate the time
    function calTime(arr , n)
    {
        var work = 0;
        for (i = 0; i < n; i++)
            work += 1 / arr[i];

        return 1 / work;
    }

    // Driver Code

    var arr = [ 6.0, 3.0, 4.0 ];
    var n = arr.length;

    document.write(calTime(arr, n).toFixed(5) + " Hours");

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
1.33333 Hours
```

**注意:**这里输入数组包含小时，可以是天、分钟……等等。