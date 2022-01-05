# 找出两个缺失的数字|集合 1(一个有趣的线性时间解)

> 原文:[https://www . geesforgeks . org/find-two-missing-numbers-set-1-一个有趣的线性时间解决方案/](https://www.geeksforgeeks.org/find-two-missing-numbers-set-1-an-interesting-linear-time-solution/)

给定 n 个唯一整数的数组，其中数组中的每个元素都在[1，n]的范围内。数组包含所有不同的元素，数组的大小为(n-2)。因此，该数组中缺少该范围内的两个数字。找出两个丢失的数字。
**例:**

```
Input  : arr[] = {1, 3, 5, 6}
Output : 2 4

Input : arr[] = {1, 2, 4}
Output : 3 5

Input : arr[] = {1, 2}
Output : 3 4
```

**方法 1–O(n)时间复杂度和 O(n)额外空间**

**第一步:**取一个布尔数组*标记*，跟踪数组中存在的所有元素。
**第二步:**从 1 到 n 迭代，检查每个元素在布尔数组中是否标记为真，如果不是，则简单地显示该元素。

## C++

```
// C++ Program to find two Missing Numbers using O(n)
// extra space
#include <bits/stdc++.h>
using namespace std;

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
void findTwoMissingNumbers(int arr[], int n)
{
    // Create a boolean vector of size n+1 and
    // mark all present elements of arr[] in it.
    vector<bool> mark(n+1, false);
    for (int i = 0; i < n-2; i++)
        mark[arr[i]] = true;

    // Print two unmarked elements
    cout << "Two Missing Numbers are\n";
    for (int i = 1; i <= n; i++)
       if (! mark[i])
           cout << i << " ";

    cout << endl;
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 3, 5, 6};

    // Range of numbers is 2 plus size of array
    int n = 2 + sizeof(arr)/sizeof(arr[0]);

    findTwoMissingNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find two Missing Numbers using O(n)
// extra space
import java.util.*;

class GFG
{

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
static void findTwoMissingNumbers(int arr[], int n)
{
    // Create a boolean vector of size n+1 and
    // mark all present elements of arr[] in it.
    boolean []mark = new boolean[n+1];
    for (int i = 0; i < n-2; i++)
        mark[arr[i]] = true;

    // Print two unmarked elements
    System.out.println("Two Missing Numbers are");
    for (int i = 1; i <= n; i++)
    if (! mark[i])
        System.out.print(i + " ");

    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {1, 3, 5, 6};

    // Range of numbers is 2 plus size of array
    int n = 2 + arr.length;

    findTwoMissingNumbers(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find two Missing Numbers using O(n)
# extra space

# Function to find two missing numbers in range
# [1, n]. This function assumes that size of array
# is n-2 and all array elements are distinct
def findTwoMissingNumbers(arr, n):
    # Create a boolean vector of size n+1 and
    # mark all present elements of arr[] in it.
    mark = [False for i in range(n+1)]
    for i in range(0,n-2,1):
        mark[arr[i]] = True

    # Print two unmarked elements
    print("Two Missing Numbers are")
    for i in range(1,n+1,1):
        if (mark[i] == False):
            print(i,end = " ")

    print("\n")

# Driver program to test above function
if __name__ == '__main__':
    arr = [1, 3, 5, 6]

    # Range of numbers is 2 plus size of array
    n = 2 + len(arr)

    findTwoMissingNumbers(arr, n);

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find two Missing Numbers
// using O(n) extra space
using System;
using System.Collections.Generic;

class GFG
{

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
static void findTwoMissingNumbers(int []arr, int n)
{
    // Create a boolean vector of size n+1 and
    // mark all present elements of arr[] in it.
    Boolean []mark = new Boolean[n + 1];
    for (int i = 0; i < n - 2; i++)
        mark[arr[i]] = true;

    // Print two unmarked elements
    Console.WriteLine("Two Missing Numbers are");
    for (int i = 1; i <= n; i++)
    if (! mark[i])
        Console.Write(i + " ");

    Console.WriteLine();
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {1, 3, 5, 6};

    // Range of numbers is 2 plus size of array
    int n = 2 + arr.Length;

    findTwoMissingNumbers(arr, n);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript Program to find two
    // Missing Numbers using O(n) extra space

    // Function to find two missing numbers in range
    // [1, n]. This function assumes that size of array
    // is n-2 and all array elements are distinct
    function findTwoMissingNumbers(arr, n)
    {
        // Create a boolean vector of size n+1 and
        // mark all present elements of arr[] in it.
        let mark = new Array(n+1);
        for (let i = 0; i < n-2; i++)
            mark[arr[i]] = true;

        // Print two unmarked elements
        document.write("Two Missing Numbers are" + "</br>");
        for (let i = 1; i <= n; i++)
            if (!mark[i])
                document.write(i + " ");

        document.write("</br>");
    }

    let arr = [1, 3, 5, 6];

    // Range of numbers is 2 plus size of array
    let n = 2 + arr.length;

    findTwoMissingNumbers(arr, n);

</script>
```

**输出:**

```
Two Missing Numbers are
2 4
```

**方法 2–O(n)时间复杂度和 O(1)额外空间**

这个想法是基于[这个](https://www.geeksforgeeks.org/find-the-missing-number/)流行的寻找一个缺失数字的解决方案。我们扩展了解决方案，以便打印两个缺失的元素。
让我们找出两个缺失数字的和:

```
arrSum => Sum of all elements in the array

sum (Sum of 2 missing numbers) = (Sum of integers from 1 to n) - arrSum
                               = ((n)*(n+1))/2 – arrSum 

avg (Average of 2 missing numbers) = sum / 2;
```

*   其中一个数字将小于或等于**平均值**，而另一个数字将严格大于**平均值**。两个数字永远不可能相等，因为所有给定的数字都是不同的。
*   我们可以将第一个缺失的数作为从 1 到 **avg** 的自然数之和，即 avg*(avg+1)/2 **减去**小于 **avg** 的数组元素之和
*   我们可以通过从缺失数的总和中减去第一个缺失数来找到第二个缺失数

考虑一个更好澄清的例子

```
Input : 1 3 5 6, n = 6
Sum of missing integers = n*(n+1)/2 - (1+3+5+6) = 6.
Average of missing integers = 6/2 = 3.
Sum of array elements less than or equal to average = 1 + 3 = 4
Sum of natural numbers from 1 to avg = avg*(avg + 1)/2
                                     = 3*4/2 = 6
First missing number = 6 - 4 = 2
Second missing number = Sum of missing integers-First missing number
Second missing number = 6-2= 4
```

以下是上述想法的实现。

## C++

```
// C++ Program to find 2 Missing Numbers using O(1)
// extra space
#include <iostream>
using namespace std;

// Returns the sum of the array
int getSum(int arr[],int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
void findTwoMissingNumbers(int arr[],int n)
{
    // Sum of 2 Missing Numbers
    int sum = (n*(n + 1)) /2 - getSum(arr, n-2);

    // Find average of two elements
    int avg = (sum / 2);

    // Find sum of elements smaller than average (avg)
    // and sum of elements greater than average (avg)
    int sumSmallerHalf = 0, sumGreaterHalf = 0;
    for (int i = 0; i < n-2; i++)
    {
        if (arr[i] <= avg)
            sumSmallerHalf += arr[i];
        else
            sumGreaterHalf += arr[i];
    }

    cout << "Two Missing Numbers are\n";

    // The first (smaller) element = (sum of natural
    // numbers upto avg) - (sum of array elements
    // smaller than or equal to avg)
    int totalSmallerHalf = (avg*(avg + 1)) / 2;
    int smallerElement = totalSmallerHalf - sumSmallerHalf;
    cout << smallerElement << " ";

    // The second (larger) element = (sum of both
    // the elements) - smaller element
    cout << sum - smallerElement;
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 3, 5, 6};

    // Range of numbers is 2 plus size of array
    int n = 2 + sizeof(arr)/sizeof(arr[0]);

    findTwoMissingNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find 2 Missing
// Numbers using O(1) extra space
import java.io.*;

class GFG
{

// Returns the sum of the array
static int getSum(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to find two missing
// numbers in range [1, n]. This
// function assumes that size of
// array is n-2 and all array
// elements are distinct
static void findTwoMissingNumbers(int arr[],
                                  int n)
{
    // Sum of 2 Missing Numbers
    int sum = (n * (n + 1)) /
               2 - getSum(arr, n - 2);

    // Find average of two elements
    int avg = (sum / 2);

    // Find sum of elements smaller
    // than average (avg) and sum of
    // elements greater than average (avg)
    int sumSmallerHalf = 0,
        sumGreaterHalf = 0;
    for (int i = 0; i < n - 2; i++)
    {
        if (arr[i] <= avg)
            sumSmallerHalf += arr[i];
        else
            sumGreaterHalf += arr[i];
    }

    System.out.println("Two Missing " +
                       "Numbers are");

    // The first (smaller) element =
    // (sum of natural numbers upto
    // avg) - (sum of array elements
    // smaller than or equal to avg)
    int totalSmallerHalf = (avg *
                           (avg + 1)) / 2;
    System.out.println(totalSmallerHalf -
                         sumSmallerHalf);

    // The first (smaller) element =
    // (sum of natural numbers from
    // avg+1 to n) - (sum of array
    // elements greater than avg)
    System.out.println(((n * (n + 1)) / 2 -
                        totalSmallerHalf) -
                           sumGreaterHalf);
}

// Driver Code
public static void main (String[] args)
{
int arr[] = {1, 3, 5, 6};

// Range of numbers is 2
// plus size of array
int n = 2 + arr.length;

findTwoMissingNumbers(arr, n);
}
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python Program to find 2 Missing
# Numbers using O(1) extra space

# Returns the sum of the array
def getSum(arr,n):

    sum = 0;
    for i in range(0, n):
        sum += arr[i]
    return sum

# Function to find two missing
# numbers in range [1, n]. This
# function assumes that size of
# array is n-2 and all array
# elements are distinct
def findTwoMissingNumbers(arr, n):

    # Sum of 2 Missing Numbers
    sum = ((n * (n + 1)) / 2 -
           getSum(arr, n - 2));

    #Find average of two elements
    avg = (sum / 2);

    # Find sum of elements smaller
    # than average (avg) and sum
    # of elements greater than
    # average (avg)
    sumSmallerHalf = 0
    sumGreaterHalf = 0;
    for i in range(0, n - 2):

        if (arr[i] <= avg):
            sumSmallerHalf += arr[i]
        else:
            sumGreaterHalf += arr[i]

    print("Two Missing Numbers are")

    # The first (smaller) element = (sum
    # of natural numbers upto avg) - (sum
    # of array elements smaller than or
    # equal to avg)
    totalSmallerHalf = (avg * (avg + 1)) / 2
    print(str(totalSmallerHalf -
              sumSmallerHalf) + " ")

    # The first (smaller) element = (sum
    # of natural numbers from avg+1 to n) -
    # (sum of array elements greater than avg)
    print(str(((n * (n + 1)) / 2 -
               totalSmallerHalf) -
               sumGreaterHalf))

# Driver Code
arr = [1, 3, 5, 6]

# Range of numbers is 2
# plus size of array
n = 2 + len(arr)

findTwoMissingNumbers(arr, n)

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# Program to find 2 Missing
// Numbers using O(1) extra space
using System;

class GFG
{

// Returns the sum of the array
static int getSum(int []arr, int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to find two missing
// numbers in range [1, n]. This
// function assumes that size of
// array is n-2 and all array
// elements are distinct
static void findTwoMissingNumbers(int []arr,
                                  int n)
{
    // Sum of 2 Missing Numbers
    int sum = (n * (n + 1)) / 2 -
              getSum(arr, n - 2);

    // Find average of two elements
    int avg = (sum / 2);

    // Find sum of elements smaller
    // than average (avg) and sum of
    // elements greater than average (avg)
    int sumSmallerHalf = 0,
        sumGreaterHalf = 0;
    for (int i = 0; i < n - 2; i++)
    {
        if (arr[i] <= avg)
            sumSmallerHalf += arr[i];
        else
            sumGreaterHalf += arr[i];
    }

    Console.WriteLine("Two Missing " +
                      "Numbers are ");

    // The first (smaller) element =
    // (sum of natural numbers upto
    // avg) - (sum of array elements
    // smaller than or equal to avg)
    int totalSmallerHalf = (avg *
                           (avg + 1)) / 2;
    Console.WriteLine(totalSmallerHalf -
                        sumSmallerHalf);

    // The first (smaller) element =
    // (sum of natural numbers from
    // avg+1 to n) - (sum of array
    // elements greater than avg)
    Console.WriteLine(((n * (n + 1)) / 2 -
                        totalSmallerHalf) -
                        sumGreaterHalf);
}

// Driver Code
static public void Main ()
{
    int []arr = {1, 3, 5, 6};

    // Range of numbers is 2
    // plus size of array
    int n = 2 + arr.Length;

    findTwoMissingNumbers(arr, n);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find 2 Missing
// Numbers using O(1) extra space

// Returns the sum of the array
function getSum($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];
    return $sum;
}

// Function to find two missing
// numbers in range [1, n]. This
// function assumes that size of
// array is n-2 and all array
// elements are distinct
function findTwoMissingNumbers($arr, $n)
{
    // Sum of 2 Missing Numbers
    $sum = ($n * ($n + 1)) /2 -
            getSum($arr, $n - 2);

    // Find average of two elements
    $avg = ($sum / 2);

    // Find sum of elements smaller
    // than average (avg) and sum of
    // elements greater than average (avg)
    $sumSmallerHalf = 0;
    $sumGreaterHalf = 0;
    for ($i = 0; $i < $n - 2; $i++)
    {
        if ($arr[$i] <= $avg)
            $sumSmallerHalf += $arr[$i];
        else
            $sumGreaterHalf += $arr[$i];
    }

    echo "Two Missing Numbers are\n";

    // The first (smaller) element =
    // (sum of natural numbers upto avg) -
    // (sum of array elements smaller
    // than or equal to avg)
    $totalSmallerHalf = ($avg * ($avg + 1)) / 2;
    echo ($totalSmallerHalf -
          $sumSmallerHalf) , " ";

    // The first (smaller) element =
    // (sum of natural numbers from avg +
    // 1 to n) - (sum of array elements
    // greater than avg)
    echo ((($n * ($n + 1)) / 2 - $totalSmallerHalf) -
                                 $sumGreaterHalf);
}

// Driver Code
$arr= array (1, 3, 5, 6);

// Range of numbers is
// 2 plus size of array
$n = 2 + sizeof($arr);

findTwoMissingNumbers($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find 2 Missing
    // Numbers using O(1) extra space

    // Returns the sum of the array
    function getSum(arr, n)
    {
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Function to find two missing
    // numbers in range [1, n]. This
    // function assumes that size of
    // array is n-2 and all array
    // elements are distinct
    function findTwoMissingNumbers(arr, n)
    {
        // Sum of 2 Missing Numbers
        let sum = (n * (n + 1)) / 2 -
        getSum(arr, n - 2);

        // Find average of two elements
        let avg = (sum / 2);

        // Find sum of elements smaller
        // than average (avg) and sum of
        // elements greater than average (avg)
        let sumSmallerHalf = 0,
        sumGreaterHalf = 0;
        for (let i = 0; i < n - 2; i++)
        {
            if (arr[i] <= avg)
                sumSmallerHalf += arr[i];
            else
                sumGreaterHalf += arr[i];
        }

        document.write(
        "Two Missing " + "Numbers are " + "</br>"
        );

        // The first (smaller) element =
        // (sum of natural numbers upto
        // avg) - (sum of array elements
        // smaller than or equal to avg)
        let totalSmallerHalf = (avg * (avg + 1)) / 2;
        document.write(
        (totalSmallerHalf - sumSmallerHalf) + " "
        );

        // The first (smaller) element =
        // (sum of natural numbers from
        // avg+1 to n) - (sum of array
        // elements greater than avg)
        document.write(
        ((n * (n + 1)) / 2 - totalSmallerHalf) -
        sumGreaterHalf + "</br>"
        );
    }

    let arr = [1, 3, 5, 6];

    // Range of numbers is 2
    // plus size of array
    let n = 2 + arr.length;

    findTwoMissingNumbers(arr, n);

</script>
```

**输出:**

```
Two Missing Numbers are
2 4
```

注意:上述解决方案可能存在溢出问题。
在下面的集合 2 中，讨论了另一种解决方案，即 O(n)时间，O(1)空间，并且不会导致溢出问题。
[找到两个缺失的数字|集合 2(基于异或的解)](https://www.geeksforgeeks.org/find-two-missing-numbers-set-2-xor-based-solution/)
本文由 **Chirag Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。