# 检查是否可以通过给定的跳跃从(a，0)移动到(b，0)

> 原文:[https://www . geeksforgeeks . org/check-如果有可能通过给定的跳转从 a-0 移动到 B- 0/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-move-from-a-0-to-b-0-with-given-jumps/)

给定两点，即(a，0)到(b，0)。任务是检查是否有可能从(a，0)移动到(b，0)。一个可以移动为(a，0)，(a+x，0)，(a+x+1，0)，(a，2*x，0)，(a，2*x+1，0)……

**示例:**

```
Input: a = 3, x = 10, b = 4
Output: No

Input: a = 3, x = 2, b = 5
Output: Yes
```

**方法:**在下列情况下，答案是可能的

> 1.  **a + n*x = b，**其中 n 为非负整数。
> 2.  **a + n*x + 1 = b** 其中 n 为正整数。
> 
> 所以，
> (b–a)/x 是整数或者(b–a–1)/x 是整数
> (b–a)% x = 0 或者(b–a–1)% x = 0

下面是上述方法的实现:

## C++

```
// CPP program to move form
// (a, 0) to (b, 0) with given jumps
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
bool Move(int a, int x, int b)
{
    if ((((b - a) % x == 0) || ((b - a - 1) % x == 0) && a + 1 != b) && b >= a)
        return true;

    return false;
}

// Driver code
int main()
{
    int a = 3, x = 2, b = 7;

    // function call
    if (Move(a, x, b))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to move form
// (a, 0) to (b, 0) with given jumps
import java.io.*;

class GFG {

// Function to check if it is possible
static boolean Move(int a, int x, int b)
{
    if ((((b - a) % x == 0) || ((b - a - 1) % x == 0) && a + 1 != b) && b >= a)
        return true;

    return false;
}

// Driver code
    public static void main (String[] args) {
            int a = 3, x = 2, b = 7;

    // function call
    if (Move(a, x, b))
        System.out.println( "Yes");
    else
        System.out.println( "No");
    }
}
//This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to move form
# (a, 0) to (b, 0) with given jumps

# Function to check if it
# is possible
def Move(a, x, b):

    if ((((b - a) % x == 0) or
         ((b - a - 1) % x == 0) and
           a + 1 != b) and b >= a):
        return True

    return False

# Driver code
if __name__ == "__main__":
    a = 3
    x = 2
    b = 7

    # function call
    if (Move(a, x, b)):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to move form
// (a, 0) to (b, 0) with given jumps
using System;

class GFG
{

// Function to check if it is possible
static bool Move(int a, int x, int b)
{
    if ((((b - a) % x == 0) ||
         ((b - a - 1) % x == 0) &&
           a + 1 != b) && b >= a)
        return true;

    return false;
}

// Driver code
public static void Main ()
{
    int a = 3, x = 2, b = 7;

    // function call
    if (Move(a, x, b))
        Console.WriteLine( "Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to move form
// (a, 0) to (b, 0) with given jumps

// Function to check if it is possible
function Move($a, $x, $b)
{
    if (((($b - $a) % $x == 0) ||
         (($b - $a - 1) % $x == 0) &&
           $a + 1 != $b) && $b >= $a)
        return true;

    return false;
}

// Driver code
$a = 3; $x = 2; $b = 7;

// function call
if (Move($a, $x, $b))
    echo "Yes";
else
    echo"No";

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>
// Javascript program to move form
// (a, 0) to (b, 0) with given jumps

    // Function to check if it is possible
    function Move(a,x,b)
    {
        if ((((b - a) % x == 0) || ((b - a - 1) % x == 0)
             && a + 1 != b) && b >= a)
            return true;

        return false;
    }

    // Driver code
    let a = 3, x = 2, b = 7;
    // function call
    if (Move(a, x, b))
        document.write( "Yes");
    else
        document.write( "No");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Yes
```