# 阵列中最大的间隙

> 原文:[https://www.geeksforgeeks.org/largest-gap-in-an-array/](https://www.geeksforgeeks.org/largest-gap-in-an-array/)

给定一个长度为 N 的未排序数组，我们必须找到数组中任意两个元素之间的最大间距。简单来说，求 max(|A <sub>i</sub> -A <sub>j</sub> |)其中 1 ≤ i ≤ N，1 ≤ j ≤ N

**示例:**

```
Input : arr = {3, 10, 6, 7}
Output : 7
Explanation :
Here, we can see largest gap can be
found between 3 and 10 which is 7

Input : arr = {-3, -1, 6, 7, 0}
Output : 10
Explanation :
Here, we can see largest gap can be 
found between -3 and 7 which is 10 
```

**简单的方法:**
一个简单的解决方法是，我们可以用一个幼稚的方法。我们将检查数组中每对的绝对差，我们将找到它的最大值。所以我们将运行两个循环，一个是 I，一个是 j，这个方法的复杂度是 O(N^2)

## C++

```
// A C++ program to find largest gap
// between two elements in an array.
#include<bits/stdc++.h>
using namespace std;

// function to solve the given problem
int solve(int a[], int n)
{
    int max1 = INT_MIN;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (abs(a[i] - a[j]) > max1)
            {
                max1 = abs(a[i] - a[j]);
            }
        }
    }
    return max1;
}

// Driver Code
int main()
{
    int arr[] = { -1, 2, 3, -4, -10, 22 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << "Largest gap is : "
         << solve(arr, size);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// A C program to find largest gap
// between two elements in an array.
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

// function to solve the given problem
int solve(int a[], int n)
{
    int max1 = INT_MIN;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (abs(a[i] - a[j]) > max1) {
                max1 = abs(a[i] - a[j]);
            }
        }
    }
    return max1;
}

int main()
{
    int arr[] = { -1, 2, 3, -4, -10, 22 };
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("Largest gap is : %d", solve(arr, size));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// largest gap between
// two elements in an array.
import java .io.*;

class GFG
{

// function to solve
// the given problem
static int solve(int []a,
                 int n)
{
    int max1 = Integer.MIN_VALUE ;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (Math.abs(a[i] -
                         a[j]) > max1)
            {
                max1 = Math.abs(a[i] -
                                a[j]);
            }
        }
    }
    return max1;
}

// Driver Code
static public void main (String[] args)
{
    int []arr = {-1, 2, 3,
                 -4, -10, 22};
    int size = arr.length;
    System.out.println("Largest gap is : " +
                        solve(arr, size));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# A Python 3 program to find largest gap
# between two elements in an array.
import sys

# function to solve the given problem
def solve(a, n):
    max1 = -sys.maxsize - 1
    for i in range(0, n, 1):
        for j in range(0, n, 1):
            if (abs(a[i] - a[j]) > max1):
                max1 = abs(a[i] - a[j])

    return max1

# Driver Code
if __name__ == '__main__':
    arr = [-1, 2, 3, -4, -10, 22]
    size = len(arr)
    print("Largest gap is :", solve(arr, size))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// A C# program to find
// largest gap between
// two elements in an array.
using System;

class GFG
{

// function to solve
// the given problem
static int solve(int []a,
                 int n)
{
    int max1 = int.MinValue ;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (Math.Abs(a[i] -
                         a[j]) > max1)
            {
                max1 = Math.Abs(a[i] -
                                a[j]);
            }
        }
    }
    return max1;
}

// Driver Code
static public void Main ()
{
    int []arr = {-1, 2, 3,
                 -4, -10, 22};
    int size = arr.Length;
    Console.WriteLine("Largest gap is : " +
                         solve(arr, size));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find
// largest gap between
// two elements in an array.

// function to solve
// the given problem
function solve($a, $n)
{
    $max1 = PHP_INT_MIN;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if (abs($a[$i] -
                    $a[$j]) > $max1)
            {
                $max1 = abs($a[$i] -
                            $a[$j]);
            }
        }
    }
    return $max1;
}

// Driver Code
$arr = array(-1, 2, 3,
             -4, -10, 22);
$size = count($arr);
echo "Largest gap is : ",
      solve($arr, $size);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

// A Javascript program to find
// largest gap between
// two elements in an array.

    // function to solve
// the given problem
    function solve(a,n)
    {
        let max1 = Number.MIN_VALUE ;

    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
        {
            if (Math.abs(a[i] - a[j]) > max1)
            {

                max1 = Math.abs(a[i] - a[j]);
            }
        }
    }
    return max1;
    }

    // Driver Code
    let arr=[-1, 2, 3,
                 -4, -10, 22];
    let size = arr.length;
    document.write("Largest gap is : " +
                         solve(arr, size));

    // This code is contributed by rag2127

</script>
```

**Output:** 

```
Largest gap is : 32
```

**更好的方法:**
现在我们将看到一个更好的方法它是一个贪婪的方法，可以在 O(N)中解决这个问题。我们将找到数组的最大和最小元素，这可以在 O(N)中完成，然后我们将返回(最大-最小)的值。

## C++

```
// A C++ program to find largest gap between
// two elements in an array.
#include<bits/stdc++.h>
using namespace std;

// function to solve the given problem
int solve(int a[], int n)
{
    int min1 = a[0];
    int max1 = a[0];

    // finding maximum and minimum of an array
    for (int i = 0; i < n; i++)
    {
        if (a[i] > max1)
            max1 = a[i];
        if (a[i] < min1)
            min1 = a[i];
    }
    return abs(min1 - max1);
}

// Driver code
int main()
{
    int arr[] = { -1, 2, 3, 4, -10 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << "Largest gap is : " << solve(arr, size);
    return 0;
}

//This code is contributed by Mukul Singh.
```

## C

```
// A C program to find largest gap between
// two elements in an array.
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

// function to solve the given problem
int solve(int a[], int n)
{
    int min1 = a[0];
    int max1 = a[0];

    // finding maximum and minimum of an array
    for (int i = 0; i < n; i++) {
        if (a[i] > max1)
            max1 = a[i];
        if (a[i] < min1)
            min1 = a[i];
    }

    return abs(min1 - max1);
}

int main()
{
    int arr[] = { -1, 2, 3, 4, -10 };
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("Largest gap is : %d", solve(arr, size));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find largest gap
// between two elements in an array.
import java.io.*;

class GFG {

    // function to solve the given
    // problem
    static int solve(int a[], int n)
    {
        int min1 = a[0];
        int max1 = a[0];

        // finding maximum and minimum
        // of an array
        for (int i = 0; i < n; i++)
        {
            if (a[i] > max1)
                max1 = a[i];
            if (a[i] < min1)
                min1 = a[i];
        }

        return Math.abs(min1 - max1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int []arr = { -1, 2, 3, 4, -10 };
        int size = arr.length;
        System.out.println("Largest gap is : "
                         + solve(arr, size));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# A python 3 program to find largest gap between
# two elements in an array.

# function to solve the given problem
def solve(a,  n):

    min1 = a[0]
    max1 = a[0]

    # finding maximum and minimum of an array
    for i in range ( n):

        if (a[i] > max1):
            max1 = a[i]
        if (a[i] < min1):
            min1 = a[i]

    return abs(min1 - max1)

# Driver code
if __name__ == "__main__":

    arr = [ -1, 2, 3, 4, -10 ]
    size = len(arr)
    print("Largest gap is : " ,solve(arr, size))

# This code is contributed by chitranayal 
```

## C#

```
// A C# program to find
// largest gap between
// two elements in an array.
using System;

class GFG
{

    // function to solve
    // the given problem
    static int solve(int []a,
                     int n)
    {
        int min1 = a[0];
        int max1 = a[0];

        // finding maximum and
        // minimum of an array
        for (int i = 0; i < n; i++)
        {
            if (a[i] > max1)
                max1 = a[i];
            if (a[i] < min1)
                min1 = a[i];
        }

        return Math.Abs(min1 -
                        max1);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {-1, 2, 3, 4, -10};
        int size = arr.Length;
        Console.WriteLine("Largest gap is : " +
                             solve(arr, size));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find
// largest gap between
// two elements in an array.

// function to solve
// the given problem
function solve($a, $n)
{
    $min1 = $a[0];
    $max1 = $a[0];

    // finding maximum and
    // minimum of an array
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] > $max1)
            $max1 = $a[$i];
        if ($a[$i] < $min1)
            $min1 = $a[$i];
    }

    return abs($min1 - $max1);
}

// Driver Code
$arr = array(-1, 2, 3, 4, -10);
$size = count($arr);
echo "Largest gap is : ",
      solve($arr, $size);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
// A Javascript program to find largest gap
// between two elements in an array.

    // function to solve the given
    // problem
    function solve(a,n)
    {
        let min1 = a[0];
        let max1 = a[0];

        // finding maximum and minimum
        // of an array
        for (let i = 0; i < n; i++)
        {
            if (a[i] > max1)
                max1 = a[i];
            if (a[i] < min1)
                min1 = a[i];
        }

        return Math.abs(min1 - max1);
    }

     // Driver code
    let arr=[-1, 2, 3, 4, -10 ];
    let size = arr.length;
    document.write("Largest gap is : "
                         + solve(arr, size));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Largest gap is : 14
```