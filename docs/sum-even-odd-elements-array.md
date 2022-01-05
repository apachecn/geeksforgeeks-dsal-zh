# 打印数组中奇偶元素之和的程序

> 原文:[https://www.geeksforgeeks.org/sum-even-odd-elements-array/](https://www.geeksforgeeks.org/sum-even-odd-elements-array/)

先决条件–[数组基础](https://www.geeksforgeeks.org/arrays-in-c-language-set-1-introduction/)
给定一个数组，编写一个程序，分别求出偶数和奇数索引位置的值之和。
示例:

```
Input : arr = {1, 2, 3, 4, 5, 6}
Output :Even index positions sum 9
        Odd index positions sum 12
Explanation: Here, n = 6 so there will be 3 even 
index positions and 3 odd index positions in an array
Even = 1 + 3 + 5 = 9
Odd =  2 + 4 + 6 = 12

Input : arr = {10, 20, 30, 40, 50, 60, 70}
Output : Even index positions sum 160
        Odd index positions sum 170
Explanation: Here, n = 7 so there will be 3 odd
index positions and 4 even index positions in an array
Even = 10 + 30 + 50 + 70 = 160
Odd = 20 + 40 + 60 = 120 
```

## C++

```
// CPP program to find out
// Sum of elements at even and
// odd index positions separately
#include <iostream>

using namespace std;

// Function to calculate sum
void EvenOddSum(int arr[], int n)
{
    int even = 0;
    int odd = 0;
    for (int i = 0; i < n; i++) {
        // Loop to find even, odd sum
        if (i % 2 == 0)
            even += arr[i];
        else
            odd += arr[i];
    }

    cout << "Even index positions sum " << even;
    cout << "\nOdd index positions sum " << odd;
}

// Driver function
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    EvenOddSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out
// Sum of elements at even and
// odd index positions separately
import java.io.*;

class EvenOddSum {
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int even = 0, odd = 0;

        // Loop to find even, odd sum
        for (int i = 0; i < arr.length; i++) {
            if (i % 2 == 0)
                even += arr[i];
            else
                odd += arr[i];
        }

        System.out.println("Even index positions sum: " + even);
        System.out.println("Odd index positions sum: " + odd);
    }
}
```

## 计算机编程语言

```
# Python program to find out
# Sum of elements at even and
# odd index positions separately

# Function to calculate Sum
def EvenOddSum(a, n):
    even = 0
    odd = 0
    for i in range(n):

        # Loop to find even, odd Sum
        if i % 2 == 0:
            even += a[i]
        else:
            odd += a[i]

    print "Even index positions sum ", even
    print "nOdd index positions sum ", odd

# Driver Function

arr = [1, 2, 3, 4, 5, 6]
n = len(arr)

EvenOddSum(arr, n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find out
// Sum of elements at even and
// odd index positions separately
using System;

public class GFG {

    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int even = 0, odd = 0;

        // Loop to find even, odd sum
        for (int i = 0; i < arr.Length; i++)
        {
            if (i % 2 == 0)
                even += arr[i];
            else
                odd += arr[i];
        }

        Console.WriteLine("Even index positions"
                             + " sum: " + even);

        Console.WriteLine("Odd index positions "
                               + "sum: " + odd);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find out
// Sum of elements at even and
// odd index positions separately

// Function to calculate sum
function EvenOddSum($arr, $n)
{
    $even = 0;
    $odd = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Loop to find even, odd sum
        if ($i % 2 == 0)
            $even += $arr[$i];
        else
            $odd += $arr[$i];
    }

    echo("Even index positions sum " . $even);
    echo("\nOdd index positions sum " . $odd);
}

// Driver Code
$arr = array( 1, 2, 3, 4, 5, 6 );
$n = sizeof($arr);

EvenOddSum($arr, $n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find out
// Sum of elements at even and
// odd index positions separately

// Function to calculate sum
function EvenOddSum(arr, n)
{
    let even = 0;
    let odd = 0;
    for (let i = 0; i < n; i++)
    {

        // Loop to find even, odd sum
        if (i % 2 == 0)
            even += arr[i];
        else
            odd += arr[i];
    }

    document.write("Even index positions sum " + even);
    document.write("<br>" + "Odd index positions sum " + odd);
}

// Driver function
    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;

    EvenOddSum(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
Even index positions sum 9
Odd index positions sum 12
```

#### 方法二:使用 python 中的[切片:](https://www.geeksforgeeks.org/python-list-slicing/)

使用切片计算所有偶数索引的总和，用奇数索引重复相同的操作，并打印总和。

下面是实现:

## 蟒蛇 3

```
# Python program to find out
# Sum of elements at even and
# odd index positions separately

# Function to calculate Sum

def EvenOddSum(a, n):
    even_sum = sum(a[::2])
    odd_sum = sum(a[1::2])
    print("Even index positions sum", even_sum)
    print("Odd index positions sum", odd_sum)

# Driver Function

arr = [1, 2, 3, 4, 5, 6]
n = len(arr)

EvenOddSum(arr, n)

# This code is contributed by vikkycirus
```

## java 描述语言

```
<script>

// Javascript program to find out
// Sum of elements at even and
// odd index positions separately

// Function to calculate sum
function EvenOddSum(arr, n)
{
    let even = 0;
    let odd = 0;
    for (let i = 0; i < n; i++)
    {

        // Loop to find even, odd sum
        if (i % 2 == 0)
            even += arr[i];
        else
            odd += arr[i];
    }

    document.write("Even index positions sum " + even);
    document.write("<br>" + "Odd index positions sum " + odd);
}

// Driver function
    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;

    EvenOddSum(arr, n);

    // This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
Even index positions sum 9
Odd index positions sum 12
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。