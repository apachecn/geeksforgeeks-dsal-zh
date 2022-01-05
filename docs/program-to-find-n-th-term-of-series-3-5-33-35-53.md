# 求数列 3、5、33、35、53 的第 N 项的程序。

> 原文:[https://www . geesforgeks . org/program-to-find-n-th-term-of-series-3-5-33-35-53/](https://www.geeksforgeeks.org/program-to-find-n-th-term-of-series-3-5-33-35-53/)

给定一系列仅由数字 3 和 5 组成的数字。系列的前几个数字是:

> **3，5，33，35，53，55，…..**

给定一个数 n。任务是找出给定数列中的第 n 个数。
**例** :

```
Input : N = 2
Output : 5

Input : N = 5
Output : 53
```

这个想法是基于这样一个事实，即序列中最后一个数字的值是交替的。例如，如果第 i <sup>个</sup>数字的最后一位是 3，那么第(i-1) <sup>个</sup>和第(i+1) <sup>个</sup>数字的最后一位必须是 5。
创建一个大小为(n+1)的数组，并向其推送 3 和 5(这两个总是系列的前两个元素)。更多元素请查看

```
1) If i is odd,
      arr[i] = arr[i/2]*10 + 3;
2) If it is even,
      arr[i] = arr[(i/2)-1]*10 + 5;
At last return arr[n].
```

以下是上述思路的实现:

## C++

```
// C++ program to find n-th number in a series
// made of digits 3 and 5

#include <bits/stdc++.h>
using namespace std;

// Function to find n-th number in series
// made of 3 and 5
int printNthElement(int n)
{
    // create an array of size (n+1)
    int arr[n + 1];
    arr[1] = 3;
    arr[2] = 5;

    for (int i = 3; i <= n; i++) {
        // If i is odd
        if (i % 2 != 0)
            arr[i] = arr[i / 2] * 10 + 3;
        else
            arr[i] = arr[(i / 2) - 1] * 10 + 5;
    }
    return arr[n];
}

// Driver code
int main()
{
    int n = 6;

    cout << printNthElement(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number in a series
// made of digits 3 and 5

class FindNth {
    // Function to find n-th number in series
    // made of 3 and 5
    static int printNthElement(int n)
    {
        // create an array of size (n+1)
        int arr[] = new int[n + 1];
        arr[1] = 3;
        arr[2] = 5;

        for (int i = 3; i <= n; i++) {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[i / 2] * 10 + 3;
            else
                arr[i] = arr[(i / 2) - 1] * 10 + 5;
        }
        return arr[n];
    }

    // main function
    public static void main(String[] args)
    {
        int n = 6;

        System.out.println(printNthElement(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find n-th number 
# in a series made of digits 3 and 5

# Return n-th number in series made 
# of 3 and 5
def printNthElement(n) :

    # create an array of size (n + 1)
    arr =[0] * (n + 1);
    arr[1] = 3
    arr[2] = 5

    for i in range(3, n + 1) :
        # If i is odd
        if (i % 2 != 0) :
            arr[i] = arr[i // 2] * 10 + 3
        else :
            arr[i] = arr[(i // 2) - 1] * 10 + 5

    return arr[n]

# Driver code
n = 6
print(printNthElement(n))
```

## C#

```
// C# program to find n-th number
// in a series made of digits 3 and 5
using System;

class GFG
{
// Function to find n-th number
// in series made of 3 and 5
static int printNthElement(int n)
{
    // create an array of size (n+1)
    int [] arr = new int[n + 1];
    arr[1] = 3;
    arr[2] = 5;

    for (int i = 3; i <= n; i++)
    {
        // If i is odd
        if (i % 2 != 0)
            arr[i] = arr[i / 2] * 10 + 3;
        else
            arr[i] = arr[(i / 2) - 1] * 10 + 5;
    }
    return arr[n];
}

// Driver Code
static void Main()
{
    int n = 6;

    Console.WriteLine(printNthElement(n));
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// number in a series made
// of digits 3 and 5

// Function to find n-th number
// in series made of 3 and 5
function printNthElement($n)
{
    // create an array of size (n+1)
    $arr = array_fill(0, ($n + 1), NULL);
    $arr[1] = 3;
    $arr[2] = 5;

    for ($i = 3; $i <= $n; $i++)
    {
        // If i is odd
        if ($i % 2 != 0)
            $arr[$i] = $arr[$i / 2] * 10 + 3;
        else
            $arr[$i] = $arr[($i / 2) -
                             1] * 10 + 5;
    }
    return $arr[$n];
}

// Driver code
$n = 6;

echo printNthElement($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th number in a series
// made of digits 3 and 5

    // Function to find n-th number in series
    // made of 3 and 5
    function prletNthElement( n) {
        // create an array of size (n+1)
        let arr = Array(n + 1).fill(0);
        arr[1] = 3;
        arr[2] = 5;

        for ( i = 3; i <= n; i++) {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[i / 2] * 10 + 3;
            else
                arr[i] = arr[(i / 2) - 1] * 10 + 5;
        }
        return arr[n];
    }

    // main function

        let n = 6;

        document.write(prletNthElement(n));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
55
```