# 偶数位置的偶数之和

> 原文:[https://www . geesforgeks . org/sum-偶数-偶数-位置/](https://www.geeksforgeeks.org/sum-even-numbers-even-position/)

给定一个大小为 n 的数组，问题是找出偶数和索引为偶数的数的和。
**例:**

```
Input :  arr[] = {5, 6, 12, 1, 18, 8}
Output : 30
Explanation: Here, n = 6 
Now here are index and numbers as: index->arr[index]
0->5, 1->6, 2->12, 3->1, 4->18, 5->8
so, number which are even and are at even indices 
are: 2->12, 4->18
sum = 12+18 = 30

Input  : arr[] = {3, 20, 17, 9, 2, 10, 
                        18, 13, 6, 18}
Output : 26
Explanation: Here, n = 10
Now here are index and numbers as: index->arr[index]
0->3, 1->20, 2->17, 3->9, 4->2, 5->10, 
6->18, 7->13, 8->6, 9->18 
So, number which are even and are at even indices are: 
4->2, 6->18, 8->6
sum = 2+18+6 = 26
```

## C++

```
// C++ implementation to
// find sum of even numbers
// at even indices
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum
// of even numbers at even indices
int sum_even_and_even_index(
                int arr[], int n) {

    int i = 0, sum = 0;

    // calculating sum of even
    // number at even index
    for (i = 0; i < n; i+=2) {

        if (arr[i] % 2 == 0) {

            sum += arr[i];
        }
    }

    // required sum
    return sum;
}

// Driver program to test above
int main() {
    int arr[] = {5, 6, 12, 1, 18, 8};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Sum of even numbers at even indices is "
         << sum_even_and_even_index(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum of
// even numbers at even indices

import java.io.*;

class GFG {

    // Function to calculate sum
    // of even numbers at even indices
    static int sum_even_and_even_index(
                       int arr[], int n)
    {

        int i = 0, sum = 0;

        // calculating sum of even
        // number at even index
        for (i = 0; i < n; i+=2) {

            if (arr[i] % 2 == 0) {
                sum += arr[i];
            }
        }

        // required sum
        return sum;
    }

    // Driver program to test above
    public static void main (String[] args) {

        int arr[] = {5, 6, 12, 1, 18, 8};
        int n = arr.length;
        System.out.println("Sum of even numbers"
                      + " at even indices is " +
             + sum_even_and_even_index(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# python 3 implementation to
# find sum of even numbers
# at even indices

# Function to calculate sum
# of even numbers at even indices
def sum_even_and_even_index(arr,n):

    i = 0
    sum = 0

# calculating sum of even
# number at even index
    for i in range(0,n,2):
        if (arr[i] % 2 == 0) :
            sum += arr[i]

    # required sum
    return sum

# Driver program to test above
arr = [5, 6, 12, 1, 18, 8]
n = len(arr)
print("Sum of even numbers at ",
             "even indices is ",
   sum_even_and_even_index(arr, n))

# This code is contributed by Sam007
```

## C#

```
// C# implementation to find sum of
// even numbers at even indices

using System;

class GFG {

    // Function to calculate sum
    // of even numbers at even indices
    static int sum_even_and_even_index(
                    int []arr, int n)
    {

        int i = 0, sum = 0;

        // calculating sum of even
        // number at even index
        for (i = 0; i < n; i+=2) {

            if (arr[i] % 2 == 0) {

                sum += arr[i];
            }
        }

        // required sum
        return sum;
    }

    // Driver program to test above
    public static void Main () {

        int []arr = {5, 6, 12, 1, 18, 8};
        int n = arr.Length;
        Console.WriteLine("Sum of even numbers"
                    + " at even indices is " +
            + sum_even_and_even_index(arr, n));
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find sum of even numbers
// at even indices

// Function to calculate sum
// of even numbers at even indices
function sum_even_and_even_index($arr, $n)
{

    $i = 0; $sum = 0;

    // calculating sum of even
    // number at even index
    for ($i = 0; $i < $n; $i=$i+2) {

        if ($arr[$i] % 2 == 0) {

            $sum += $arr[$i];
        }
    }

    // required sum
    return $sum;
}

// Driver Code
{
    $arr = array(5, 6, 12, 1, 18, 8);
    $n = sizeof($arr) / sizeof($arr[0]);
    echo "Sum of even numbers at ".
                 "even indices is ",
          sum_even_and_even_index($arr, $n);

    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to
// find sum of even numbers
// at even indices

// Function to calculate sum
// of even numbers at even indices
function sum_even_and_even_index(
                arr, n) {

    let i = 0, sum = 0;

    // calculating sum of even
    // number at even index
    for (i = 0; i < n; i += 2)
    {
        if (arr[i] % 2 == 0)
        {   
            sum += arr[i];
        }
    }

    // required sum
    return sum;
}

// Driver code
    let arr = [5, 6, 12, 1, 18, 8];
    let n = arr.length;
    document.write("Sum of even numbers at even indices is "
        + sum_even_and_even_index(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
 Sum of even numbers at even indices is 30
```