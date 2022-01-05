# 计算四边形角度的程序

> 原文:[https://www . geesforgeks . org/program-to-find-a-angles-of-a-四边形/](https://www.geeksforgeeks.org/program-to-find-the-angles-of-a-quadrilateral/)

假设一个四边形的所有角度都在具有公共差“d”的 AP 中，那么任务就是找到所有的角度。
**例:**

```
Input: d = 10
Output: 75, 85, 95, 105

Input: d = 20
Output: 60, 80, 100, 120
```

**进场:**

> 我们知道四边形的角度在α，并且有一个共同的区别“d”。
> 所以，如果我们假设第一个角度是‘a’，那么其他角度可以计算为，
> ‘a+d’‘a+2d’和‘a+3d’
> 并且，从四边形的性质来看，四边形的所有角度之和是 360°。所以，
> (a)+(a+d)+(a+2 * d)+(a+3 * d)= 360
> 4 * a+6 * d = 360
> a =(360 –( 6 * d))/4
> 其中‘a’是开头假设的角度，‘d’是共同的区别。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Driver code
int main()
{
    int d = 10;
    double a;

    // according to formula derived above
    a = (double)(360 - (6 * d)) / 4;

    // print all the angles
    cout << a << ", " << a + d << ", " << a + (2 * d)
         << ", " << a + (3 * d) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation of the approach

import java.io.*;

class GFG {

// Driver code

    public static void main (String[] args) {
            int d = 10;
    double a;

    // according to formula derived above
    a = (double)(360 - (6 * d)) / 4;

    // print all the angles
    System.out.print( a + ", " + (a + d) + ", " + (a + (2 * d))
        + ", " + (a + (3 * d)));
    }
}
//This code is contributed
//by  inder_verma
```

## 计算机编程语言

```
# Python implementation
# of the approach
d = 10
a = 0.0

# according to formula
# derived above
a=(360 - (6 * d)) / 4

# print all the angles
print(a,",", a + d, ",", a + 2 * d,
        ",", a + 3 * d, sep = ' ')

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Driver code
public static void Main ()
{
    int d = 10;
    double a;

    // according to formula derived above
    a = (double)(360 - (6 * d)) / 4;

    // print all the angles
    Console.WriteLine( a + ", " + (a + d) +
                           ", " + (a + (2 * d)) +
                           ", " + (a + (3 * d)));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Driver code
$d = 10;

// according to formula
// derived above
$a = (360 - (6 * $d)) / 4 ;

// print all the angles
echo $a, ", ", $a + $d , ", ",
     $a + (2 * $d), ", ", $a + (3 * $d);

// This code is contributed
// by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Driver code
var d = 10;
var a;

// according to formula derived above
a = parseInt((360 - (6 * d)) / 4);

// print all the angles
document.write( a + ", " + (a + d) + ", " + (a + (2 * d))
    + ", " + (a + (3 * d)));

</script>
```

**Output:** 

```
75, 85, 95, 105
```