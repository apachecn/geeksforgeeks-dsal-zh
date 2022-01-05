# 检查 N 是否可以表示为从集合{A，B}

中选择的整数之和

> 原文:[https://www . geeksforgeeks . org/check-if-n-可以表示为整数之和-从集合 a-b 中选择/](https://www.geeksforgeeks.org/check-if-n-can-be-represented-as-sum-of-integers-chosen-from-set-a-b/)

给定三个整数 **N** 、 **A** 和 **B** ，任务是找出 **N** 是否可以表示为 **A 的**和 **B 的**之和。

**示例:**

> **输入:** N = 11，A = 2，B = 3
> **输出:**是
> 2 + 2 + 2 + 2 + 3 = 11
> 
> **输入:** N = 8，A = 3，B = 7
> T3】输出:否

**方法:**一个有效的解决方法是调用以零开始的递归函数(因为零总是可能的)。如果函数调用是 **fun(x)** 那么递归调用 **fun(x + a)** 和 **fun(x + b)** (因为如果 **x** 是可能的，那么 **x + a** 和 **x + b** 也是可能的)。如果 **x > n** ，则退出该功能。

下面是上述方法的实现:

## C++

```
// CPP program to find if number N can
// be represented as sum of a's and b's
#include <bits/stdc++.h>
using namespace std;

// Function to find if number N can
// be represented as sum of a's and b's
void checkIfPossibleRec(int x, int a, int b,
                   bool isPossible[], int n)
{
    // base condition
    if (x > n)
        return;

    // if x is already visited
    if (isPossible[x])
        return;

    // set x as possible
    isPossible[x] = true;

    // recursive call
    checkIfPossibleRec(x + a, a, b, isPossible, n);
    checkIfPossibleRec(x + b, a, b, isPossible, n);
}

bool checkPossible(int n, int a, int b)
{
    bool isPossible[n + 1] = { false };
    checkIfPossibleRec(0, a, b, isPossible, n);
    return isPossible[n];
}

// Driver program
int main()
{
    int a = 3, b = 7, n = 8;
    if (checkPossible(a, b, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if number N can
// be represented as sum of a's and b's

import java.util.*;
class solution
{

// Function to find if number N can
// be represented as sum of a's and b's
static void checkIfPossibleRec(int x, int a, int b,
                                boolean isPossible[], int n)
{
    // base condition
    if (x > n)
        return;

    // if x is already visited
    if (isPossible[x])
        return;

    // set x as possible
    isPossible[x] = true;

    // recursive call
    checkIfPossibleRec(x + a, a, b, isPossible, n);
    checkIfPossibleRec(x + b, a, b, isPossible, n);
}

static boolean checkPossible(int n, int a, int b)
{
    boolean isPossible[]=new boolean[n + 1];
    for(int i=0;i<=n;i++)
    isPossible[i]=false;
    checkIfPossibleRec(0, a, b, isPossible, n);
    return isPossible[n];
}

// Driver program
public static void main(String args[])
{
    int a = 3, b = 7, n = 8;
    if (checkPossible(a, b, n))
        System.out.print("Yes");
    else
        System.out.print( "No");

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find if number N can
# be represented as sum of a's and b's

# Function to find if number N can
# be represented as sum of a's and b's
def checkIfPossibleRec(x, a, b, isPossible, n):

    # base condition
    if x > n:
        return

    # If x is already visited
    if isPossible[x]:
        return

    # Set x as possible
    isPossible[x] = True

    # Recursive call
    checkIfPossibleRec(x + a, a, b, isPossible, n)
    checkIfPossibleRec(x + b, a, b, isPossible, n)

def checkPossible(n, a, b):

    isPossible = [False] * (n + 1)
    checkIfPossibleRec(0, a, b, isPossible, n)
    return isPossible[n]

# Driver Code
if __name__ == "__main__":

    a, b, n = 3, 7, 8
    if checkPossible(a, b, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find if number N can
// be represented as sum of a's and b's
using System;

class GFG
{
// Function to find if number N can
// be represented as sum of a's and b's
static void checkIfPossibleRec(int x, int a, int b,
                               bool []isPossible, int n)
{
    // base condition
    if (x > n)
        return;

    // if x is already visited
    if (isPossible[x])
        return;

    // set x as possible
    isPossible[x] = true;

    // recursive call
    checkIfPossibleRec(x + a, a, b, isPossible, n);
    checkIfPossibleRec(x + b, a, b, isPossible, n);
}

static bool checkPossible(int n, int a, int b)
{
    bool []isPossible = new bool[n + 1];
    for(int i = 0; i <= n; i++)
    isPossible[i] = false;
        checkIfPossibleRec(0, a, b, isPossible, n);
    return isPossible[n];
}

// Driver Code
static public void Main ()
{
    int a = 3, b = 7, n = 8;
    if (checkPossible(a, b, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if number N can
// be represented as sum of a's and b's
// Function to find if number N can
// be represented as sum of a's and b's
function checkIfPossibleRec($x, $a, $b,
                            $isPossible, $n)
{
    // base condition
    if ($x > $n)
        return;

    // if x is already visited
    if ($isPossible == true)
        return;

    // set x as possible
    $isPossible[$x] = true;

    // recursive call
    checkIfPossibleRec($x + $a, $a, $b,
                       $isPossible, $n);
    checkIfPossibleRec($x + $b, $a, $b,
                       $isPossible, $n);
}

function checkPossible($n, $a, $b)
{
    $isPossible[$n + 1] = array(false);
    checkIfPossibleRec(0, $a, $b, $isPossible, $n);
    return $isPossible;
}

// Driver Code
$a = 3;
$b = 7;
$n = 8;
if (checkPossible($a, $b, $n))
    echo "No";
else
    echo "Yes";

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript program to find if number N can
// be represented as sum of a's and b's   

// Function to find if number N can
// be represented as sum of a's and b's
function checkIfPossibleRec(x, a, b, isPossible, n)
{

    // Base condition
    if (x > n)
        return;

    // If x is already visited
    if (isPossible[x])
        return;

    // Set x as possible
    isPossible[x] = true;

    // Recursive call
    checkIfPossibleRec(x + a, a, b, isPossible, n);
    checkIfPossibleRec(x + b, a, b, isPossible, n);
}

function checkPossible(n, a, b)
{
    var isPossible = Array(n + 1).fill(false);

    checkIfPossibleRec(0, a, b, isPossible, n);
    return isPossible[n];
}

// Driver code
var a = 3, b = 7, n = 8;
if (checkPossible(a, b, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
No
```