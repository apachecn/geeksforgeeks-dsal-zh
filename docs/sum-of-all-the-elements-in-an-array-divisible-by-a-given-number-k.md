# 可被给定数字 K 整除的数组中所有元素的总和

> 原文:[https://www . geeksforgeeks . org/数组中所有元素的总和可被给定数字 k 整除/](https://www.geeksforgeeks.org/sum-of-all-the-elements-in-an-array-divisible-by-a-given-number-k/)

给定一个包含 N 个元素和一个数字 k 的数组，任务是找出所有可被 k 整除的元素的和
**示例** :

```
Input : arr[] = {15, 16, 10, 9, 6, 7, 17}
        K = 3
Output : 30
Explanation: As 15, 9, 6 are divisible by 3\. So, sum of elements divisible by K = 15 + 9 + 6 = 30.

Input : arr[] = {5, 3, 6, 8, 4, 1, 2, 9}
        K = 2
Output : 20
```

这个想法是遍历数组并逐个检查元素。如果一个元素可以被 K 整除，那么把这个元素的值和到目前为止的总和相加，并在到达数组末尾时继续这个过程。
以下是上述方法的实现:

## C++

```
// C++ program to find sum of all the elements
// in an array divisible by a given number K

#include <iostream>
using namespace std;

// Function to find sum of all the elements
// in an array divisible by a given number K
int findSum(int arr[], int n, int k)
{
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If current element is divisible by k
        // add it to sum
        if (arr[i] % k == 0) {
            sum += arr[i];
        }
    }

    // Return calculated sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 15, 16, 10, 9, 6, 7, 17 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << findSum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all the elements
// in an array divisible by a given number K

import java.io.*;

class GFG {

// Function to find sum of all the elements
// in an array divisible by a given number K
static int findSum(int arr[], int n, int k)
{
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If current element is divisible by k
        // add it to sum
        if (arr[i] % k == 0) {
            sum += arr[i];
        }
    }

    // Return calculated sum
    return sum;
}

    // Driver code
    public static void main (String[] args) {

    int arr[] = { 15, 16, 10, 9, 6, 7, 17 };
    int n = arr.length;
    int k = 3;

    System.out.println( findSum(arr, n, k));
    }
}

// this code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find sum of
# all the elements in an array
# divisible by a given number K

# Function to find sum of all
# the elements in an array
# divisible by a given number K
def findSum(arr, n, k) :

    sum = 0

    # Traverse the array
    for i in range(n) :

        # If current element is divisible
        # by k add it to sum
        if arr[i] % k == 0 :

            sum += arr[i]

    # Return calculated sum
    return sum

# Driver code
if __name__ == "__main__" :

    arr = [ 15, 16, 10, 9, 6, 7, 17]
    n = len(arr)
    k = 3

    print(findSum(arr, n, k))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find sum of all the elements
// in an array divisible by a given number K

using System;

public class GFG{

// Function to find sum of all the elements
// in an array divisible by a given number K
static int findSum(int []arr, int n, int k)
{
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If current element is divisible by k
        // add it to sum
        if (arr[i] % k == 0) {
            sum += arr[i];
        }
    }

    // Return calculated sum
    return sum;
}

    // Driver code

    static public void Main (){

    int []arr = { 15, 16, 10, 9, 6, 7, 17 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine( findSum(arr, n, k));
    }
}
//This code is contributed by anuj_67..

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of all
// the elements in an array divisible
// by a given number K

// Function to find sum of all
// the elements in an array
// divisible by a given number K
function findSum($arr, $n, $k)
{
    $sum = 0;

    // Traverse the array
    for ($i = 0; $i < $n; $i++)
    {

        // If current element is divisible
        // by k add it to sum
        if ($arr[$i] % $k == 0)
        {
            $sum += $arr[$i];
        }
    }

    // Return calculated sum
    return $sum;
}

// Driver code
$arr = array(15, 16, 10, 9, 6, 7, 17);
$n = sizeof($arr);
$k = 3;

echo findSum($arr, $n, $k);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
    // Javascript program to find sum of all the elements
    // in an array divisible by a given number K

    // Function to find sum of all the elements
    // in an array divisible by a given number K
    function findSum(arr, n, k)
    {
        let sum = 0;

        // Traverse the array
        for (let i = 0; i < n; i++) {

            // If current element is divisible by k
            // add it to sum
            if (arr[i] % k == 0) {
                sum += arr[i];
            }
        }

        // Return calculated sum
        return sum;
    }

    let arr = [ 15, 16, 10, 9, 6, 7, 17 ];
    let n = arr.length;
    let k = 3;

    document.write(findSum(arr, n, k));

</script>
```

**Output:** 

```
30
```

**时间复杂度** : O(N)，其中 N 为数组中的元素个数。
**辅助空间:** O(1)