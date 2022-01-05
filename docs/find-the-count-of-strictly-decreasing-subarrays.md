# 求严格递减子阵的计数

> 原文:[https://www . geeksforgeeks . org/find-严格递减子数组的计数/](https://www.geeksforgeeks.org/find-the-count-of-strictly-decreasing-subarrays/)

给定整数数组 A[]。任务是计算严格递减子阵列的总数(大小> 1)。
**例** :

> **输入** : A[] = { 100，3，1，15 }
> **输出** : 3
> 子阵为- > { 100，3 }，{ 100，3，1 }，{ 3，1 }
> **输入** : A[] = { 4，2，2，1 }
> **输出** : 2

**天真方法:**一个简单的解决方案是运行两个[进行循环](https://www.geeksforgeeks.org/loops-in-c/)，并检查子阵列是否在减少。
如果知道子阵列 arr[i:j]不是严格递减的，那么子阵列 arr[i:j+1]，arr[i:j+2]就可以改进这一点，..arr[i:n-1]不能严格递减。
**高效途径:**在上面的解决方案中，我们对许多子阵列进行了两次计数。这也是可以改进的，这个想法是基于长度为“len”的排序(递减)子阵列将 len*(len-1)/2 添加到结果中的事实。
以下是上述方法的实施:

## C++

```
// C++ program to count number of strictly
// decreasing subarrays in O(n) time.

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of strictly
// decreasing subarrays
int countDecreasing(int A[], int n)
{
    int cnt = 0; // Initialize result

    // Initialize length of current
    // decreasing subarray
    int len = 1;

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i) {
        // If arr[i+1] is less than arr[i],
        // then increment length
        if (A[i + 1] < A[i])
            len++;

        // Else Update count and reset length
        else {
            cnt += (((len - 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += (((len - 1) * len) / 2);

    return cnt;
}

// Driver program
int main()
{
    int A[] = { 100, 3, 1, 13 };
    int n = sizeof(A) / sizeof(A[0]);

    cout << countDecreasing(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of strictly
// decreasing subarrays in O(n) time.

import java.io.*;

class GFG {

// Function to count the number of strictly
// decreasing subarrays
static int countDecreasing(int A[], int n)
{
    int cnt = 0; // Initialize result

    // Initialize length of current
    // decreasing subarray
    int len = 1;

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i) {
        // If arr[i+1] is less than arr[i],
        // then increment length
        if (A[i + 1] < A[i])
            len++;

        // Else Update count and reset length
        else {
            cnt += (((len - 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += (((len - 1) * len) / 2);

    return cnt;
}

// Driver program
    public static void main (String[] args) {
    int A[] = { 100, 3, 1, 13 };
    int n = A.length;

    System.out.println(countDecreasing(A, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to count number
# of strictly decreasing subarrays
# in O(n) time.

# Function to count the number of
# strictly decreasing subarrays
def countDecreasing(A, n):

    cnt = 0 # Initialize result

    # Initialize length of current
    # decreasing subarray
    len = 1

    # Traverse through the array
    for i in range (n - 1) :

        # If arr[i+1] is less than arr[i],
        # then increment length
        if (A[i + 1] < A[i]):
            len += 1

        # Else Update count and
        # reset length
        else :
            cnt += (((len - 1) * len) // 2);
            len = 1

    # If last length is more than 1
    if (len > 1):
        cnt += (((len - 1) * len) // 2)

    return cnt

# Driver Code
if __name__=="__main__":

    A = [ 100, 3, 1, 13 ]
    n = len(A)

    print (countDecreasing(A, n))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to count number of strictly
// decreasing subarrays in O(n) time.

using System;

class GFG
{
// Function to count the number of strictly
// decreasing subarrays
static int countDecreasing(int []A, int n)
{
int cnt = 0; // Initialize result

// Initialize length of current
// decreasing subarray
int len = 1;

// Traverse through the array
for (int i = 0; i < n - 1; ++i) {
// If arr[i+1] is less than arr[i],
// then increment length
if (A[i + 1] < A[i])
len++;

// Else Update count and reset length
else {
cnt += (((len - 1) * len) / 2);
len = 1;
}
}

// If last length is more than 1
if (len > 1)
cnt += (((len - 1) * len) / 2);

return cnt;
}

// Driver code
static void Main()
{
int []A = { 100, 3, 1, 13 };
int n = A.Length ;
Console.WriteLine(countDecreasing(A, n));
}
// This code is contributed by ANKITRAI1
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of strictly
// decreasing subarrays in O(n) time.

// Function to count the number of
// strictly decreasing subarrays
function countDecreasing($A, $n)
{
    $cnt = 0; // Initialize result

    // Initialize length of current
    // decreasing subarray
    $len = 1;

    // Traverse through the array
    for ($i = 0; $i < $n - 1; ++$i)
    {
        // If arr[i+1] is less than arr[i],
        // then increment length
        if ($A[$i + 1] < $A[$i])
            $len++;

        // Else Update count and
        // reset length
        else
        {
            $cnt += ((($len - 1) * $len) / 2);
            $len = 1;
        }
    }

    // If last length is more than 1
    if ($len > 1)
        $cnt += ((($len - 1) * $len) / 2);

    return $cnt;
}

// Driver Code
$A = array( 100, 3, 1, 13 );
$n = sizeof($A);

echo countDecreasing($A, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to count number of strictly
// decreasing subarrays in O(n) time.

// Function to count the number of strictly
// decreasing subarrays
function countDecreasing(A, n)
{
    var cnt = 0; // Initialize result

    // Initialize length of current
    // decreasing subarray
    var len = 1;

    // Traverse through the array
    for (var i = 0; i < n - 1; ++i) {
        // If arr[i+1] is less than arr[i],
        // then increment length
        if (A[i + 1] < A[i])
            len++;

        // Else Update count and reset length
        else {
            cnt += parseInt(((len - 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += parseInt(((len - 1) * len) / 2);

    return cnt;
}

    var A = [ 100, 3, 1, 13 ];
    var n = A.length;
    document.write( countDecreasing(A, n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)