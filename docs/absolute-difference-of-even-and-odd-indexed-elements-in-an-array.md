# 数组中偶数和奇数索引元素的绝对差

> 原文:[https://www . geeksforgeeks . org/数组中奇偶索引元素的绝对差/](https://www.geeksforgeeks.org/absolute-difference-of-even-and-odd-indexed-elements-in-an-array/)

给定一个整数数组 *arr* ，任务是分别找到偶数和奇数索引位置元素的运行绝对差。
**注:**数组考虑基于 0 的索引。也就是说，数组中第一个元素的索引为零。
**例:**

> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:**偶指数绝对差:3
> 奇指数绝对差:4
> **说明:**
> 这里偶索引元素是 1，3 和 5
> 所以偶绝对差会是(| 1–3 | = 2)=>(| 2–5 | = 3)
> 同样奇索引元素是 2， 4 和 6
> 而奇数绝对差将为(| 2–4 | = 2)=>(| 2–6 | = 4)
> **输入:** arr[] = {10，20，30，40，50，60，70}
> **输出:**偶数指数绝对差:40
> 奇数指数绝对差:40

**方式:**遍历数组，保留两个变量*偶*和*奇*分别存储偶、奇索引元素的绝对差。遍历时，检查当前索引是否为偶数，即 *(i%2) == 0* 。最后打印结果。
以下是上述方法的实施:

## C++

```
// CPP program to find absolute difference of elements
// at even and odd index positions separately
#include <bits/stdc++.h>
using namespace std;

// Function to calculate absolute difference
void EvenOddAbsoluteDifference(int arr[], int n)
{
    int even = 0;
    int odd = 0;

    for (int i = 0; i < n; i++) {

        // Loop to find even, odd absolute difference
        if (i % 2 == 0)
            even = abs(even - arr[i]);
        else
            odd = abs(odd - arr[i]);
    }

    cout << "Even Index absolute difference : " << even;
    cout << endl;
    cout << "Odd Index absolute difference : " << odd;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    EvenOddAbsoluteDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find absolute difference of elements
// at even and odd index positions separately

public class GFG{

    // Function to calculate absolute difference
    static void EvenOddAbsoluteDifference(int arr[], int n)
    {
        int even = 0;
        int odd = 0;

        for (int i = 0; i < n; i++) {

            // Loop to find even, odd absolute difference
            if (i % 2 == 0)
                even = Math.abs(even - arr[i]);
            else
                odd = Math.abs(odd - arr[i]);
        }

        System.out.println("Even Index absolute difference : " + even);
        System.out.println("Odd Index absolute difference : " + odd);
    }

     // Driver Code
     public static void main(String []args){

              int arr[] = { 1, 2, 3, 4, 5, 6 };
              int n = arr.length;

             EvenOddAbsoluteDifference(arr, n);
     }
     // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to find absolute difference of
# elements at even and odd index positions separately

# Function to calculate absolute difference
def EvenOddAbsoluteDifference(arr, n):
    even = 0
    odd = 0

    for i in range(0, n, 1):

        # Loop to find even, odd absolute
        # difference
        if (i % 2 == 0):
            even = abs(even - arr[i]);
        else:
            odd = abs(odd - arr[i]);

    print("Even Index absolute difference :", even)
    print("Odd Index absolute difference :", odd)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6]
    n = len(arr)

    EvenOddAbsoluteDifference(arr, n)

# This code is contributed by
# Sahil_shelangia
```

## C#

```
// C# program to find absolute difference
// of elements at even and odd index
// positions separately
using System;

class GFG
{
// Function to calculate absolute difference
static void EvenOddAbsoluteDifference(int []arr,
                                      int n)
{
    int even = 0;
    int odd = 0;

    for (int i = 0; i < n; i++)
    {

        // Loop to find even, odd
        // absolute difference
        if (i % 2 == 0)
            even = Math.Abs(even - arr[i]);
        else
            odd = Math.Abs(odd - arr[i]);
    }

    Console.WriteLine("Even Index absolute " +
                      "difference : " + even);
    Console.WriteLine("Odd Index absolute " +
                      "difference : " + odd);
}

// Driver Code
static public void Main ()
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    int n = arr.Length;
    EvenOddAbsoluteDifference(arr, n);
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find absolute
// difference of elements at even
// and odd index positions separately

// Function to calculate absolute
// difference
function EvenOddAbsoluteDifference($arr, $n)
{
    $even = 0;
    $odd = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Loop to find even, odd
        // absolute difference
        if ($i % 2 == 0)
            $even = abs($even - $arr[$i]);
        else
            $odd = abs($odd - $arr[$i]);
    }

    echo "Even Index absolute difference : ",
                                       $even;
    echo "\n";
    echo "Odd Index absolute difference : ",
                                       $odd;
}

// Driver Code
$arr = array( 1, 2, 3, 4, 5, 6 );
$n = sizeof($arr);

EvenOddAbsoluteDifference($arr, $n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

    // Javascript program to find absolute difference
    // of elements at even and odd index
    // positions separately

    // Function to calculate absolute difference
    function EvenOddAbsoluteDifference(arr, n)
    {
        let even = 0;
        let odd = 0;

        for (let i = 0; i < n; i++)
        {

            // Loop to find even, odd
            // absolute difference
            if (i % 2 == 0)
                even = Math.abs(even - arr[i]);
            else
                odd = Math.abs(odd - arr[i]);
        }

        document.write("Even Index absolute " +
                          "difference : " + even + "</br>");
        document.write("Odd Index absolute " +
                          "difference : " + odd + "</br>");
    }

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;
    EvenOddAbsoluteDifference(arr, n);

</script>
```

**Output:** 

```
Even Index absolute difference : 3
Odd Index absolute difference : 4
```

**时间复杂度:** O(n)