# 检查阵列是否美观

> 原文:[https://www.geeksforgeeks.org/check-array-beautiful/](https://www.geeksforgeeks.org/check-array-beautiful/)

给定一个整数 n 和一个大小为 n 的数组，检查它是否满足以下条件:-

1.  数组的所有元素必须在 1 到 n 之间。
2.  数组必须**而不是**按升序排序。
3.  数组由独特的元素组成。

如果所有条件都满足，打印是否则不打印
**示例:**

```
Input:  4
        1 2 3 4
Output: No
Array is sorted in ascending order

Input:  4
        4 3 2 1
Output: Yes 
Satisfies all given condition

Input:  4
        1 1 2 3
Output: No 
Array has repeated entries
```

一个**简单的解决方法**就是统计所有元素的频率。计数频率时，检查所有元素是否从 1 到 n。最后检查每个元素的频率是否为 1，数组是否按升序排序。
一个**高效的解决方案**是避免额外的空间。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check array is
// beautiful or not
#include <iostream>
using namespace std;

// Function to implement the given task
bool isBeautiful(int a[], int n) {

  int sum = a[0];
  bool isAscSorted = true;
  for (int i = 1; i < n; i++) {

    // Checking for any repeated entry
    if (a[i] == a[i - 1])
      return 0;

    // Checking for ascending sorting
    if (a[i] < a[i - 1])
      isAscSorted = false;
    sum += a[i];
  }

  // Does not satisfy second condition
  if (isAscSorted == true)
    return false;

  // Sum of 1 to n elements is
  // (n*(n + 1)/2))
  return (sum == (n * (n + 1) / 2));
}

// Driver Code
int main() {
  int a[] = {1, 2, 4, 3};
  int n = sizeof(a) / sizeof(a[0]);
  if (isBeautiful(a, n))
    cout << "Yes";
  else
    cout << "No";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to check array is
// beautiful or not

import java.io.*;

class GFG {

// Function to implement the given task
 static boolean isBeautiful(int a[], int n) {

int sum = a[0];
boolean  isAscSorted = true;
for (int i = 1; i < n; i++) {

    // Checking for any repeated entry
    if (a[i] == a[i - 1])
    return false;

    // Checking for ascending sorting
    if (a[i] < a[i - 1])
    isAscSorted = false;
    sum += a[i];
}

// Does not satisfy second condition
if (isAscSorted == true)
    return false;

// Sum of 1 to n elements is
// (n*(n + 1)/2))
return (sum == (n * (n + 1) / 2));
}

// Driver Code
public static void main (String[] args) {

int a[] = {1, 2, 4, 3};
int n = a.length;

if (isBeautiful(a, n))
    System.out.println ( "Yes");
else
    System.out.println("No");

}
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to check array is
# beautiful or not

# Function to implement the given task
def isBeautiful(a,n):

    sum = a[0]
    isAscSorted = True
    for i in range(1,n):

        # Checking for any repeated entry
        if (a[i] == a[i - 1]):
            return False

        # Checking for ascending sorting
        if (a[i] < a[i - 1]):
            isAscSorted = False
        sum=sum+ a[i]

    # Does not satisfy second condition
    if (isAscSorted == True):
        return False

    #Sum of 1 to n elements is
    # (n*(n + 1)/2))
    return (sum == (n * (n + 1) // 2))

# Driver code

a= [1, 2, 4, 3]
n = len(a)

if (isBeautiful(a, n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to check array is
// beautiful or not
using System;

class GFG {

    // Function to implement the given task
    static bool isBeautiful(int []a, int n) {

        int sum = a[0];
        bool isAscSorted = true;
        for (int i = 1; i < n; i++) {

            // Checking for any repeated entry
            if (a[i] == a[i - 1])
            return false;

            // Checking for ascending sorting
            if (a[i] < a[i - 1])
            isAscSorted = false;
            sum += a[i];
        }

        // Does not satisfy second condition
        if (isAscSorted == true)
            return false;

        // Sum of 1 to n elements is
        // (n*(n + 1)/2))
        return (sum == (n * (n + 1) / 2));
    }

    // Driver Code
    public static void Main ()
    {

        int []a = {1, 2, 4, 3};
        int n = a.Length;

        if (isBeautiful(a, n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine("No");

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check array is
// beautiful or not

// Function to implement
// the given task
function isBeautiful($a, $n)
{
    $sum = $a[0];
    $sAscSorted = true;
    for ($i = 1; $i < $n; $i++)
    {

        // Checking for any repeated entry
        if ($a[$i] == $a[$i - 1])
            return 0;

        // Checking for ascending sorting
        if ($a[$i] < $a[$i - 1])
            $isAscSorted = false;
        $sum += $a[$i];
    }

        // Does not satisfy second condition
        if ($isAscSorted == true)
            return false;

        // Sum of 1 to n elements is
        // (n*(n + 1)/2))
        return ($sum == ($n * ($n + 1) / 2));
}

// Driver Code
$a = array(1, 2, 4, 3);
$n = count($a);
if (isBeautiful($a, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to check array is
// beautiful or not

// Function to implement the given task
function isBeautiful(a, n) {

  var sum = a[0];
  var isAscSorted = true;
  for (var i = 1; i < n; i++) {

    // Checking for any repeated entry
    if (a[i] == a[i - 1])
      return 0;

    // Checking for ascending sorting
    if (a[i] < a[i - 1])
      isAscSorted = false;
    sum += a[i];
  }

  // Does not satisfy second condition
  if (isAscSorted == true)
    return false;

  // Sum of 1 to n elements is
  // (n*(n + 1)/2))
  return (sum == (n * (n + 1) / 2));
}

// Driver Code
var a = [1, 2, 4, 3];
var n = a.length;
if (isBeautiful(a, n))
  document.write( "Yes");
else
  document.write( "No");

</script>
```

**Output:** 

```
Yes
```