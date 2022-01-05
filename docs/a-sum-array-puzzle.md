# 一个和数组难题

> 原文:[https://www.geeksforgeeks.org/a-sum-array-puzzle/](https://www.geeksforgeeks.org/a-sum-array-puzzle/)

给定一个由 n 个整数组成的数组 arr[]，构造一个 Sum Array sum[](大小相同)，使得 sum[i]等于 arr[]中除 arr[i]之外的所有元素的和。求解**不用减法运算符，在 O(n)中。**

**示例:**

> **输入:** arr[] = {3，6，4，8，9}
> **输出:** sum[] = {27，24，26，22，21}
> 
> **输入:** arr[] = {4，5，7，3，10，1}
> **输出:** sum[] = {26，25，23，27，20，29}

**算法:**
1)构造一个临时数组 leftSum[]，使得 leftSum[i]包含 arr[i]左边除 arr[i]之外的所有元素的和。
2)构造另一个临时数组 rightSum[]，使得 rightSum[i]包含 arr[i]右边除 arr[i]之外的所有元素的和。
3)求和[]，求左[]，求右[]。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

void sumArray(int arr[], int n)
{
    /* Allocate memory for temporary arrays leftSum[],
    rightSum[] and Sum[]*/
    int leftSum[n], rightSum[n], Sum[n], i, j;

    /* Left most element of left array is always 0 */
    leftSum[0] = 0;

    /* Rightmost most element of right
    array is always 0 */
    rightSum[n - 1] = 0;

    /* Construct the left array*/
    for (i = 1; i < n; i++)
        leftSum[i] = arr[i - 1] + leftSum[i - 1];

    /* Construct the right array*/
    for (j = n - 2; j >= 0; j--)
        rightSum[j] = arr[j + 1] + rightSum[j + 1];

    /* Construct the sum array using
        left[] and right[] */
    for (i = 0; i < n; i++)
        Sum[i] = leftSum[i] + rightSum[i];

    /* print the constructed prod array */
    for (i = 0; i < n; i++)
        cout << Sum[i] << " ";
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 3, 6, 4, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sumArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class Geeks {
    public static void sumArray(int arr[], int n)
    {
        /* Allocate memory for temporary arrays
           leftSum[], rightSum[] and Sum[]*/
        int leftSum[] = new int[n];
        int rightSum[] = new int[n];
        int Sum[] = new int[n];

        int i = 0, j = 0;

        /* Left most element of left array is
           always 0 */
        leftSum[0] = 0;

        /* Right most element of right array
           is always 0 */
        rightSum[n - 1] = 0;

        /* Construct the left array*/
        for (i = 1; i < n; i++)
            leftSum[i] = arr[i - 1] + leftSum[i - 1];

        /* Construct the right array*/
        for (j = n - 2; j >= 0; j--)
            rightSum[j] = arr[j + 1] + rightSum[j + 1];

        /* Construct the sum array using
        left[] and right[] */
        for (i = 0; i < n; i++)
            Sum[i] = leftSum[i] + rightSum[i];

        /*print the sum array*/
        for (i = 0; i < n; i++)
            System.out.print(Sum[i] + " ");
    }

    /* Driver function to test above function*/
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 4, 8, 9 };
        int n = arr.length;
        sumArray(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

def sumArray(arr, n):

    # Allocate memory for temporary arrays
    # leftSum[], rightSum[] and Sum[]
    leftSum = [0 for i in range(n)]
    rightSum = [0 for i in range(n)]
    Sum = [0 for i in range(n)]
    i, j = 0, 0

    # Left most element of left
    # array is always 0
    leftSum[0] = 0

    # Rightmost most element of right
    # array is always 0
    rightSum[n - 1] = 0

    # Construct the left array
    for i in range(1, n):
        leftSum[i] = arr[i - 1] + leftSum[i - 1]

    # Construct the right array
    for j in range(n - 2, -1, -1):
        rightSum[j] = arr[j + 1] + rightSum[j + 1]

    # Construct the sum array using
    # left[] and right[]
    for i in range(0, n):
        Sum[i] = leftSum[i] + rightSum[i]

    # print the constructed prod array
    for i in range(n):
        print(Sum[i], end = " ")

# Driver Code
arr = [3, 6, 4, 8, 9]
n = len(arr)
sumArray(arr, n)

# This code is contributed by
# mohit kumar 29
```

## C#

```
// C# implementation of above approach

using System ;

class Geeks {
    public static void sumArray(int []arr, int n)
    {
        /* Allocate memory for temporary arrays
        leftSum[], rightSum[] and Sum[]*/
        int []leftSum = new int[n];
        int []rightSum = new int[n];
        int []Sum = new int[n];

        int i = 0, j = 0;

        /* Left most element of left array is
        always 0 */
        leftSum[0] = 0;

        /* Right most element of right array
        is always 0 */
        rightSum[n - 1] = 0;

        /* Construct the left array*/
        for (i = 1; i < n; i++)
            leftSum[i] = arr[i - 1] + leftSum[i - 1];

        /* Construct the right array*/
        for (j = n - 2; j >= 0; j--)
            rightSum[j] = arr[j + 1] + rightSum[j + 1];

        /* Construct the sum array using
        left[] and right[] */
        for (i = 0; i < n; i++)
            Sum[i] = leftSum[i] + rightSum[i];

        /*print the sum array*/
        for (i = 0; i < n; i++)
            Console.Write(Sum[i] + " ");
    }

    /* Driver function to test above function*/
    public static void Main()
    {
        int []arr = { 3, 6, 4, 8, 9 };
        int n = arr.Length;
        sumArray(arr, n);
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

function sumArray($arr, $n)
{
    /* Allocate memory for temporary
    arrays leftSum[], rightSum[] and Sum[]*/
    $leftSum = array_fill(0, $n, 0);
    $rightSum = array_fill(0, $n, 0);
    $Sum = array_fill(0, $n, 0);

    /* Left most element of left
       array is always 0 */
    $leftSum[0] = 0;

    /* Rightmost most element of right
    array is always 0 */
    $rightSum[$n - 1] = 0;

    /* Construct the left array*/
    for ($i = 1; $i < $n; $i++)
        $leftSum[$i] = $arr[$i - 1] +
                       $leftSum[$i - 1];

    /* Construct the right array*/
    for ($j = $n - 2; $j >= 0; $j--)
        $rightSum[$j] = $arr[$j + 1] +
                        $rightSum[$j + 1];

    /* Construct the sum array using
        left[] and right[] */
    for ($i = 0; $i < $n; $i++)
        $Sum[$i] = $leftSum[$i] + $rightSum[$i];

    /* print the constructed prod array */
    for ($i = 0; $i < $n; $i++)
        echo $Sum[$i]." ";
}

// Driver Code
$arr = array( 3, 6, 4, 8, 9 );
$n = count($arr);
sumArray($arr, $n);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of above approach

    function sumArray(arr, n)
    {
        /* Allocate memory for temporary arrays
           leftSum[], rightSum[] and Sum[]*/
        let leftSum = new Array(n);
        let rightSum = new Array(n);
        let Sum = new Array(n);

        let i = 0, j = 0;

        /* Left most element of left array is
           always 0 */
        leftSum[0] = 0;

        /* Right most element of right array
           is always 0 */
        rightSum[n - 1] = 0;

        /* Construct the left array*/
        for (i = 1; i < n; i++)
            leftSum[i] = arr[i - 1] + leftSum[i - 1];

        /* Construct the right array*/
        for (j = n - 2; j >= 0; j--)
            rightSum[j] = arr[j + 1] + rightSum[j + 1];

        /* Construct the sum array using
        left[] and right[] */
        for (i = 0; i < n; i++)
            Sum[i] = leftSum[i] + rightSum[i];

        /*print the sum array*/
        for (i = 0; i < n; i++)
            document.write(Sum[i] + " ");
    }

    let arr = [ 3, 6, 4, 8, 9 ];
    let n = arr.length;
    sumArray(arr, n);

</script>
```

**Output:** 

```
27 24 26 22 21
```

**时间复杂度:**O(n)
T3】空间复杂度:O(n)
T6】辅助空间: O(n)

**上述方法可以优化到在 O(1)辅助空间工作。**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

void sumArray(int arr[], int n)
{
    int i, temp = 0;

    /* Allocate memory for the sum array */
    int Sum[n];

    /* Initialize the sum array as 0 */
    memset(Sum, 0, n);

    /* In this loop, temp variable contains
    sum of elements on left side excluding
    arr[i] */
    for (i = 0; i < n; i++) {
        Sum[i] = temp;
        temp += arr[i];
    }

    /* Initialize temp to 0 for sum on right
    side */
    temp = 0;

    /* In this loop, temp variable contains
    sum of elements on right side excluding
        arr[i] */
    for (i = n - 1; i >= 0; i--) {
        Sum[i] += temp;
        temp += arr[i];
    }

    for (i = 0; i < n; i++)
        cout << Sum[i] << " ";
}

/* Driver program to test above function */
int main()
{
    int arr[] = { 3, 6, 4, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sumArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class Geeks {
    public static void sumArray(int arr[], int n)
    {
        int i = 0, temp = 0;
        int Sum[] = new int[n];

        Arrays.fill(Sum, 0);

        /* In this loop, temp variable contains
           sum of elements on left side excluding
           arr[i] */
        for (i = 0; i < n; i++) {
            Sum[i] = temp;
            temp += arr[i];
        }

        /* Initialize temp to 0 for sum on right side */
        temp = 0;

        /* In this loop, temp variable contains
           sum of elements on right side excluding
           arr[i] */
        for (i = n - 1; i >= 0; i--) {
            Sum[i] += temp;
            temp += arr[i];
        }

        for (i = 0; i < n; i++)
            System.out.print(Sum[i] + " ");
    }

    /* Driver function to test above function*/
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 4, 8, 9 };
        int n = arr.length;
        sumArray(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach
def sumArray(arr, n):

    i, temp = 0, 0

    # Allocate memory for the sum array */
    Sum = [0 for i in range(n)]

    '''In this loop, temp variable contains
    sum of elements on left side excluding
    arr[i] '''
    for i in range(n):
        Sum[i] = temp
        temp += arr[i]

    # Initialize temp to 0 for sum
    # on right side */
    temp = 0

    ''' In this loop, temp variable contains
        sum of elements on right side excluding
        arr[i] */'''
    for i in range(n - 1, -1, -1):
        Sum[i] += temp
        temp += arr[i]

    for i in range(n):
        print(Sum[i], end = " ")

# Driver Code
arr = [ 3, 6, 4, 8, 9 ]
n = len(arr)
sumArray(arr, n)

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation of above approach
using System;
class Geeks {
    public static void sumArray(int []arr, int n)
    {
        int i = 0, temp = 0;
        int []Sum = new int[n];
        for( i=0;i<n;i++)
        Sum[i] = 0;

        /* In this loop, temp variable contains
        sum of elements on left side excluding
        arr[i] */
        for (i = 0; i < n; i++) {
            Sum[i] = temp;
            temp += arr[i];
        }

        /* Initialize temp to 0 for sum on right side */
        temp = 0;

        /* In this loop, temp variable contains
        sum of elements on right side excluding
        arr[i] */
        for (i = n - 1; i >= 0; i--) {
            Sum[i] += temp;
            temp += arr[i];
        }

        for (i = 0; i < n; i++)
            Console.Write(Sum[i] + " ");
    }

    /* Driver function to test above function*/
    public static void Main()
    {
        int []arr = { 3, 6, 4, 8, 9 };
        int n = arr.Length;
        sumArray(arr, n);
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
function sumArray($arr, $n)
{
    $temp = 0;

    /* Allocate memory for the sum array */
    /* Initialize the sum array as 0 */
    $Sum = array_fill(0, $n, 0);

    /* In this loop, temp variable contains
    sum of elements on left side excluding
    arr[i] */
    for ($i = 0; $i < $n; $i++)
    {
        $Sum[$i] = $temp;
        $temp += $arr[$i];
    }

    /* Initialize temp to 0 for sum
    on right side */
    $temp = 0;

    /* In this loop, temp variable contains
    sum of elements on right side excluding
    arr[i] */
    for ($i = $n - 1; $i >= 0; $i--)
    {
        $Sum[$i] += $temp;
        $temp += $arr[$i];
    }

    for ($i = 0; $i < $n; $i++)
        echo $Sum[$i] . " ";
}

// Driver Code
$arr = array( 3, 6, 4, 8, 9 );
$n = count($arr);
sumArray($arr, $n);

// This code is contributed by
// chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    function sumArray(arr, n)
    {
        let i = 0, temp = 0;
        let Sum = new Array(n);
        for( i=0;i<n;i++)
            Sum[i] = 0;

        /* In this loop, temp variable contains
        sum of elements on left side excluding
        arr[i] */
        for (i = 0; i < n; i++) {
            Sum[i] = temp;
            temp += arr[i];
        }

        /* Initialize temp to 0 for sum on right side */
        temp = 0;

        /* In this loop, temp variable contains
        sum of elements on right side excluding
        arr[i] */
        for (i = n - 1; i >= 0; i--) {
            Sum[i] += temp;
            temp += arr[i];
        }

        for (i = 0; i < n; i++)
            document.write(Sum[i] + " ");
    }

    let arr = [ 3, 6, 4, 8, 9 ];
    let n = arr.length;
    sumArray(arr, n);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
27 24 26 22 21
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)