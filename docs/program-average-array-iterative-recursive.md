# 数组平均程序(迭代和递归)

> 原文:[https://www . geesforgeks . org/program-average-array-iterative-recursive/](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)

给定一个数组，任务是找到该数组的平均值。Average 是数组元素的总和除以元素的数量。

**示例:**

```
Input : arr[] = {1, 2, 3, 4, 5}
Output : 3
Sum of the elements is 1+2+3+4+5 = 15 
and total number of elements is 5.
So average is 15/5 = 3

Input : arr[] = {5, 3, 6, 7, 5, 3}
Output : 4.83333
Sum of the elements is 5+3+6+7+5+3 = 29
and total number of elements is 6.
So average is 29/6 = 4.83333.
```

**迭代:**
迭代程序很容易。我们需要求和并将和除以元素总数。

## C++

```
// C++ program to calculate average of array elements
#include <iostream>
using namespace std;

// Function that return average of an array.
double average(int a[], int n)
{
    // Find sum of array element
    int sum = 0;
    for (int i=0; i<n; i++)
       sum += a[i];

    return (double)sum/n;
}

// Driver code
int main()
{
    int arr[] = {10, 2, 3, 4, 5, 6, 7, 8, 9};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << average(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate average of array elements
class GFG {

    // Function that return average of an array.
    static double average(int a[], int n)
    {

        // Find sum of array element
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += a[i];

        return (double)sum / n;
    }

    //driver code
    public static void main (String[] args)
    {

        int arr[] = {10, 2, 3, 4, 5, 6, 7, 8, 9};
        int n = arr.length;

        System.out.println(average(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 code to calculate
# average of array elements

# Function that return
# average of an array.
def average( a , n ):

    # Find sum of array element
    sum = 0
    for i in range(n):
        sum += a[i]

    return sum/n;

# Driver code
arr = [10, 2, 3, 4, 5, 6, 7, 8, 9]
n = len(arr)
print(average(arr, n))

# This code is contributed by "Shard_Bhardwaj".
```

## C#

```
// C# program to calculate average of
// array elements
using System;
class GFG {

    // Function that return average of
    // an array.
    static double average(int []a, int n)
    {

        // Find sum of array element
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += a[i];

        return (double)sum / n;
    }

    // Driver code
    public static void Main ()
    {

        int []arr = {10, 2, 3, 4, 5, 6,
                                7, 8, 9};
        int n = arr.Length;

        Console.Write(average(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate average
// of array elements

// Function that return average of
// an array.
function average( $a, $n)
{

    // Find sum of array element
    $sum = 0;
    for ( $i = 0; $i < $n; $i++)
        $sum += $a[$i];

    return $sum / $n;
}

// Driver code
    $arr = array(10, 2, 3, 4, 5,
                        6, 7, 8, 9);
    $n = count($arr);

    echo average($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
      // JavaScript program to calculate average of array elements

      // Function that return average of an array.
      function average(a, n)
      {

        // Find sum of array element
        var sum = 0;
        for (var i = 0; i < n; i++) sum += a[i];

        return parseFloat(sum / n);
      }

      // Driver code

      var arr = [10, 2, 3, 4, 5, 6, 7, 8, 9];
      var n = arr.length;

      document.write(average(arr, n));
      document.write("<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output**

```
6
```