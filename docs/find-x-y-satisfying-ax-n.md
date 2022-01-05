# 通过= n 找到满足 ax +的 x 和 y

> 原文:[https://www.geeksforgeeks.org/find-x-y-satisfying-ax-n/](https://www.geeksforgeeks.org/find-x-y-satisfying-ax-n/)

给定 a、b 和 n，找到满足 ax + by = n 的 x 和 y，打印满足公式
**的 x 和 y 中的任何一个，示例:**

```
Input : n=7 a=2 b=3
Output : x=2, y=1 
Explanation: here x and y satisfies the equation

Input : 4 2 7 
Output : No solution
```

我们可以使用[线性丢番图方程](https://www.geeksforgeeks.org/linear-diophantine-equations/)来检查是否存在任何解，但是这里我们需要找出这个方程的解，所以我们可以简单地迭代从 0 到 n 的所有可能的值，因为对于这个给定的方程，它不能超过 n。所以用纸和笔解这个方程得到 **y=(n-ax)/b** ，同样我们得到另一个数为 **x=(n-by)/a** 。如果没有一个值满足等式，最后我们打印“无解”

## C++

```
// CPP program to find solution of ax + by = n
#include <bits/stdc++.h>
using namespace std;

// function to find the solution
void solution(int a, int b, int n)
{
    // traverse for all possible values
    for (int i = 0; i * a <= n; i++) {

        // check if it is satisfying the equation
        if ((n - (i * a)) % b == 0) {
            cout << "x = " << i << ", y = "
                 << (n - (i * a)) / b;
            return;
        }
    }

    cout << "No solution";
}

// driver program to test the above function
int main()
{
    int a = 2, b = 3, n = 7;
    solution(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find solution
// of ax + by = n
import java.io.*;

class GfG {

    // function to find the solution
    static void solution(int a, int b, int n)
    {
        // traverse for all possible values
        for (int i = 0; i * a <= n; i++)
        {

            // check if it is satisfying the equation
            if ((n - (i * a)) % b == 0)
            {
                System.out.println("x = " + i +
                                   ", y = " +
                                   (n - (i * a)) / b);

                return ;
            }
        }

        System.out.println("No solution");
    }

    public static void main (String[] args)
    {
        int a = 2, b = 3, n = 7;
        solution(a, b, n);

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 code to find solution of
# ax + by = n

# function to find the solution
def solution (a, b, n):

    # traverse for all possible values
    i = 0
    while i * a <= n:

        # check if it is satisfying
        # the equation
        if (n - (i * a)) % b == 0:
            print("x = ",i ,", y = ",
               int((n - (i * a)) / b))
            return 0
        i = i + 1

    print("No solution")

# driver program to test the above function
a = 2
b = 3
n = 7
solution(a, b, n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find solution
// of ax + by = n
using System;

class GfG {

    // function to find the solution
    static void solution(int a, int b, int n)
    {

        // traverse for all possible values
        for (int i = 0; i * a <= n; i++)
        {

            // check if it is satisfying the
            // equation
            if ((n - (i * a)) % b == 0)
            {
                Console.Write("x = " + i +
                                ", y = " +
                        (n - (i * a)) / b);

                return ;
            }
        }

        Console.Write("No solution");
    }

    // Driver code
    public static void Main ()
    {
        int a = 2, b = 3, n = 7;
        solution(a, b, n);

    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// solution of ax + by = n

// function to find the solution
function solution($a, $b, $n)
{
    // traverse for all possible values
    for ($i = 0; $i * $a <= $n; $i++)
    {

        // check if it is satisfying
        // the equation
        if (($n - ($i * $a)) % $b == 0)
        {
            echo "x = " , $i , ", y = " ,
                   ($n - ($i * $a)) / $b;
            return;
        }
    }

    echo "No solution";
}

// Driver Code
$a = 2; $b = 3; $n = 7;
solution($a, $b, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find solution
// of ax + by = n

    // function to find the solution
    function solution(a, b, n)
    {
        // traverse for all possible values
        for (let i = 0; i * a <= n; i++)
        {

            // check if it is satisfying the equation
            if ((n - (i * a)) % b == 0)
            {
                document.write("x = " + i +
                                   ", y = " +
                                   (n - (i * a)) / b);

                return ;
            }
        }

        document.write("No solution");
    }

// Driver code

        let a = 2, b = 3, n = 7;
        solution(a, b, n);

         // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
x = 2, y = 1         
```