# 求最大连续偶数的个数

> 原文:[https://www . geesforgeks . org/find-最大连续偶数计数/](https://www.geeksforgeeks.org/find-the-count-of-maximum-contiguous-even-numbers/)

给定一个由 N 个元素组成的数组*arr[]*。任务是找出给定数组中连续偶数的最大数量。
**示例** :

> **输入** : arr[] = {1，2，3，4，6，7}
> **输出** : 2
> 最大连续偶数序列为{4，6}
> **输入** : arr[] = {1，0，2，4，3，8，9}
> **输出** : 3
> 最大连续偶数序列为{0，2，4}

**方法:**想法是用两个计数变量 current_max 和 max_so_far 继续遍历数组。如果找到一个偶数，则递增 current_max，并将其与 max_so_far 进行比较。每次发现奇数元素时，将 current_max 复位为 0。
以下是上述办法的实施情况:

## C++

```
// CPP program to count maximum
// contiguous even numbers

#include <iostream>
using namespace std;

// Function to count maximum
// contiguous even numbers
int countMaxContiguous(int arr[], int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++) {

        // If current element is not even
        // reset current_max
        if (arr[i] % 2 != 0)
            current_max = 0;

        // If even element is found, increment
        // current_max and update result if
        // count becomes more
        else {
            current_max++; // increase count
            max_so_far = max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 2, 4, 3, 8, 9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countMaxContiguous(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count maximum
// contiguous even numbers
import java.io.*;

class GFG
{

// Function to count maximum
// contiguous even numbers
static int countMaxContiguous(int arr[], int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is not
        // even reset current_max
        if (arr[i] % 2 != 0)
            current_max = 0;

        // If even element is found, increment
        // current_max and update result if
        // count becomes more
        else
        {
            current_max++; // increase count
            max_so_far = Math.max(current_max,
                                  max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 0, 2, 4, 3, 8, 9 };

    int n = arr.length;

    System.out.println(countMaxContiguous(arr, n));
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to count maximum
# contiguous even numbers

# Function to count maximum
# contiguous even numbers
def countMaxContiguous(arr, n):

    current_max = 0
    max_so_far = 0

    for i in range(n) :

        # If current element is not
        # even reset current_max
        if (arr[i] % 2 != 0):
            current_max = 0

        # If even element is found,
        # increment current_max and
        # update result if count
        # becomes more
        else :
            current_max += 1 # increase count
            max_so_far = max(current_max,
                             max_so_far)

    return max_so_far

# Driver code
if __name__ == "__main__":

    arr = [ 1, 0, 2, 4, 3, 8, 9 ]

    n = len(arr)

    print(countMaxContiguous(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count maximum
// contiguous even numbers
using System;

class GFG
{

// Function to count maximum
// contiguous even numbers
static int countMaxContiguous(int []arr, int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is not
        // even reset current_max
        if (arr[i] % 2 != 0)
            current_max = 0;

        // If even element is found, increment
        // current_max and update result if
        // count becomes more
        else
        {
            current_max++; // increase count
            max_so_far = Math.Max(current_max,
                                max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
public static void Main ()
{
    int []arr = { 1, 0, 2, 4, 3, 8, 9 };
      int n = arr.Length;

    Console.WriteLine(countMaxContiguous(arr, n));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count maximum
// contiguous even numbers

// Function to count maximum
// contiguous even numbers
function countMaxContiguous(&$arr, $n)
{
    $max_so_far=0;
    for ($i = 0; $i < $n; $i++)
    {

        // If current element is not
        // even reset current_max
        if ($arr[$i] % 2 != 0)
            $current_max = 0;

        // If even element is found, 
        // increment current_max and
        // update result if count
        // becomes more
        else
        {
            // increase count
            $current_max = $current_max + 1;
            $max_so_far = max($current_max,
                              $max_so_far);
        }
    }

    return $max_so_far;
}

// Driver code
$arr = array(1, 0, 2, 4, 3, 8, 9 );
$n = sizeof($arr);

echo countMaxContiguous($arr, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to count maximum
// contiguous even numbers

// Function to count maximum
// contiguous even numbers
function countMaxContiguous(arr, n)
{
    let current_max = 0, max_so_far = 0;

    for (let i = 0; i < n; i++) {

        // If current element is not even
        // reset current_max
        if (arr[i] % 2 != 0)
            current_max = 0;

        // If even element is found, increment
        // current_max and update result if
        // count becomes more
        else {
            current_max++; // increase count
            max_so_far = Math.max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver code

    let arr = [ 1, 0, 2, 4, 3, 8, 9 ];

    let n = arr.length;

    document.write(countMaxContiguous(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3
```