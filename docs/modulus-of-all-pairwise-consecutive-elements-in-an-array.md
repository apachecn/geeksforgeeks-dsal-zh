# 数组中所有成对连续元素的模

> 原文:[https://www . geesforgeks . org/数组中所有成对连续元素的模数/](https://www.geeksforgeeks.org/modulus-of-all-pairwise-consecutive-elements-in-an-array/)

给定一组![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")元素。任务是打印所有成对连续元素的模数。也就是说，对于所有连续的元素对(a[i]，a[i+1])，打印 **(a[i] % a[i+1])** 。
**注**:大小为 N 的数组的连续对是(a[i]，a[i+1])，范围从 0 到 N-2。
**示例** :

```
Input: arr[] = {8, 5, 4, 3, 15, 20}
Output: 3 1 1 3 15 

Input: arr[] = {5, 10, 15, 20}
Output: 5 10 15 
```

**方法:**解决方法是遍历数组，计算并打印每对(arr[i]，arr[i+1])的模。
以下是上述办法的实施情况:

## C++

```
// C++ program to print the modulus
// of the consecutive elements
#include <iostream>
using namespace std;

// Function to print pairwise modulus
// of consecutive elements
void pairwiseModulus(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++) {

        // Modulus of consecutive numbers
        cout << (arr[i] % arr[i + 1]) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 8, 5, 4, 3, 15, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pairwiseModulus(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the modulus
// of the consecutive elements
import java.util.*;

class Geeks {

// Function to print pairwise modulus
// of consecutive elements
static void pairwiseModulus(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++) {

        // Modulus of consecutive numbers
        System.out.println((arr[i] % arr[i + 1]));
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 8, 5, 4, 3, 15, 20 };
    int n = arr.length;

    pairwiseModulus(arr, n);
}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python 3 program to print the modulus
# of the consecutive elements

# Function to print pairwise modulus
# of consecutive elements
def pairwiseModulus(arr, n):
    for i in range(0, n - 1, 1):

        # Modulus of consecutive numbers
        print((arr[i] % arr[i + 1]),
                         end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [8, 5, 4, 3, 15, 20]
    n = len(arr)
    pairwiseModulus(arr, n)

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to print the modulus
// of the consecutive elements
using System;

class Geeks {

// Function to print pairwise modulus
// of consecutive elements
static void pairwiseModulus(int[] arr, int n)
{
    for (int i = 0; i < n - 1; i++) {

        // Modulus of consecutive numbers
        Console.WriteLine((arr[i] % arr[i + 1]));
    }
}

// Driver Code
public static void Main(String []args)
{
    int[] arr = {8, 5, 4, 3, 15, 20};
    int n = arr.Length;

    pairwiseModulus(arr, n);
}
}

// This code is contributed by ankita_saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to print the modulus
// of the consecutive elements

// Function to print pairwise modulus
// of consecutive elements
function pairwiseModulus( $arr, $n)
{
    for ($i = 0; $i < $n - 1; $i++) {

        // Modulus of consecutive numbers
        echo  ($arr[$i] % $arr[$i + 1]), " ";
    }
}

// Driver Code
    $arr = array( 8, 5, 4, 3, 15, 20 );
    $n = sizeof($arr) / sizeof($arr[0]);

    pairwiseModulus($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to print the modulus
// of the consecutive elementsclass Geeks {

    // Function to print pairwise modulus
    // of consecutive elements
    function pairwiseModulus(arr , n) {
        for (i = 0; i < n - 1; i++) {

            // Modulus of consecutive numbers
            document.write((arr[i] % arr[i + 1]) + " ");
        }
    }

    // Driver Code

        var arr = [ 8, 5, 4, 3, 15, 20 ];
        var n = arr.length;

        pairwiseModulus(arr, n);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
3 1 1 3 15
```

**时间复杂度:**O(n)
T3**辅助空间** : O(1)