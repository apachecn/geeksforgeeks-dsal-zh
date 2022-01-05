# 长度为 k 的小数个数，严格单调

> 原文:[https://www . geesforgeks . org/number-decimal-numbers-length-k-strict-monotonic/](https://www.geeksforgeeks.org/number-decimal-numbers-length-k-strict-monotone/)

我们称十进制数为单调数，如果:![D[i] \leq D[i+1], 0 \leq i \leq |D| ](img/11732dc0ef4ddc3fde9fdfe3b2af67f4.png "Rendered by QuickLaTeX.com")

编写一个程序，在输入时取正数 n，并返回长度为 n 的严格单调的十进制数。数字不能以 0 开头。

**示例:**

```
Input : 2
Output : 36
Numbers are 12, 13, ... 19, 23
24, ... 29, .... 89.

Input : 3
Output : 84

```

这个问题的解释遵循相同的规则:长度为 k 的十进制数的数量是单调的

唯一的区别是，现在我们不能重复，所以以前计算的值是左边和左上角对角线上的值。

## C++

```
// CPP program to count numbers of k
// digits that are strictly monotone.
#include <cstring>
#include <iostream>

int static const DP_s = 9;

int getNumStrictMonotone(int len)
{
    // DP[i][j] is going to store monotone
    // numbers of length i+1 considering
    // j+1 digits (1, 2, 3, ..9)
    int DP[len][DP_s];
    memset(DP, 0, sizeof(DP));

    // Unit length numbers
    for (int i = 0; i < DP_s; ++i) 
        DP[0][i] = i + 1;    

    // Building dp[] in bottom up
    for (int i = 1; i < len; ++i) 
        for (int j = 1; j < DP_s; ++j) 
            DP[i][j] = DP[i - 1][j - 1] + DP[i][j - 1];        

    return DP[len - 1][DP_s - 1];
}

// Driver code
int main()
{
    std::cout << getNumStrictMonotone(2); 
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers of k
// digits that are strictly monotone.
import java.io.*;
import java.util.*;

class GFG {

    static int DP_s = 9;

    static int getNumStrictMonotone(int len) 
    {
        // DP[i][j] is going to store monotone
        // numbers of length i+1 considering
        // j+1 digits (1, 2, 3, ..9)
        int[][] DP = new int[len][DP_s];

        // Unit length numbers
        for (int i = 0; i < DP_s; ++i)
        DP[0][i] = i + 1;

        // Building dp[] in bottom up
        for (int i = 1; i < len; ++i)
             for (int j = 1; j < DP_s; ++j)
                DP[i][j] = DP[i - 1][j - 1] 
                             + DP[i][j - 1];

        return DP[len - 1][DP_s - 1];
    }
    public static void main(String[] args) 
    {
        int n = 2;
        System.out.println(getNumStrictMonotone(n));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to count numbers of k
# digits that are strictly monotone.

DP_s = 9

def getNumStrictMonotone(ln):

    # DP[i][j] is going to store monotone
    # numbers of length i+1 considering
    # j+1 digits (1, 2, 3, ..9)
    DP = [[0] * DP_s for _ in range(ln)]

    # Unit length numbers
    for i in range(DP_s):
        DP[0][i] = i + 1 

    # Building dp[] in bottom up
    for i in range(1, ln):

        for j in range(1, DP_s):

            DP[i][j] = DP[i - 1][j - 1] + DP[i][j - 1]     

    return DP[ln - 1][DP_s - 1]

# Driver code
print(getNumStrictMonotone(2))

# This code is contributed by Ansu Kumari.
```

## C#

```
// C# program to count numbers of k
// digits that are strictly monotone.
using System;

class GFG {

    static int DP_s = 9;

    static int getNumStrictMonotone(int len) 
    {
        // DP[i][j] is going to store monotone
        // numbers of length i+1 considering
        // j+1 digits (1, 2, 3, ..9)
        int[,] DP = new int[len,DP_s];

        // Unit length numbers
        for (int i = 0; i < DP_s; ++i)
        DP[0,i] = i + 1;

        // Building dp[] in bottom up
        for (int i = 1; i < len; ++i)
            for (int j = 1; j < DP_s; ++j)
                DP[i,j] = DP[i - 1,j - 1] 
                            + DP[i,j - 1];

        return DP[len - 1,DP_s - 1];
    }

    // Driver code
    public static void Main() 
    {
        int n = 2;
        Console.WriteLine(getNumStrictMonotone(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count 
// numbers of k digits
// that are strictly
// monotone.
$DP_s = 9;

function getNumStrictMonotone($len)
{
    global $DP_s;

    // DP[i][j] is going to
    // store monotone numbers
    // of length i+1 considering
    // j+1 digits (1, 2, 3, ..9)
    $DP = array(array());
    for($i = 0; $i < $len; $i++)
    {
        for($j = 0; $j < $DP_s; $j++)
            $DP[$i][$j] = 0;
    }

    // Unit length numbers
    for ($i = 0; $i < $DP_s; ++$i) 
        $DP[0][$i] = $i + 1; 

    // Building dp[]
    // in bottom up
    for ($i = 1; $i < $len; ++$i) 
        for ($j = 1; $j < $DP_s; ++$j) 
            $DP[$i][$j] = $DP[$i - 1][$j - 1] + 
                          $DP[$i][$j - 1];     

    return $DP[$len - 1][$DP_s - 1];
}

// Driver code
echo (getNumStrictMonotone(2));

// This code is contributed by 
// Manish Shaw(manishshaw1)
?>
```

**Output :**

```
36

```