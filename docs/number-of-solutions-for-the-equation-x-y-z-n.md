# 方程 x + y + z 的解的数量< = n

> 原文:[https://www . geeksforgeeks . org/方程求解数-x-y-z-n/](https://www.geeksforgeeks.org/number-of-solutions-for-the-equation-x-y-z-n/)

给定四个数字 X，Y，z，n，任务是求方程 x + y + z <= n 的解的个数，使得 0 <= x <= X，0 <= y <= Y，0 <= z <= Z。

**示例:**

```
Input: x = 1, y = 1, z = 1, n = 1
Output: 4

Input: x = 1, y = 2, z = 3, n = 4
Output: 20
```

**方法:**让我们显式迭代 x 和 y 的所有可能值(使用嵌套循环)。对于这样一个 x 和 y 的固定值，问题简化为有多少个 z 值使得**z<= n–x–y 和 0 < = z < = Z.**

以下是找到解决方案数量所需的实施:

## C++

```
// CPP program to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
#include <bits/stdc++.h>
using namespace std;

// function to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
int NumberOfSolutions(int x, int y, int z, int n)
{
    // to store answer
    int ans = 0;

    // for values of x
    for (int i = 0; i <= x; i++) {

        // for values of y
        for (int j = 0; j <= y; j++) {

            // maximum possible value of z
            int temp = n - i - j;

            // if z value greater than equals to 0
            // then only it is valid
            if (temp >= 0) {

                // find minimum of temp and z
                temp = min(temp, z);
                ans += temp + 1;
            }
        }
    }

    // return required answer
    return ans;
}

// Driver code
int main()
{
    int x = 1, y = 2, z = 3, n = 4;

    cout << NumberOfSolutions(x, y, z, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.

import java.io.*;

class GFG {

// function to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
static int NumberOfSolutions(int x, int y, int z, int n)
{
    // to store answer
    int ans = 0;

    // for values of x
    for (int i = 0; i <= x; i++) {

        // for values of y
        for (int j = 0; j <= y; j++) {

            // maximum possible value of z
            int temp = n - i - j;

            // if z value greater than equals to 0
            // then only it is valid
            if (temp >= 0) {

                // find minimum of temp and z
                temp = Math.min(temp, z);
                ans += temp + 1;
            }
        }
    }

    // return required answer
    return ans;
}

       // Driver code
    public static void main (String[] args) {

    int x = 1, y = 2, z = 3, n = 4;
    System.out.println( NumberOfSolutions(x, y, z, n));

    }
}

// this code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find the number 
# of solutions for the equation
# x + y + z <= n, such that
# 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.

# function to find the number of solutions
# for the equation x + y + z <= n, such that
# 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
def NumberOfSolutions(x, y, z, n) :

    # to store answer
    ans = 0

    # for values of x
    for i in range(x + 1) :

        # for values of y
        for j in range(y + 1) :

            # maximum possible value of z
            temp = n - i - j

            # if z value greater than equals 
            # to 0 then only it is valid
            if temp >= 0 :

                # find minimum of temp and z
                temp = min(temp, z)
                ans += temp + 1

    # return required answer
    return ans

# Driver code
if __name__ == "__main__" :

    x, y, z, n = 1, 2, 3, 4

    # function calling
    print(NumberOfSolutions(x, y, z, n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
using System;

public class GFG{

// function to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
static int NumberOfSolutions(int x, int y, int z, int n)
{
    // to store answer
    int ans = 0;

    // for values of x
    for (int i = 0; i <= x; i++) {

        // for values of y
        for (int j = 0; j <= y; j++) {

            // maximum possible value of z
            int temp = n - i - j;

            // if z value greater than equals to 0
            // then only it is valid
            if (temp >= 0) {

                // find minimum of temp and z
                temp = Math.Min(temp, z);
                ans += temp + 1;
            }
        }
    }

    // return required answer
    return ans;
}

// Driver code

    static public void Main (){

    int x = 1, y = 2, z = 3, n = 4;

    Console.WriteLine( NumberOfSolutions(x, y, z, n));

    }
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number
// of solutions for the equation
// x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.

// function to find the number of
// solutions for the equation
// x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
function NumberOfSolutions($x, $y, $z, $n)
{
    // to store answer
    $ans = 0;

    // for values of x
    for ($i = 0; $i <= $x; $i++)
    {

        // for values of y
        for ($j = 0; $j <= $y; $j++)
        {

            // maximum possible value of z
            $temp = $n - $i - $j;

            // if z value greater than equals
            // to 0 then only it is valid
            if ($temp >= 0)
            {

                // find minimum of temp and z
                $temp = min($temp, $z);
                $ans += $temp + 1;
            }
        }
    }

    // return required answer
    return $ans;
}

// Driver code
$x = 1; $y = 2;
$z = 3; $n = 4;

echo NumberOfSolutions($x, $y, $z, $n);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of solutions for the equation x + y + z <= n,
// such that 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.

// Function to find the number of solutions for
// the equation x + y + z <= n, such that
// 0 <= x <= X, 0 <= y <= Y, 0 <= z <= Z.
function NumberOfSolutions(x, y, z, n)
{

    // To store answer
    var ans = 0;

    // for values of x
    for(var i = 0; i <= x; i++)
    {

        // for values of y
        for(var j = 0; j <= y; j++)
        {

            // Maximum possible value of z
            var temp = n - i - j;

            // If z value greater than equals to 0
            // then only it is valid
            if (temp >= 0)
            {

                // Find minimum of temp and z
                temp = Math.min(temp, z);
                ans += temp + 1;
            }
        }
    }

    // Return required answer
    return ans;
}

// Driver Code
var x = 1, y = 2, z = 3, n = 4;

document.write(NumberOfSolutions(x, y, z, n));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
20
```