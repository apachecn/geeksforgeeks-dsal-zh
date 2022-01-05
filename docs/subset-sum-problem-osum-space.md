# O(和)空间中的子集和问题

> 原文:[https://www . geesforgeks . org/subset-sum-problem-osum-space/](https://www.geeksforgeeks.org/subset-sum-problem-osum-space/)

给定一个非负整数数组和值，确定给定集合中是否有和等于给定和的子集。

**示例:**

```
Input : arr[] = {4, 1, 10, 12, 5, 2}, 
          sum = 9
Output : TRUE
{4, 5} is a subset with sum 9.

Input : arr[] = {1, 8, 2, 5}, 
          sum = 4
Output : FALSE 
There exists no subset with sum 4.
```

我们已经在下面的帖子中讨论了基于[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的解决方案。
[动态规划|集合 25(子集和问题)](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)
上面讨论的解决方案需要 O(n *和)空间和 O(n *和)时间。我们可以优化空间。我们创建一个布尔 2D 数组子集[2][sum+1]。用自下而上的方式，我们可以填满这张桌子。在“子集[2][总和+1]”中使用 **2 的想法是，为了填充一行，只需要前一行的值。因此，交替行被用于使第一行成为当前行，第二行成为前一行，或者第一行成为前一行，第二行成为当前行。**

## C++

```
// Returns true if there exists a subset
// with given sum in arr[]
#include <iostream>
using namespace std;

bool isSubsetSum(int arr[], int n, int sum)
{

    // The value of subset[i%2][j] will be true
    // if there exists a subset of sum j in
    // arr[0, 1, ...., i-1]
    bool subset[2][sum + 1];

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= sum; j++) {

            // A subset with sum 0 is always possible
            if (j == 0)
                subset[i % 2][j] = true;

            // If there exists no element no sum
            // is possible
            else if (i == 0)
                subset[i % 2][j] = false;
            else if (arr[i - 1] <= j)
                subset[i % 2][j] = subset[(i + 1) % 2]
             [j - arr[i - 1]] || subset[(i + 1) % 2][j];
            else
                subset[i % 2][j] = subset[(i + 1) % 2][j];
        }
    }

    return subset[n % 2][sum];
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 5 };
    int sum = 7;
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isSubsetSum(arr, n, sum) == true)
        cout <<"There exists a subset with given sum";
    else
        cout <<"No subset exists with given sum";
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// Returns true if there exists a subset
// with given sum in arr[]
#include <stdio.h>
#include <stdbool.h>

bool isSubsetSum(int arr[], int n, int sum)
{
    // The value of subset[i%2][j] will be true
    // if there exists a subset of sum j in
    // arr[0, 1, ...., i-1]
    bool subset[2][sum + 1];

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= sum; j++) {

            // A subset with sum 0 is always possible
            if (j == 0)
                subset[i % 2][j] = true;

            // If there exists no element no sum
            // is possible
            else if (i == 0)
                subset[i % 2][j] = false;
            else if (arr[i - 1] <= j)
                subset[i % 2][j] = subset[(i + 1) % 2]
             [j - arr[i - 1]] || subset[(i + 1) % 2][j];
            else
                subset[i % 2][j] = subset[(i + 1) % 2][j];
        }
    }

    return subset[n % 2][sum];
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 5 };
    int sum = 7;
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isSubsetSum(arr, n, sum) == true)
        printf("There exists a subset with given sum");
    else
        printf("No subset exists with given sum");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to get a subset with a
// with a sum provided by the user
public class Subset_sum {

    // Returns true if there exists a subset
    // with given sum in arr[]
    static boolean isSubsetSum(int arr[], int n, int sum)
    {
        // The value of subset[i%2][j] will be true
        // if there exists a subset of sum j in
        // arr[0, 1, ...., i-1]
        boolean subset[][] = new boolean[2][sum + 1];

        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= sum; j++) {

                // A subset with sum 0 is always possible
                if (j == 0)
                    subset[i % 2][j] = true;

                // If there exists no element no sum
                // is possible
                else if (i == 0)
                    subset[i % 2][j] = false;
                else if (arr[i - 1] <= j)
                    subset[i % 2][j] = subset[(i + 1) % 2]
                 [j - arr[i - 1]] || subset[(i + 1) % 2][j];
                else
                    subset[i % 2][j] = subset[(i + 1) % 2][j];
            }
        }

        return subset[n % 2][sum];
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 5 };
        int sum = 7;
        int n = arr.length;
        if (isSubsetSum(arr, n, sum) == true)
            System.out.println("There exists a subset with" +
                                              "given sum");
        else
            System.out.println("No subset exists with" +
                                           "given sum");
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Returns true if there exists a subset
# with given sum in arr[]

def isSubsetSum(arr, n, sum):

    # The value of subset[i%2][j] will be true
    # if there exists a subset of sum j in
    # arr[0, 1, ...., i-1]
    subset = [ [False for j in range(sum + 1)] for i in range(3) ]

    for i in range(n + 1):
        for j in range(sum + 1):
            # A subset with sum 0 is always possible
            if (j == 0):
                subset[i % 2][j] = True

            # If there exists no element no sum
            # is possible
            elif (i == 0):
                subset[i % 2][j] = False
            elif (arr[i - 1] <= j):
                subset[i % 2][j] = subset[(i + 1) % 2][j - arr[i - 1]] or subset[(i + 1)
                                                                               % 2][j]
            else:
                subset[i % 2][j] = subset[(i + 1) % 2][j]

    return subset[n % 2][sum]

# Driver code
arr = [ 6, 2, 5 ]
sum = 7
n = len(arr)
if (isSubsetSum(arr, n, sum) == True):
    print ("There exists a subset with given sum")
else:
    print ("No subset exists with given sum")

# This code is contributed by Sachin Bisht
```

## C#

```
// C# Program to get a subset with a
// with a sum provided by the user

using System;

public class Subset_sum {

    // Returns true if there exists a subset
    // with given sum in arr[]
    static bool isSubsetSum(int []arr, int n, int sum)
    {
        // The value of subset[i%2][j] will be true
        // if there exists a subset of sum j in
        // arr[0, 1, ...., i-1]
        bool [,]subset = new bool[2,sum + 1];

        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= sum; j++) {

                // A subset with sum 0 is always possible
                if (j == 0)
                    subset[i % 2,j] = true;

                // If there exists no element no sum
                // is possible
                else if (i == 0)
                    subset[i % 2,j] = false;
                else if (arr[i - 1] <= j)
                    subset[i % 2,j] = subset[(i + 1) % 2,j - arr[i - 1]] || subset[(i + 1) % 2,j];
                else
                    subset[i % 2,j] = subset[(i + 1) % 2,j];
            }
        }

        return subset[n % 2,sum];
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 5 };
        int sum = 7;
        int n = arr.Length;
        if (isSubsetSum(arr, n, sum) == true)
            Console.WriteLine("There exists a subset with" +
                                         "given sum");
        else
            Console.WriteLine("No subset exists with" +
                                        "given sum");
    }
}
// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Returns true if there exists a subset
// with given sum in arr[]

function isSubsetSum($arr, $n, $sum)
{
    // The value of subset[i%2][j] will be
    // true if there exists a subset of
    // sum j in arr[0, 1, ...., i-1]
    $subset[2][$sum + 1] = array();

    for ($i = 0; $i <= $n; $i++)
    {
        for ($j = 0; $j <= $sum; $j++)
        {

            // A subset with sum 0 is
            // always possible
            if ($j == 0)
                $subset[$i % 2][$j] = true;

            // If there exists no element no
            // sum is possible
            else if ($i == 0)
                $subset[$i % 2][$j] = false;
            else if ($arr[$i - 1] <= $j)
                $subset[$i % 2][$j] = $subset[($i + 1) % 2]
                                             [$j - $arr[$i - 1]] ||
                                      $subset[($i + 1) % 2][$j];
            else
                $subset[$i % 2][$j] = $subset[($i + 1) % 2][$j];
        }
    }

    return $subset[$n % 2][$sum];
}

// Driver code
$arr = array( 6, 2, 5 );
$sum = 7;
$n = sizeof($arr);
if (isSubsetSum($arr, $n, $sum) == true)
    echo ("There exists a subset with given sum");
else
    echo ("No subset exists with given sum");

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript Program to get a subset with a
// with a sum provided by the user

    // Returns true if there exists a subset
    // with given sum in arr[]
    function isSubsetSum(arr, n, sum)
    {
        // The value of subset[i%2][j] will be true
        // if there exists a subset of sum j in
        // arr[0, 1, ...., i-1]
        let subset = new Array(2);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < subset.length; i++) {
            subset[i] = new Array(2);
        }

        for (let i = 0; i <= n; i++) {
            for (let j = 0; j <= sum; j++) {

                // A subset with sum 0 is always possible
                if (j == 0)
                    subset[i % 2][j] = true;

                // If there exists no element no sum
                // is possible
                else if (i == 0)
                    subset[i % 2][j] = false;
                else if (arr[i - 1] <= j)
                    subset[i % 2][j] = subset[(i + 1) % 2]
                 [j - arr[i - 1]] || subset[(i + 1) % 2][j];
                else
                    subset[i % 2][j] = subset[(i + 1) % 2][j];
            }
        }

        return subset[n % 2][sum];
    }

// driver program
        let arr = [ 1, 2, 5 ];
        let sum = 7;
        let n = arr.length;
        if (isSubsetSum(arr, n, sum) == true)
            document.write("There exists a subset with" +
                                              "given sum");
        else
            document.write("No subset exists with" +
                                           "given sum");

// This code is contributed by code_hunt.
</script>
```

**Output**

```
There exists a subset with given sum
```