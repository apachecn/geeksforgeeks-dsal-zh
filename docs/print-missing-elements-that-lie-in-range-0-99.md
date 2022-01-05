# 打印 0–99 范围内的缺失元素

> 原文:[https://www . geesforgeks . org/print-missing-elements-in-range-0-99/](https://www.geeksforgeeks.org/print-missing-elements-that-lie-in-range-0-99/)

给定一个整数数组，打印 0-99 范围内缺失的元素。如果有一个以上的缺失，整理它们，否则只打印数字。
注意，输入数组可能没有排序，可能包含范围[0-99]之外的数字，但打印缺失元素时只考虑这个范围。

**示例:**

```
Input: {88, 105, 3, 2, 200, 0, 10}
Output: 1
        4-9
        11-87
        89-99

Input: {9, 6, 900, 850, 5, 90, 100, 99}
Output: 0-4
        7-8
        10-89
        91-98
```

预期时间复杂度 O(n)，其中 n 是输入数组的大小。

想法是使用大小为 100 的布尔数组来跟踪 0 到 99 范围内的数组元素。我们首先遍历输入数组，并在布尔数组中标记这些当前元素。一旦标记了所有存在的元素，布尔数组就被用来打印丢失的元素。

以下是上述想法的实现。

## C++

```
// C++ program for print missing elements
#include <bits/stdc++.h>
#define LIMIT 100
using namespace std;

// A O(n) function to print missing elements in an array
void printMissing(int arr[], int n)
{
    // Initialize all number from 0 to 99 as NOT seen
    bool seen[LIMIT] = {false};

    // Mark present elements in range [0-99] as seen
    for (int i=0; i<n; i++)
    if (arr[i] < LIMIT)
    seen[arr[i]] = true;

    // Print missing element
    int i = 0;
    while (i < LIMIT)
    {
        // If i is missing
        if (seen[i] == false)
        {
            // Find if there are more missing elements after i
            int j = i+1;
            while (j < LIMIT && seen[j] == false)
                j++;

            // Print missing single or range
            (i+1 == j)? cout  <<  i : cout << "\n" << i << "-" << j-1;

            // Update u
            i = j;
        }
        else
            i++;
    }
}

// Driver program
int main()
{
    int arr[] = {88, 105, 3, 2, 200, 0, 10};
    int n = sizeof(arr)/sizeof(arr[0]);
    printMissing(arr, n);
    return 0;
}
// This code is contributed by shivanisinghss2110
```

## C

```
// C program for print missing elements
#include<stdio.h>
#define LIMIT 100

// A O(n) function to print missing elements in an array
void printMissing(int arr[], int n)
{
    // Initialize all number from 0 to 99 as NOT seen
    bool seen[LIMIT] = {false};

    // Mark present elements in range [0-99] as seen
    for (int i=0; i<n; i++)
      if (arr[i] < LIMIT)
       seen[arr[i]] = true;

    // Print missing element
    int i = 0;
    while (i < LIMIT)
    {
        // If i is missing
        if (seen[i] == false)
        {
            // Find if there are more missing elements after i
            int j = i+1;
            while (j < LIMIT && seen[j] == false)
                  j++;

            // Print missing single or range
            (i+1 == j)? printf("%dn", i): printf("%d-%dn", i, j-1);

            // Update u
            i = j;
        }
        else
            i++;
    }
}

// Driver program
int main()
{
    int arr[] = {88, 105, 3, 2, 200, 0, 10};
    int n = sizeof(arr)/sizeof(arr[0]);
    printMissing(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class PrintMissingElement
{
    // A O(n) function to print missing elements in an array
    void printMissing(int arr[], int n)
    {
        int LIMIT = 100;

        boolean seen[] = new boolean[LIMIT];

        // Initialize all number from 0 to 99 as NOT seen
        for (int i = 0; i < LIMIT; i++)
            seen[i] = false;

        // Mark present elements in range [0-99] as seen
        for (int i = 0; i < n; i++)
        {
            if (arr[i] < LIMIT)
                seen[arr[i]] = true;
        }

        // Print missing element
        int i = 0;
        while (i < LIMIT)
        {
            // If i is missing
            if (seen[i] == false)
            {
                // Find if there are more missing elements after i
                int j = i + 1;
                while (j < LIMIT && seen[j] == false)
                    j++;

                // Print missing single or range
                int p = j-1;
                System.out.println(i+1==j ? i : i + "-" + p);

                // Update u
                i = j;
            }
            else
                i++;
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        PrintMissingElement missing = new PrintMissingElement();
        int arr[] = {88, 105, 3, 2, 200, 0, 10};
        int n = arr.length;
        missing.printMissing(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for print missing elements

# A O(n) function to print missing elements in an array
def printMissing(arr, n) : 
    LIMIT = 100
    seen = [False]*LIMIT

    # Initialize all number from 0 to 99 as NOT seen
    for i in range(LIMIT) :
      seen[i] = False

    # Mark present elements in range [0-99] as seen
    for i in range(n) :
      if (arr[i] < LIMIT) :
        seen[arr[i]] = True

    # Print missing element
    i = 0
    while (i < LIMIT) :

      # If i is missing
      if (seen[i] == False) :

        # Find if there are more missing elements after i
        j = i + 1
        while (j < LIMIT and seen[j] == False) :
          j += 1

        # Print missing single or range
        p = j - 1
        if(i + 1 == j) :   
          print(i)

        else :
          print(i, "-", p)

        # Update u
        i = j

      else :
        i += 1

  # Driver code
arr = [88, 105, 3, 2, 200, 0, 10]
n = len(arr)
printMissing(arr, n)

# This code is contributed by divyesh072019.
```

## C#

```
using System;
class GFG
{

  // A O(n) function to print missing elements in an array
  static void printMissing(int[] arr, int n) 
  {
    int LIMIT = 100;
    bool[] seen = new bool[LIMIT];
    int i;

    // Initialize all number from 0 to 99 as NOT seen
    for (i = 0; i < LIMIT; i++) 
      seen[i] = false;

    // Mark present elements in range [0-99] as seen
    for (i = 0; i < n; i++) 
    {
      if (arr[i] < LIMIT)
        seen[arr[i]] = true;
    }

    // Print missing element
    i = 0;
    while (i < LIMIT) 
    {
      // If i is missing
      if (seen[i] == false) 
      {
        // Find if there are more missing elements after i
        int j = i + 1;
        while (j < LIMIT && seen[j] == false)
          j++;

        // Print missing single or range
        int p = j - 1;
        if(i + 1 == j)
        {
          Console.WriteLine(i);
        }
        else
        {
          Console.WriteLine(i + "-" + p);
        }

        // Update u
        i = j;
      } 
      else
        i++;
    }
  }

  // Driver code
  static void Main()
  {
    int[] arr = {88, 105, 3, 2, 200, 0, 10};
    int n = arr.Length;
    printMissing(arr, n);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for print
// missing elements
$LIMIT= 100;

// A O(n) function to print
// missing elements in an array
function printMissing($arr, $n)
{
    global $LIMIT;

    // Initialize all number from
    // 0 to 99 as NOT seen
    $seen = (false);

    // Mark present elements in.
    // range [0-99] as seen
    for ($i = 0; $i < $n; $i++)
    if ($arr[$i] < $LIMIT)
    $seen[$arr[$i]] = true;

    // Print missing element
    $i = 0;
    while ($i < $LIMIT)
    {
        // If i is missing
        if ($seen[$i] == false)
        {
            // Find if there are more
            // missing elements after i
            $j = $i + 1;
            while ($j < $LIMIT &&
                   $seen[$j] == false)
                $j++;

            // Print missing
            // single or range
            if (($i + 1 == $j) == true)

            echo $i, "\n";
            else
            echo $i , "-", $j - 1, "\n";

            // Update u
            $i = $j;
        }
        else
            $i++;
    }
}

// Driver Code
$arr = array (88, 105, 3, 2,
              200, 0, 10);
$n = sizeof($arr);
printMissing($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program for print missing elements

// A O(n) function to print missing
// elements in an array
function printMissing(arr, n)
{
    let LIMIT = 100;
    let seen = new Array(LIMIT);
    let i;

    // Initialize all number from
    // 0 to 99 as NOT seen
    for(i = 0; i < LIMIT; i++)
        seen[i] = false;

    // Mark present elements in
    // range [0-99] as seen
    for(i = 0; i < n; i++)
    {
        if (arr[i] < LIMIT)
            seen[arr[i]] = true;
    }

    // Print missing element
    i = 0;
    while (i < LIMIT)
    {
        // If i is missing
        if (seen[i] == false)
        {

            // Find if there are more missing
            // elements after i
            let j = i + 1;
            while (j < LIMIT && seen[j] == false)
                j++;

            // Print missing single or range
            let p = j - 1;

            if (i + 1 == j)
            {
                document.write(i + "</br>");
            }
            else
            {
                document.write(i + "-" + p + "</br>");
            }

            // Update u
            i = j;
        }
        else
            i++;
    }
}

// Driver code
let arr = [88, 105, 3, 2, 200, 0, 10];
let n = arr.length;

printMissing(arr, n);

// This code is contributed by suresh07

</script>
```

**输出:**

```
1
4-9
11-87
89-99
```

上述程序的时间复杂度为 O(n)。

本文由[Vignesh Narayanan](https://sites.google.com/a/asu.edu/vignesh-narayanan/)[Sowmya Sampath](https://sites.google.com/a/usc.edu/sowmya/)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。