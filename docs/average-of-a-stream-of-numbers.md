# 一串数字的平均值

> 原文:[https://www . geesforgeks . org/平均数字流/](https://www.geeksforgeeks.org/average-of-a-stream-of-numbers/)

难度等级:初出茅庐
给定一个数字流，打印该流在每个点的平均值(或均值)。例如，让我们将该流视为 10、20、30、40、50、60……

```
  Average of 1 numbers is 10.00
  Average of 2 numbers is 15.00
  Average of 3 numbers is 20.00
  Average of 4 numbers is 25.00
  Average of 5 numbers is 30.00
  Average of 6 numbers is 35.00
  ..................
```

要打印一个流的平均值，我们需要知道当一个新的数字被添加到流中时，如何找到平均值。要做到这一点，我们只需要统计到目前为止在数据流中看到的数字、以前的平均值和新的数字。设 *n* 为计数， *prev_avg* 为前一平均值，x 为新加入的数。包含 *x* 数后的平均值可以写成 *(prev_avg*n + x)/(n+1)* 。

## C++

```
#include <iostream>
using namespace std;

// Returns the new average after including x
float getAvg(float prev_avg, int x, int n)
{
    return (prev_avg * n + x) / (n + 1);
}

// Prints average of a stream of numbers
void streamAvg(float arr[], int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++) {
        avg = getAvg(avg, arr[i], i);
        cout <<"Average of " <<i+1 << " numbers is " << avg << endl;
    }
    return;
}

// Driver program to test above functions
int main()
{
    float arr[] = { 10, 20, 30, 40, 50, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);
    streamAvg(arr, n);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>

// Returns the new average after including x
float getAvg(float prev_avg, int x, int n)
{
    return (prev_avg * n + x) / (n + 1);
}

// Prints average of a stream of numbers
void streamAvg(float arr[], int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++) {
        avg = getAvg(avg, arr[i], i);
        printf("Average of %d numbers is %f \n", i + 1, avg);
    }
    return;
}

// Driver program to test above functions
int main()
{
    float arr[] = { 10, 20, 30, 40, 50, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);
    streamAvg(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find average
// of a stream of numbers
class GFG {

    // Returns the new average after including x
    static float getAvg(float prev_avg, float x, int n)
    {
        return (prev_avg * n + x) / (n + 1);
    }

    // Prints average of a stream of numbers
    static void streamAvg(float arr[], int n)
    {
        float avg = 0;
        for (int i = 0; i < n; i++)
        {
            avg = getAvg(avg, arr[i], i);
            System.out.printf("Average of %d numbers is %f \n",
                                                   i + 1, avg);
        }
        return;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        float arr[] = { 10, 20, 30, 40, 50, 60 };
        int n = arr.length;
        streamAvg(arr, n);
    }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Returns the new average
# after including x
def getAvg(prev_avg, x, n):
    return ((prev_avg *
             n + x) /
            (n + 1));

# Prints average of
# a stream of numbers
def streamAvg(arr, n):
    avg = 0;
    for i in range(n):
        avg = getAvg(avg, arr[i], i);
        print("Average of ", i + 1,
              " numbers is ", avg);

# Driver Code
arr = [10, 20, 30,
       40, 50, 60];
n = len(arr);
streamAvg(arr, n);

# This code is contributed
# by mits
```

## C#

```
// C# program to find average
// of a stream of numbers
using System;

class GFG
{

    // Returns the new average
    // after including x
    static float getAvg(float prev_avg,
                        float x, int n)
    {
        return (prev_avg * n + x) / (n + 1);
    }

    // Prints average of
    // a stream of numbers
    static void streamAvg(float[] arr,
                          int n)
    {
        float avg = 0;
        for (int i = 0; i < n; i++)
        {
            avg = getAvg(avg, arr[i], i);
            Console.WriteLine("Average of {0} " +
                                "numbers is {1}",
                                     i + 1, avg);
        }
        return;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        float[] arr = {10, 20, 30,
                       40, 50, 60};
        int n = arr.Length;
        streamAvg(arr, n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Average of
// a stream of numbers

// Returns the new average
// after including x
function getAvg($prev_avg, $x, $n)
{
    return ($prev_avg * $n + $x) /
                        ($n + 1);
}

// Prints average of a
// stream of numbers
function streamAvg($arr, $n)
{
    $avg = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $avg = getAvg($avg, $arr[$i], $i);
        echo "Average of ",$i + 1, "numbers is "
                                    ,$avg,"\n";
    }
    return;
}

    // Driver Code
    $arr = array(10, 20, 30, 40, 50, 60);
    $n = sizeof($arr);
    streamAvg($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// javascript program to find average
// of a stream of numbers

// Returns the new average after including x
function getAvg( prev_avg,  x,  n)
{
    return (prev_avg * n + x) / (n + 1);
}

// Prints average of a stream of numbers
function streamAvg( arr,  n)
{
    let avg = 0;
    for (let i = 0; i < n; i++) {
        avg = getAvg(avg, arr[i], i);
       document.write("Average of "+(i + 1) +" numbers is "+  avg.toFixed(6) + "<br/>");
    }
    return;
}

// Driver program to test above functions
    let arr = [10, 20, 30, 40, 50, 60 ];
    let n = arr.length;
    streamAvg(arr, n);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Average of 1 numbers is 10.000000 
Average of 2 numbers is 15.000000 
Average of 3 numbers is 20.000000 
Average of 4 numbers is 25.000000 
Average of 5 numbers is 30.000000 
Average of 6 numbers is 35.000000 
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

上述函数 getAvg()可以使用以下更改进行优化。我们可以通过使用静态变量来避免使用 prev_avg 和元素数量(假设对流的平均值只调用这个函数)。以下是优化版本。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Returns the new average after including x
float getAvg(int x)
{
    static int sum, n;

    sum += x;
    return (((float)sum) / ++n);
}

// Prints average of a stream of numbers
void streamAvg(float arr[], int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++)
    {
        avg = getAvg(arr[i]);
        cout<<"Average of "<<i+1<<" numbers is "<<fixed<<setprecision(1)<<avg<<endl;
    }
    return;
}

// Driver code
int main()
{
    float arr[] = { 10, 20, 30, 40, 50, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);
    streamAvg(arr, n);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>

// Returns the new average after including x
float getAvg(int x)
{
    static int sum, n;

    sum += x;
    return (((float)sum) / ++n);
}

// Prints average of a stream of numbers
void streamAvg(float arr[], int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++) {
        avg = getAvg(arr[i]);
        printf("Average of %d numbers is %f \n", i + 1, avg);
    }
    return;
}

// Driver program to test above functions
int main()
{
    float arr[] = { 10, 20, 30, 40, 50, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);
    streamAvg(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to return
// Average of a stream of numbers
class GFG
{
static int sum, n;

// Returns the new average
// after including x
static float getAvg(int x)
{
    sum += x;
    return (((float)sum) / ++n);
}

// Prints average of a
// stream of numbers
static void streamAvg(float[] arr,
                      int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++)
    {
        avg = getAvg((int)arr[i]);
        System.out.println("Average of "+ (i + 1) +
                           " numbers is " + avg);
    }
    return;
}

// Driver Code
public static void main(String[] args)
{
    float[] arr = new float[]{ 10, 20, 30,
                               40, 50, 60 };
    int n = arr.length;
    streamAvg(arr, n);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Returns the new average
# after including x
def getAvg(x, n, sum):
    sum = sum + x;
    return float(sum) / n;

# Prints average of a
# stream of numbers
def streamAvg(arr, n):
    avg = 0;
    sum = 0;
    for i in range(n):
        avg = getAvg(arr[i], i + 1, sum);
        sum = avg * (i + 1);
        print("Average of ", end = "");
        print(i + 1, end = "");
        print(" numbers is ", end = "");
        print(avg);
    return;

# Driver Code
arr= [ 10, 20, 30,
       40, 50, 60 ];
n = len(arr);
streamAvg(arr,n);

# This code is contributed by mits
```

## C#

```
using System;

class GFG
{
static int sum, n;

// Returns the new average
// after including x
static float getAvg(int x)
{

    sum += x;
    return (((float)sum) / ++n);
}

// Prints average of a
// stream of numbers
static void streamAvg(float[] arr, int n)
{
    float avg = 0;
    for (int i = 0; i < n; i++)
    {
        avg = getAvg((int)arr[i]);
        Console.WriteLine("Average of {0} numbers " +
                             "is {1}", (i + 1), avg);
    }
    return;
}

// Driver Code
static int Main()
{
    float[] arr = new float[]{ 10, 20, 30,
                               40, 50, 60 };
    int n = arr.Length;
    streamAvg(arr, n);

    return 0;
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Returns the new average
// after including x
function getAvg($x)
{
    static $sum;
    static $n;
    $sum += $x;
    return (((float)$sum) / ++$n);
}

// Prints average of
// a stream of numbers
function streamAvg($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        $avg = getAvg($arr[$i]);
        echo "Average of " . ($i + 1) .
             " numbers is ".$avg." \n";
    }
    return;
}

// Driver Code
$arr = array(10, 20, 30,
             40, 50, 60);
$n = sizeof($arr) / sizeof($arr[0]);
streamAvg($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to return
// Average of a stream of numbers

    var sum=0, n=0;

    // Returns the new average
    // after including x
    function getAvg(x) {
        sum += x;
        n++;
        return (sum / n);
    }

    // Prints average of a
    // stream of numbers
    function streamAvg( arr , m) {
        var avg = 0;
        for (i = 0; i < m; i++) {
            avg = getAvg(parseInt(arr[i]));
            document.write("Average of " + (i + 1) + " numbers is " + avg.toFixed(1)+"<br/>");
        }
        return;
    }

    // Driver Code

        var arr =  [ 10, 20, 30, 40, 50, 60 ];
        var m = arr.length;
        streamAvg(arr, m);

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Average of 1 numbers is 10.0
Average of 2 numbers is 15.0
Average of 3 numbers is 20.0
Average of 4 numbers is 25.0
Average of 5 numbers is 30.0
Average of 6 numbers is 35.0
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

感谢 Abhijeet Deshpande 提出这个优化版本。
**相关文章:**
[求一个数组平均值的程序(迭代和递归)](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)
如发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息。