# 检查是否可以从(0，0)分 N 步移动到(x，y)

> 原文:[https://www . geeksforgeeks . org/check-in-n-steps-从 0-0 到 x-y-in-n-steps 是否有可能迁移/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-move-from-0-0-to-x-y-in-n-steps/)

给定点(x，y)。找出是否有可能从(0，0)到(x，y)精确 n 步移动。4 种类型的步骤是有效的，您可以从一个点(a，b)移动到(a，b+1)，(a，b-1，b)，(a+1，b)
**示例** :

```
Input: x = 0, y = 0, n = 2
Output: POSSIBLE

Input: x = 1, y = 1, n = 3 
Output: IMPOSSIBLE
```

**接近** :

> 在最短路径中，可以在|x| + |y|中从(0，0)移动到(x，y)。因此，从(0，0)到(x，y)的移动不可能少于|x| + |y|步。到达一级后可以再走两步作为(x，y) -> (x，y+1) -> (x，y)。

所以，有可能

> **n > = |x| + |y|** 和**(n-(| x |+| y |)% 2 = 0。**

以下是上述方法的实现:

## C++

```
// CPP program to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
#include <bits/stdc++.h>
using namespace std;

// Function to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
bool Arrive(int a, int b, int n)
{
    if (n >= abs(a) + abs(b) and (n - (abs(a) + abs(b))) % 2 == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int a = 5, b = 5, n = 11;

    if (Arrive(a, b, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
import java.io.*;

public class GFG {

// Function to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
static boolean Arrive(int a, int b, int n)
{
    if (n >= Math.abs(a) + Math.abs(b) && (n - (Math.abs(a) + Math.abs(b))) % 2 == 0)
        return true;

    return false;
}

// Driver code
int main()
{

    return 0;
}

    public static void main (String[] args) {

    int a = 5, b = 5, n = 11;

    if (Arrive(a, b, n))
        System.out.println( "Yes");
    else
        System.out.println( "No");
    }
}
//This code is contributed by shs..
```

## 蟒蛇 3

```
# Python3 program to check whether
# it is possible or not to move from
# (0, 0) to (x, y) in exactly n steps

# Function to check whether it is
# possible or not to move from
# (0, 0) to (x, y) in exactly n steps
def Arrive(a, b, n):

    if (n >= abs(a) + abs(b) and
       (n - (abs(a) + abs(b))) % 2 == 0):
        return True

    return False

# Driver code
a = 5
b = 5
n = 11

if (Arrive(a, b, n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Yatin Gupta    
```

## C#

```
// C# program to check whether
// it is possible or not to
// move from (0, 0) to (x, y)
// in exactly n steps
using System;

class GFG
{

// Function to check whether it
// is possible or not to move
// from (0, 0) to (x, y) in
// exactly n steps
static bool Arrive(int a, int b, int n)
{
    if (n >= Math.Abs(a) + Math.Abs(b) &&
       (n - (Math.Abs(a) + Math.Abs(b))) % 2 == 0)
        return true;

    return false;
}

// Driver code
public static void Main ()
{
    int a = 5, b = 5, n = 11;

    if (Arrive(a, b, n))
        Console.WriteLine( "Yes");
    else
        Console.WriteLine( "No");
    }
}

// This code is contributed by shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// it is possible or not to move
// from (0, 0) to (x, y) in exactly n steps

// Function to check whether it
// is possible or not to move
// from (0, 0) to (x, y) in exactly n steps
function Arrive($a, $b, $n)
{
    if ($n >= abs($a) + abs($b) and
       ($n - (abs($a) + abs($b))) % 2 == 0)
        return true;

    return false;
}

// Driver code
$a = 5; $b = 5; $n = 11;

if (Arrive($a, $b, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// JavaScript program to check whether it is
// possible or not to move from (0, 0) to (x, y)
// in exactly n steps

// Function to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
function Arrive(a, b, n)
{
    if (n >= Math.abs(a) + Math.abs(b) &&
       (n - (Math.abs(a) + Math.abs(b))) % 2 == 0)
        return true;

    return false;
}

// Driver code
var a = 5, b = 5, n = 11;

if (Arrive(a, b, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
No
```