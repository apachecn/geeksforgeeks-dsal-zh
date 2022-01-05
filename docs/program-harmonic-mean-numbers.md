# 调和平均数程序

> 原文:[https://www . geesforgeks . org/program-harmonic-mean-numbers/](https://www.geeksforgeeks.org/program-harmonic-mean-numbers/)

给定一组元素，求数字的调和平均数。
示例:

```
Input : arr[] = {2.0, 1.0}
Output : 1.3333
Harmonic mean = 2/(1/2.0 + 1/1.0)
             = (2 * 2)/3
             = 1.333

Input : arr[] = {13.5, 14.5, 14.8, 15.2, 16.1}
Output : 14.7707
```

> 当需要速率平均值时，使用调和平均值，公式如下。
> n 个数字的调和平均值 x <sub>1</sub> ，x <sub>2</sub> ，
> x <sub>3</sub> 。。。，x <sub>n</sub> 可以写成如下。
> 调和平均数= n**/**((1/x<sub>1</sub>)+(1/x<sub>2</sub>)+(1/x<sub>3</sub>)+。。。+ (1/x <sub>n</sub> )

下面是调和平均值的实现。

## C++

```
// CPP program to find harmonic mean of numbers.
#include <bits/stdc++.h>
using namespace std;

// Function that returns harmonic mean.
float harmonicMean(float arr[], int n)
{
    // Declare sum variables and initialize
    // with zero.
    float sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + (float)1 / arr[i];

    return (float)n/sum;
}

// Driver code
int main()
{
    float arr[] = { 13.5, 14.5, 14.8, 15.2, 16.1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << harmonicMean(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find harmonic
// mean of numbers.
import java.io.*;

class GFG {

    // Function that returns harmonic mean.
    static float harmonicMean(float arr[], int n)
    {
        // Declare sum variables and
        // initialize with zero
        float sum = 0;
        for (int i = 0; i < n; i++)
            sum = sum + (float)1 / arr[i];

        return (float)n/sum;
    }

    // Driver code
    public static void main(String args[])
    {
        float arr[]= { 13.5f, 14.5f, 14.8f,
                      15.2f, 16.1f };
        int n = arr.length;
        System.out.println(harmonicMean(arr, n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find harmonic
# mean of numbers.

# Function that returns harmonic mean.
def harmonicMean(arr, n) :

    # Declare sum variables and
    # initialize with zero.
    sm = 0
    for i in range(0, n) :
        sm = sm + (1) / arr[i];

    return n / sm

# Driver code
arr = [ 13.5, 14.5, 14.8, 15.2, 16.1 ];
n = len(arr)
print(harmonicMean(arr, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find harmonic
// mean of numbers.
using System;

class GFG {

    // Function that returns harmonic mean.
    static float harmonicMean(float[] arr, int n)
    {
        // Declare sum variables and
        // initialize with zero
        float sum = 0;
        for (int i = 0; i < n; i++)
            sum = sum + (float)1 / arr[i];

        return (float)n / sum;
    }

    // Driver code
    public static void Main()
    {
        float[] arr = { 13.5f, 14.5f, 14.8f,
                        15.2f, 16.1f };
        int n = arr.Length;
        Console.WriteLine(harmonicMean(arr, n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// harmonic mean of numbers.

// Function that returns
// harmonic mean.
function harmonicMean($arr, $n)
{

    // Declare sum variables and
    // initialize with zero
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + (float)
               (1 / $arr[$i]);

    return (float)($n / $sum);
}

// Driver code
$arr = array(13.5, 14.5, 14.8, 15.2, 16.1);
$n = sizeof($arr);
echo(harmonicMean($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find harmonic mean of numbers.

// Function that returns harmonic mean.
function harmonicMean(arr, n)
{
    // Declare sum variables and initialize
    // with zero.
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum = sum + (1 / arr[i]);

    return n/sum;
}

// Driver code

let arr = [ 13.5, 14.5, 14.8, 15.2, 16.1 ];
let n = arr.length;
document.write(harmonicMean(arr, n));

</script>
```

**输出:**

```
14.7707
```

**如果给我们元素及其频率呢？**
如果给我们 n 个数字，每个数字都有一些频率，那么我们简单地使用公式
调和平均值=(频率-和)/((f<sub>1</sub>/x<sub>1</sub>)+(f<sub>2</sub>/x<sub>2</sub>)+(f<sub>3</sub>/x<sub>3</sub>)+。。。+(f<sub>n</sub>/x<sub>n</sub>)
其中 f <sub>1</sub> ，f <sub>2</sub> ，f <sub>3</sub> 。。。，f <sub>n</sub> 为元素的频率，x <sub>1</sub> ， <sub>2</sub> ，x <sub>3</sub> ，。。。，x <sub>n</sub> 是数组的元素。
频率-总和= f<sub>1</sub>+f<sub>2</sub>+f<sub>3</sub>。。。，f <sub>n</sub>
例:

```
Input : num[] = {13, 14, 15, 16, 17}
        freq[] = {2, 5, 13, 7, 3}
Output : 15.0631
```

## C++

```
// C++ program to find harmonic mean.
#include <bits/stdc++.h>
using namespace std;
// Function that returns harmonic mean.
float harmonicMean(int arr[], int freq[], int n)
{
    float sum = 0, frequency_sum = 0;
    for (int i = 0; i < n; i++) {
        sum = sum + (float)freq[i] / arr[i];
        frequency_sum  = frequency_sum  + freq[i];
    }
    return frequency_sum / sum;
}

// Driver code
int main()
{
    int num[] = { 13, 14, 15, 16, 17 };
    int freq[] = { 2, 5, 13, 7, 3 };
    int n = sizeof(num) / sizeof(num[0]);
    cout << harmonicMean(num, freq, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find harmonic mean.

class GFG {

    // Function that returns harmonic mean.
    static float harmonicMean(int arr[], int freq[],
                              int n)
    {
        float sum = 0, frequency_sum = 0;
        for (int i = 0; i < n; i++) {
            sum = sum + (float)freq[i] / arr[i];
            frequency_sum  = frequency_sum  + freq[i];
        }
        return (frequency_sum / sum);
    }

    // Driver code
    public static void main(String args[])
    {
        int num[] = { 13, 14, 15, 16, 17 };
        int freq[] = { 2, 5, 13, 7, 3 };
        int n = num.length;
        System.out.println(harmonicMean(num, freq, n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find harmonic mean.

# Function that returns harmonic mean.
def harmonicMean(arr, freq, n) :
    sm = 0
    frequency_sum = 0
    for i in range(0,n) :
        sm = sm + freq[i] / arr[i]
        frequency_sum  = frequency_sum  + freq[i]

    return (round(frequency_sum / sm,4))

# Driver code
num = [ 13, 14, 15, 16, 17 ]
freq = [ 2, 5, 13, 7, 3 ]
n = len(num)
print (harmonicMean(num, freq, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find harmonic mean.
using System;

class GFG {

    // Function that returns harmonic mean.
    static float harmonicMean(int[] arr, int[] freq,
                                              int n)
    {
        float sum = 0, frequency_sum = 0;
        for (int i = 0; i < n; i++) {
            sum = sum + (float)freq[i] / arr[i];
            frequency_sum = frequency_sum + freq[i];
        }
        return (frequency_sum / sum);
    }

    // Driver code
    public static void Main()
    {
        int[] num = { 13, 14, 15, 16, 17 };
        int[] freq = { 2, 5, 13, 7, 3 };
        int n = num.Length;
        Console.WriteLine(harmonicMean(num, freq, n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// harmonic mean.

// Function that returns
// harmonic mean.
function harmonicMean($arr, $freq, $n)
{
    $sum = 0; $frequency_sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $sum = $sum + (float)
               ($freq[$i] / $arr[$i]);
        $frequency_sum = $frequency_sum +
                                $freq[$i];
    }
    return ($frequency_sum / $sum);
}

// Driver code
$num = array(13, 14, 15, 16, 17);
$freq = array(2, 5, 13, 7, 3);
$n = sizeof($num);
echo(harmonicMean($num, $freq, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find harmonic mean.

// Function that returns harmonic mean.
function harmonicMean(arr, freq, n)
{
    let sum = 0, frequency_sum = 0;
    for (let i = 0; i < n; i++) {
        sum = sum + (freq[i] / arr[i]);
        frequency_sum  = frequency_sum  + freq[i];
    }
    return frequency_sum / sum;
}

// Driver code
let num = [ 13, 14, 15, 16, 17 ];
let freq = [ 2, 5, 13, 7, 3 ];
let n = num.length;
document.write(harmonicMean(num, freq, n));

</script>
```

**输出:**

```
15.0631
```

**调和平均数的数字使用** ***调和 _ 平均数()*** **在 Python 中:**
简单 Python 程序查找调和平均数使用*调和 _ 平均数()*函数。

## 蟒蛇 3

```
#'harmonic_mean()' new function added in 'Python3.6' onwards.
#Program calculates Harmonic Mean using harmonic_mean()

#imports Python statistics library
import statistics
def harmonic_mean():
    list= [13.5, 14.5, 14.8, 15.2, 16.1]
    print(statistics.harmonic_mean(list))

#Driver code
harmonic_mean()

#This code is contributed by 'Abhishek Agrawal'.
```

```
Output: 14.770680729373778
```

本文由 [**达曼德拉·库马尔**](https://auth.geeksforgeeks.org/profile.php?user=dharammnnit) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。