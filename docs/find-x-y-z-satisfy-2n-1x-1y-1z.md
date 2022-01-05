# 求满足 2/n = 1/x + 1/y + 1/z 的 x，y，z

> 原文:[https://www . geesforgeks . org/find-x-y-z-submist-2n-1x-1y-1z/](https://www.geeksforgeeks.org/find-x-y-z-satisfy-2n-1x-1y-1z/)

给定 n，求 x，y，z，使 x，y，z 满足等式“2/n = 1/x+1/y+1/z”
有多个 x，y 和 z 满足等式打印其中任何一个，如果不可能，则打印-1。
示例:

```
Input : 3
Output : 3 4 12
Explanation: here 3 4 and 12 satisfy 
the given equation

Input : 7
Output : 7 8 56 
```

注意，对于 n = 1 没有解，对于 n > 1 有解 x = n，y = n+1，z = n (n+1)。
得出这个解，把 2/n 表示为 1/n+1/n，把问题化简为把 1/n 表示为两个分数之和。我们求出 1/n 和 1/(n+1)的差，得到分数 1/(n*(n+1))，这样解就是

> 2/n = 1/n + 1/(n+1) + 1/(n*(n+1))

## C++

```
// CPP program to find x y z that
// satisfies 2/n = 1/x + 1/y + 1/z...
#include <bits/stdc++.h>
using namespace std;

// function to find x y and z that
// satisfy given equation.
void printXYZ(int n)
{
    if (n == 1)
        cout << -1;

    else
        cout << "x is " << n << "\ny is "
              << n + 1 << "\nz is "
              << n * (n + 1);
}

// driver program to test the above function
int main()
{
    int n = 7;
    printXYZ(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find x y z that
// satisfies 2/n = 1/x + 1/y + 1/z...
import java.io.*;

class Sums {
    // function to find x y and z that
    // satisfy given equation.
    static void printXYZ(int n){
        if (n == 1)
            System.out.println(-1);
        else{
        System.out.println("x is "+ n);
        System.out.println("y is "+ (n+1));
        System.out.println("z is "+ (n * (n + 1)));
        }
    }
    // Driver program to test the above function
    public static void main (String[] args) {
        int n = 7;
        printXYZ(n);
    }
}

// This code is contributed by Chinmoy Lenka
```

## 蟒蛇 3

```
# Python3 code to find x y z that
# satisfies 2/n = 1/x + 1/y + 1/z...

# function to find x y and z that
# satisfy given equation.
def printXYZ( n ):
    if n == 1:
        print(-1)
    else:
        print("x is " , n )
        print("y is " ,n + 1)
        print("z is " ,n * (n + 1))

# driver code to test the above function
n = 7
printXYZ(n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find x y z that
// satisfies 2/n = 1/x + 1/y + 1/z...
using System;

class GFG
{
    // function to find x y and z that
    // satisfy given equation.
    static void printXYZ(int n)
    {
        if (n == 1)
            Console.WriteLine(-1);
        else
        {
            Console.WriteLine("x is "+ n);
            Console.WriteLine("y is "+ (n+1));
            Console.WriteLine("z is "+ (n * (n + 1)));
        }
    }

    // Driver program
    public static void Main ()
    {
        int n = 7;
        printXYZ(n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find x y z that
// satisfies 2/n = 1/x + 1/y + 1/z...

// function to find x y and z that
// satisfy given equation.
function printXYZ($n)
{
    if ($n == 1)
        echo -1;

    else
        echo "x is " , $n , "\ny is "
                , $n + 1 , "\nz is ",
                     $n * ($n + 1);
}

    // Driver Code
    $n = 7;
    printXYZ($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find x y z that
// satisfies 2/n = 1/x + 1/y + 1/z...

// function to find x y and z that
// satisfy given equation.
function printXYZ(n)
{
    if (n == 1)
        document.write(-1);

    else
        document.write("x is " + n + "<br>y is "
              + (n + 1) + "<br>z is "
              + n * (n + 1));
}

// driver program to test the above function
    let n = 7;
    printXYZ(n);

</script>
```

**输出:**

```
x is 7
y is 8
z is 56
```

**时间复杂度:** O(1)
**交替解**
我们可以写成 2/n = 1/n + 1/n，再进一步写成 2/n = 1/n + 1/2n + 1/2n。