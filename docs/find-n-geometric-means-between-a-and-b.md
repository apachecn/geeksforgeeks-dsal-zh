# 求 A 和 B 之间的 N 个几何平均数

> 原文:[https://www . geesforgeks . org/find-n-geometric-means-介于-a 和-b 之间/](https://www.geeksforgeeks.org/find-n-geometric-means-between-a-and-b/)

给定三个整数 A、B 和 N，任务是找到 A 和 B 之间的 N 个几何平均值。我们基本上需要在一个[几何级数](https://www.geeksforgeeks.org/find-nth-term-geometric-progression-series/)中插入 N 个项。其中 A 和 B 是第一项和最后一项。
**例:**

```
Input :  A = 2  B = 32  N = 3
Output : 4 8 16
the geometric progression series as 2,
4, 8, 16 , 32

Input : A = 3 B = 81 N = 2
Output : 9 27
```

**进场:**
让 A <sub>1</sub> ，G <sub>2</sub> ，G <sub>3</sub> ，G <sub>4</sub> ……G <sub>n</sub> 为两个给定数字 A 和 B 之间的 N 个几何平均数，然后 A、G <sub>1</sub> ，G <sub>2</sub> …..G <sub>n</sub> ，B 将处于几何级数。
所以 B = (N+2) <sup>几何级数的第</sup>项。
那么这里 R 是公比
B = A * R<sup>N+1</sup>R<sup>N+1</sup>= B/A
T30】R =(B/A)<sup>1/(N+1)</sup>T34】现在我们有了 R
的值，也有了第一项 A
G <sub>1</sub> 的值= AR <sup>(B/A)<sup>2/(N+1)</sup>T50】G<sub>3</sub>= AR<sup>3</sup>= A *(B/A)<sup>3/(N+1)</sup>
。
。
。
**G<sub>N</sub>= AR<sup>N</sup>= A *(B/A)<sup>N/(N+1)</sup>**</sup> 

## C++

```
// C++ program to find n geometric means
// between A and B
#include <bits/stdc++.h>
using namespace std;

// Prints N geometric means between
// A and B.
void printGMeans(int A, int B, int N)
{
    // calculate common ratio(R)
    float R = (float)pow(float(B / A),
                  1.0 / (float)(N + 1));

    // for finding N the Geometric
    // mean between A and B
    for (int i = 1; i <= N; i++)
        cout << A * pow(R, i) <<" ";   
}

// Driver code to test above
int main()
{
    int A = 3, B = 81, N = 2;
    printGMeans(A, B, N);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to illustrate
// n geometric mean between
// A and B
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // insert function for calculating the means
    static void printGMeans(int A, int B, int N)
    {      
        // Finding the value of R Common ration
        float R = (float)Math.pow((float)(B / A),
                           1.0 / (float)(N + 1));

        // for finding N the Geometric
        // mean between A and B
        for (int i = 1; i <= N; i++)
          System.out.print(A * Math.pow(R, i) + " ");

    }

    // Driver code
    public static void main(String args[])
    {
        int A = 3, B = 81, N = 2;
        printGMeans(A, B, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# n geometric means
# between A and B
import math

# Prints N geometric means
# between A and B.
def printGMeans(A, B, N):

    # calculate
    # common ratio(R)
    R = (math.pow((B / A),
          1.0 / (N + 1)));

    # for finding N the
    # Geometric mean
    # between A and B
    for i in range(1, N + 1):
        print(int(A * math.pow(R, i)),
                           end = " ");

# Driver Code
A = 3;
B = 81;
N = 2;
printGMeans(A, B, N);

# This code is contributed
# by mits
```

## C#

```
// C# program to illustrate
// n geometric mean between
// A and B
using System;

public class GFG {

    // insert function for calculating the means
    static void printGMeans(int A, int B, int N)
    {

        // Finding the value of R Common ration
        float R = (float)Math.Pow((float)(B / A),
                        1.0 / (float)(N + 1));

        // for finding N the Geometric
        // mean between A and B
        for (int i = 1; i <= N; i++)
            Console.Write(A * Math.Pow(R, i) + " ");

    }

    // Driver code
    public static void Main()
    {
        int A = 3, B = 81, N = 2;

        printGMeans(A, B, N);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n geometric means
// between A and B

// Pr$s N geometric means
// between A and B.
function printGMeans($A, $B, $N)
{

    // calculate common ratio(R)
    $R = pow(($B / $A),
             1.0 / ($N + 1));

    // for finding N the Geometric
    // mean between A and B
    for ($i = 1; $i <= $N; $i++)
        echo $A * pow($R, $i) ," ";
}

    // Driver Code
    $A = 3;
    $B = 81;
    $N = 2;
    printGMeans($A, $B, $N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript program to illustrate
// n geometric mean between
// A and B

    // insert function for calculating the means
    function printGMeans(A, B, N)
    {      
        // Finding the value of R Common ration
        let R = Math.pow((B / A),
                           1.0 / (N + 1));

        // for finding N the Geometric
        // mean between A and B
        for (let i = 1; i <= N; i++)
          document.write(A * Math.pow(R, i) + " ");

    }

// Driver Code
        let A = 3, B = 81, N = 2;
        printGMeans(A, B, N);

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
9 27 
```