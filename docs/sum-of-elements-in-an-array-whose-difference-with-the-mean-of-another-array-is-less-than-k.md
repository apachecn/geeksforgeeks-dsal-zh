# 一个数组中与另一个数组的平均值之差小于 k 的元素之和

> 原文:[https://www . geesforgeks . org/数组中元素之和与另一个数组的平均值之差小于-k/](https://www.geeksforgeeks.org/sum-of-elements-in-an-array-whose-difference-with-the-mean-of-another-array-is-less-than-k/)

给定两个未排序的数组 **arr1[]** 和 **arr2[]** 。求**arr 1【】**的元素之和，其与**arr 2【】**的平均值之差为 **< k** 。
**举例:**

> **输入:** arr1[] = {1，2，3，4，7，9}，arr2[] = {0，1，2，1，1，4}，k = 2
> **输出:** 6
> 第二个数组的平均值为 1.5。
> 因此，1、2、3 是唯一与平均值之差小于 2 的元素
> 
> **输入:** arr1[] = {5、10、2、6、1、8、6、12}，arr2[] = {6、5、11、4、2、3、7}，k = 4
> **输出:** 5

**方法:**计算第二个数组的平均值，然后遍历第一个数组，计算那些与平均值绝对差为 **< k** 的元素的和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function for finding sum of elements
// whose diff with mean is not more than k
int findSumofEle(int arr1[], int m,
                 int arr2[], int n, int k)
{
    float arraySum = 0;

    // Find the mean of second array
    for (int i = 0; i < n; i++)
        arraySum += arr2[i];
    float mean = arraySum / n;

    // Find sum of elements from array1
    // whose difference with mean in not more than k
    int sumOfElements = 0;
    float difference;

    for (int i = 0; i < m; i++) {
        difference = arr1[i] - mean;
        if ((difference < 0) && (k > (-1) * difference)) {
            sumOfElements += arr1[i];
        }
        if ((difference >= 0) && (k > difference)) {
            sumOfElements += arr1[i];
        }
    }

    // Return result
    return sumOfElements;
}

// Driver code
int main()
{
    int arr1[] = { 1, 2, 3, 4, 7, 9 };
    int arr2[] = { 0, 1, 2, 1, 1, 4 };
    int k = 2;
    int m, n;

    m = sizeof(arr1) / sizeof(arr1[0]);
    n = sizeof(arr2) / sizeof(arr2[0]);

    cout << findSumofEle(arr1, m, arr2, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function for finding sum of elements
// whose diff with mean is not more than k
static int findSumofEle(int []arr1, int m,
                int []arr2, int n, int k)
{
    float arraySum = 0;

    // Find the mean of second array
    for (int i = 0; i < n; i++)
        arraySum += arr2[i];
    float mean = arraySum / n;

    // Find sum of elements from array1
    // whose difference with mean in not more than k
    int sumOfElements = 0;
    float difference = 0;

    for (int i = 0; i < m; i++)
    {
        difference = arr1[i] - mean;
        if ((difference < 0) && (k > (-1) * difference))
        {
            sumOfElements += arr1[i];
        }
        if ((difference >= 0) && (k > difference))
        {
            sumOfElements += arr1[i];
        }
    }

    // Return result
    return sumOfElements;
}

// Driver code
public static void main (String[] args)
{
    int []arr1 = { 1, 2, 3, 4, 7, 9 };
    int []arr2 = { 0, 1, 2, 1, 1, 4 };
    int k = 2;

    int m = arr1.length;
    int n = arr2.length;

    System.out.println(findSumofEle(arr1, m, arr2, n, k));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function for finding sum of elements
# whose diff with mean is not more than k
def findSumofEle(arr1, m, arr2, n, k):
    arraySum = 0

    # Find the mean of second array
    for i in range(n):
        arraySum += arr2[i]
    mean = arraySum / n

    # Find sum of elements from array1
    # whose difference with mean
    # is not more than k
    sumOfElements = 0
    difference = 0

    for i in range(m):

        difference = arr1[i] - mean

        if ((difference < 0) and (k > (-1) * difference)):
            sumOfElements += arr1[i]

        if ((difference >= 0) and (k > difference)):
            sumOfElements += arr1[i]

    # Return result
    return sumOfElements

# Driver code
arr1 = [ 1, 2, 3, 4, 7, 9]
arr2 = [ 0, 1, 2, 1, 1, 4]
k = 2

m = len(arr1)
n = len(arr2)

print(findSumofEle(arr1, m, arr2, n, k))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function for finding sum of elements
// whose diff with mean is not more than k
static int findSumofEle(int []arr1, int m,
                int []arr2, int n, int k)
{
    float arraySum = 0;

    // Find the mean of second array
    for (int i = 0; i < n; i++)
        arraySum += arr2[i];
    float mean = arraySum / n;

    // Find sum of elements from array1
    // whose difference with mean in not more than k
    int sumOfElements = 0;
    float difference = 0;

    for (int i = 0; i < m; i++)
    {
        difference = arr1[i] - mean;
        if ((difference < 0) && (k > (-1) * difference))
        {
            sumOfElements += arr1[i];
        }
        if ((difference >= 0) && (k > difference))
        {
            sumOfElements += arr1[i];
        }
    }

    // Return result
    return sumOfElements;
}

// Driver code
static void Main()
{
    int []arr1 = { 1, 2, 3, 4, 7, 9 };
    int []arr2 = { 0, 1, 2, 1, 1, 4 };
    int k = 2;

    int m = arr1.Length;
    int n = arr2.Length;

    Console.WriteLine(findSumofEle(arr1, m, arr2, n, k));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function for finding sum of elements
// whose diff with mean is not more than k
function findSumofEle($arr1, $m, $arr2, $n, $k)
{
    $arraySum = 0;

    // Find the mean of second array
    for ($i = 0; $i < $n; $i++)
        $arraySum += $arr2[$i];

    $mean = $arraySum / $n;

    // Find sum of elements from array1
    // whose difference with mean
    // is not more than k
    $sumOfElements = 0;

    for ($i = 0; $i < $m; $i++)
    {
        $difference = $arr1[$i] - $mean;
        if (($difference < 0) &&
            ($k > (-1) * $difference))
        {
            $sumOfElements += $arr1[$i];
        }
        if (($difference >= 0) &&
            ($k > $difference))
        {
            $sumOfElements += $arr1[$i];
        }
    }

    // Return result
    return $sumOfElements;
}

// Driver code
$arr1 = array( 1, 2, 3, 4, 7, 9 );
$arr2 = array( 0, 1, 2, 1, 1, 4 );
$k = 2;

$m = count($arr1);
$n = count($arr2);

print(findSumofEle($arr1, $m,
                   $arr2, $n, $k));

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function for finding sum of elements
// whose diff with mean is not more than k
function findSumofEle(arr1, m, arr2, n, k)
{
    var arraySum = 0;

    // Find the mean of second array
    for (var i = 0; i < n; i++)
        arraySum += arr2[i];
    var mean = (arraySum / n);

    // Find sum of elements from array1
    // whose difference with mean in not more than k
    var sumOfElements = 0;
    var difference;

    for (var i = 0; i < m; i++) {
        difference = arr1[i] - mean;
        if ((difference < 0) && (k > (-1) * difference)) {
            sumOfElements += arr1[i];
        }
        if ((difference >= 0) && (k > difference)) {
            sumOfElements += arr1[i];
        }
    }

    // Return result
    return sumOfElements;
}

// Driver code
var arr1 = [ 1, 2, 3, 4, 7, 9 ];
var arr2 = [ 0, 1, 2, 1, 1, 4 ];
var k = 2;
var m, n;
m = arr1.length;
n = arr2.length;
document.write( findSumofEle(arr1, m, arr2, n, k));

</script>
```

**Output:** 

```
6
```