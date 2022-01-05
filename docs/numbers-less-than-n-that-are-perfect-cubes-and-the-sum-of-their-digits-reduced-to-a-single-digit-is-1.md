# 小于 N 的数字是完美立方体，它们的位数之和减少到一位数为 1

> 原文:[https://www . geeksforgeeks . org/numbers-小于 n 的完美立方和它们的数字总和-简化为一位数-is-1/](https://www.geeksforgeeks.org/numbers-less-than-n-that-are-perfect-cubes-and-the-sum-of-their-digits-reduced-to-a-single-digit-is-1/)

给定一个数字 **n** ，任务是打印所有小于或等于 **n** 的数字，这些数字是**完美立方体**，它们的最终数字总和是 **1** 。
**举例:**

> **输入:** n = 100
> **输出:**1 64
> 64 = 6+4 = 10 = 1+0 = 1
> **输入:** n = 1000
> **输出:** 1 64 343 1000

**方法:**对于每一个小于或等于 **n** 的完美立方体，继续计算其位数之和，直到该数减少到一个位数(这里 O(1)方法)，如果该位数为 1，则打印完美立方体，否则跳到 **n** 下面的下一个完美立方体，直到所有完美立方体都被考虑。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <cmath>
#include <iostream>
using namespace std;

// Function that returns true if the eventual
// digit sum of number nm is 1
bool isDigitSumOne(int nm)
{
   //if reminder will 1
   //then eventual sum is 1
    if (nm % 9 == 1)
        return true;
    else
        return false;
}

// Function to print the required numbers
// less than n
void printValidNums(int n)
{
    int cbrt_n = (int)cbrt(n);
    for (int i = 1; i <= cbrt_n; i++) {
        int cube = pow(i, 3);

        // If it is the required perfect cube
        if (cube >= 1 && cube <= n && isDigitSumOne(cube))
            cout << cube << " ";
    }
}

// Driver code
int main()
{
    int n = 1000;
    printValidNums(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if the eventual
    // digit sum of number nm is 1
    static boolean isDigitSumOne(int nm)
    {

      //if reminder will 1
      //then eventual sum is 1
      if (nm % 9 == 1)
        return true;
      else
        return false;
    }

    // Function to print the required numbers
    // less than n
    static void printValidNums(int n)
    {
        int cbrt_n = (int)Math.cbrt(n);
        for (int i = 1; i <= cbrt_n; i++) {
            int cube = (int)Math.pow(i, 3);

            // If it is the required perfect cube
            if (cube >= 1 && cube <= n && isDigitSumOne(cube))
                System.out.print(cube + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 1000;
        printValidNums(n);
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach
import math

# Function that returns true if the eventual
# digit sum of number nm is 1
def isDigitSumOne(nm) :
   #if reminder will 1
   #then eventual sum is 1
    if(nm % 9 == 1):
        return True
    else:
        return False

# Function to print the required numbers
# less than n
def printValidNums(n):
    cbrt_n = math.ceil(n**(1./3.))
    for i in range(1, cbrt_n + 1):
        cube = i * i * i
        if (cube >= 1 and cube <= n and isDigitSumOne(cube)):
            print(cube, end = " ")

# Driver code
n = 1000
printValidNums(n)
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function that returns true if the
    // eventual digit sum of number nm is 1
    static bool isDigitSumOne(int nm)
    {

     //if reminder will 1
     //then eventual sum is 1
      if (nm % 9 == 1)
         return true;
      else
         return false;
    }

    // Function to print the required
    // numbers less than n
    static void printValidNums(int n)
    {
        int cbrt_n = (int)Math.Ceiling(Math.Pow(n,
                                      (double) 1 / 3));
        for (int i = 1; i <= cbrt_n; i++)
        {
            int cube = (int)Math.Pow(i, 3);

            // If it is the required perfect cube
            if (cube >= 1 && cube <= n &&
                             isDigitSumOne(cube))
                Console.Write(cube + " ");
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 1000;
        printValidNums(n);
    }
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if the
// eventual digit sum of number nm is 1
function isDigitSumOne($nm)
{
     //if reminder will 1
    //then eventual sum is 1
    if ($nm % 9 == 1)
        return true;
    else
        return false;
}

// Function to print the required numbers
// less than n
function printValidNums($n)
{
    $cbrt_n = ceil(pow($n,1/3));
    for ($i = 1; $i <= $cbrt_n; $i++)
    {
        $cube = pow($i, 3);

        // If it is the required perfect cube
        if ($cube >= 1 && $cube <= $n &&
                    isDigitSumOne($cube))
            echo $cube, " ";
    }
}

// Driver code
$n = 1000;
printValidNums($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if the
    // eventual digit sum of number nm is 1
    function isDigitSumOne(nm)
    {

     //if reminder will 1
     //then eventual sum is 1
      if (nm % 9 == 1)
         return true;
      else
         return false;
    }

    // Function to print the required
    // numbers less than n
    function printValidNums(n)
    {
        let cbrt_n = Math.ceil(Math.pow(n, 1 / 3));
        for (let i = 1; i <= cbrt_n; i++)
        {
            let cube = Math.pow(i, 3);

            // If it is the required perfect cube
            if (cube >= 1 && cube <= n && isDigitSumOne(cube))
                document.write(cube + " ");
        }
    }

    let n = 1000;
      printValidNums(n);

</script>
```

**Output:** 

```
1 64 343 1000
```