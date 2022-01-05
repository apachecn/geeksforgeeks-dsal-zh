# 等边三角形相遇所需时间

> 原文:[https://www.geeksforgeeks.org/time-meet-animals/](https://www.geeksforgeeks.org/time-meet-animals/)

给定等边三角形边的长度，以及标记在三角形顶点上的每只动物的速度，找出它们相遇的时间，如果它们开始向右移动，形成一条轨迹。

![3](img/b7bf62d57c7abc42d9b5d32a6f4cea04.png)

**例:**

```
Input : s = 2, v = 5
Output : 0.266667

Input : s = 11, v = 556
Output : 0.013189
```

**进场:**
要求出动物相遇所用的总时间，只需取 A 除以两个顶点相互靠近的初始速度。拾取任意两个顶点，可以看到第一个点以速度 v 向第二个点的方向移动，而第二个点向第一个点的方向移动(只需沿着其中一个三角形边取分量)。
参考: [StackExchange](https://math.stackexchange.com/questions/1081920/when-do-3-particles-on-the-vertices-of-an-equilateral-triangle-meet/1081921)

## C++

```
// CPP code to find time
// taken by animals to meet
#include <bits/stdc++.h>
using namespace std;

// function to calculate time to meet
void timeToMeet(double s, double v){

     double V = 3 * v / 2;

     double time = s / V;

     cout << time;
}

// Driver Code
int main(void) {

    double s = 25, v = 56;

    timeToMeet(s, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find time taken by animals
// to meet
import java.io.*;

public class GFG {

    // function to calculate time to meet
    static void timeToMeet(double s, double v){

        double V = 3 * v / 2;

        double time = s / V;

        System.out.println((float)time);
    }

    // Driver Code
    static public void main (String[] args)
    {

        double s = 25, v = 56;

        timeToMeet(s, v);
    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find time
# taken by animals to meet

# function to calculate
# time to meet
def timeToMeet(s, v):
    V = 3 * v / 2;

    time = s / V;

    print(time);

# Driver Code
s = 25;
v = 56;

timeToMeet(s, v);

# This code is contributed by mits
```

## C#

```
// C# code to find time
// taken by animals to meet
using System;

public class GFG {

    // function to calculate time to meet
    static void timeToMeet(double s, double v){

        double V = 3 * v / 2;

        double time = s / V;

        Console.WriteLine((float)time);
    }

    // Driver Code
    static public void Main ()
    {

        double s = 25, v = 56;

        timeToMeet(s, v);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find time
// taken by animals to meet

// function to calculate
// time to meet
function timeToMeet($s, $v)
{

    $V = 3 * $v / 2;
    $time = $s / $V;
    echo $time;
}

    // Driver Code
    $s = 25; $v = 56;
    timeToMeet($s, $v);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript code to find time taken by animals
// to meet

    // function to calculate time to meet
    function timeToMeet(s , v) {

        var V = 3 * v / 2;

        var time = s / V;

        document.write( time.toFixed(6));
    }

    // Driver Code

        var s = 25, v = 56;

        timeToMeet(s, v);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
0.297619
```