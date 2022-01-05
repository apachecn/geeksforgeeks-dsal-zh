# 检查数字 N 的位数之和是否除以

> 原文:[https://www . geesforgeks . org/check-if-of-number-n-division-it/](https://www.geeksforgeeks.org/check-if-the-sum-of-digits-of-a-number-n-divides-it/)

给定一个数字 n。任务是检查给定数字的位数之和是否除以该数字。如果分割，则打印是，否则打印否
**示例** :

```
Input : N = 12
Output : YES
Sum of digits = 1+2 =3 and 3 divides 12.
So, print YES.

Input : N = 15
Output : NO
```

提取数字的位数，计算其所有位数的总和，并检查位数的总和是否为 N。
以下是上述方法的实现:

## C++

```
// C++ program to check if sum of
// digits of a number divides it

#include <iostream>
using namespace std;

// Function to check if sum of
// digits of a number divides it
int isSumDivides(int N)
{
    int temp = N;

    int sum = 0;

    // Calculate sum of all of digits of N
    while (temp) {
        sum += temp % 10;
        temp /= 10;
    }

    if (N % sum == 0)
        return 1;
    else
        return 0;
}

// Driver Code
int main()
{
    int N = 12;

    if (isSumDivides(N))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if sum of
// digits of a number divides it

import java.util.*;
import java.lang.*;

class GFG
{
// Function to check if sum of
// digits of a number divides it
static int isSumDivides(int N)
{
    int temp = N;

    int sum = 0;

    // Calculate sum of all of digits of N
    while (temp > 0)
    {
        sum += temp % 10;
        temp /= 10;
    }

    if (N % sum == 0)
        return 1;
    else
        return 0;
}

// Driver Code
public static void main(String args[])
{
    int N = 12;

    if (isSumDivides(N) == 1)
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to check if sum of
# digits of a number divides it

# Function to check if sum of
# digits of a number divides it
def isSumDivides(N):

    temp = N

    sum = 0

    # Calculate sum of all of
    # digits of N
    while (temp):
        sum += temp % 10
        temp = int(temp / 10)

    if (N % sum == 0):
        return 1
    else:
        return 0

# Driver Code
if __name__=='__main__':
    N = 12

    if (isSumDivides(N)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# mits
```

## C#

```
// C# program to check if sum of
// digits of a number divides it
using System;

// Function to check if sum of
// digits of a number divides it
class GFG
{
public int isSumDivides(int N)
{
    int temp = N, sum = 0;

    // Calculate sum of all of
    // digits of N
    while (temp > 0)
    {
        sum += temp % 10;
        temp /= 10;
    }

    if (N % sum == 0)
        return 1;
    else
        return 0;
}

// Driver Code
public static void Main()
{
    GFG g = new GFG();
    int N = 12;

    if (g.isSumDivides(N) > 0)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if sum of
// digits of a number divides it

// Function to check if sum of
// digits of a number divides it
function isSumDivides($N)
{
    $temp = $N;

    $sum = 0;

    // Calculate sum of all of
    // digits of N
    while ($temp)
    {
        $sum += $temp % 10;
        $temp = (int)$temp / 10;
    }

    if ($N % $sum == 0)
        return 1;
    else
        return 0;
}

// Driver Code
$N = 12;

if (isSumDivides($N))
    echo "YES";
else
    echo "NO";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to check if sum of
// digits of a number divides it   
// Function to check if sum of
    // digits of a number divides it
    function isSumDivides(N) {
        var temp = N;

        var sum = 0;

        // Calculate sum of all of digits of N
        while (temp > 0) {
            sum += temp % 10;
            temp = parseInt(temp/10);
        }

        if (N % sum == 0)
            return 1;
        else
            return 0;
    }

    // Driver Code

        var N = 12;

        if (isSumDivides(N) == 1)
            document.write("YES");
        else
            document.write("NO");

// This code contributed by aashish1995
</script>
```

**Output:** 

```
YES
```