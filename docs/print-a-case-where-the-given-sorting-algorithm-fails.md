# 打印给定排序算法失败的情况

> 原文:[https://www . geeksforgeeks . org/print-a-case-给定排序算法失败/](https://www.geeksforgeeks.org/print-a-case-where-the-given-sorting-algorithm-fails/)

给定一个整数 N，任务是找出 N 个未通过下面排序算法的元素。如果 N 个元素都没有失败，则打印-1。

```
loop i from 1 to n-1
   loop j from i to n-1 
      if a[j]>a[i+1]  
         swap(a[i], a[j+1])
```

**例:**

```
Input: N = 10 
Output: 10 9 8 7 6 5 4 3 2 1 

Input: N = 2
Output: -1
```

**逼近**:在求解各种情况时，我们可以观察到，只有对于 *n < =2* ，给定的算法是**无效的**。任何高于 N 的值都将在给定的算法中失败。由 N 个数字(1，2，3)组成的排序数组。。n)不能使用这个给定的算法进行反向排序。
以下是上述方法的实现:

## C++

```
// C++ program to find a case where the
// given algorithm fails

#include <bits/stdc++.h>
using namespace std;

// Function to print a case
// where the given sorting algorithm fails
void printCase(int n)
{
    // only case where it fails
    if (n <= 2) {
        cout << -1;
        return;
    }

    for (int i = n; i >= 1; i--)
        cout << i << " ";
}

// Driver Code
int main()
{
    int n = 3;

    printCase(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a case where the
// given algorithm fails

import java.io.*;

class GFG {
    // Function to print a case where
// the given sorting algorithm fails
static void printCase(int n)
{
// only case where it fails
if (n <= 2) {
        System.out.print(-1);
    return;

}
for (int i = n; i >= 1; i--)
        System.out.print(i + " ");
}

// Driver Code

    public static void main (String[] args) {
        int n = 3;
        printCase(n);

//This code is contributed by akt_mit
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find a case
# where the given algorithm fails

# Function to print a case where
# the given sorting algorithm fails
def printCase(n):

    # only case where it fails
    if (n <= 2) :
        print("-1")
        return

    for i in range(n, 0, -1):
        print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    n = 3

    printCase(n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find a case where the
// given algorithm fails
using System;

class GFG
{
// Function to print a case where
// the given sorting algorithm fails
static void printCase(int n)
{
    // only case where it fails
    if (n <= 2)
    {
        Console.Write(-1);
        return;
    }

    for (int i = n; i >= 1; i--)
        Console.Write(i + " ");
}

// Driver Code
public static void Main()
{
    int n = 3;

    printCase(n);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a case where
// the given algorithm fails

// Function to print a case where
// the given sorting algorithm fails
function printCase($n)
{
    // only case where it fails
    if ($n <= 2)
    {
        echo (-1);
        return;
    }

    for ($i = $n; $i >= 1; $i--)
    {
        echo ($i);
        echo(" ");
    }
}

// Driver Code
$n = 3;

printCase($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find a case where the
    // given algorithm fails

    // Function to print a case where
    // the given sorting algorithm fails
    function printCase(n)
    {
        // only case where it fails
        if (n <= 2)
        {
            document.write(-1);
            return;
        }

        for (let i = n; i >= 1; i--)
            document.write(i + " ");
    }

    let n = 3;

    printCase(n);

</script>
```

**Output:** 

```
3 2 1
```

**时间复杂度**:O(N)
T3】辅助空间 : O(1)