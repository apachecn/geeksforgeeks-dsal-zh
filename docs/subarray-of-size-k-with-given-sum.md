# 给定和的 k 尺寸子阵列

> 原文:[https://www . geesforgeks . org/subarray-of-size-k-with-given-sum/](https://www.geeksforgeeks.org/subarray-of-size-k-with-given-sum/)

给定一个数组 arr[]，一个整数 K 和一个 Sum。任务是检查是否存在任何具有 K 个元素的子阵列，其和等于给定的和。如果尺寸为 K 的任何子阵列的总和等于给定的总和，则打印是，否则打印否
**示例** :

```
Input: arr[] = {1, 4, 2, 10, 2, 3, 1, 0, 20}
        k = 4, sum = 18
Output: YES
Subarray = {4, 2, 10, 2}

Input: arr[] = {1, 4, 2, 10, 2, 3, 1, 0, 20}
        k = 3, sum = 6
Output: YES
```

一个**简单的解决方案**是使用嵌套循环，在这里我们检查每个大小为 k 的子阵列。
下面是上述方法的实现:

## C++

```
// CPP program to check if any Subarray of size
// K has a given Sum
#include <iostream>
using namespace std;

// Function to check if any Subarray of size K
// has a  given Sum
bool checkSubarraySum(int arr[], int n,
                      int k, int sum)
{
    // Consider all blocks starting with i.
    for (int i = 0; i < n - k + 1; i++) {

        int current_sum = 0;

        // Consider each subarray of size k
        for (int j = 0; j < k; j++)
            current_sum = current_sum + arr[i + j];

        if (current_sum == sum)
            return true;       
    }
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 2, 10, 2, 3, 1, 0, 20 };
    int k = 4;
    int sum = 18;

    int n = sizeof(arr) / sizeof(arr[0]);

    if (checkSubarraySum(arr, n, k, sum))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if any Subarray of size
// K has a given Sum
class GFG
{

// Function to check if any
// Subarray of size K has
// a given Sum
static boolean checkSubarraySum(int arr[], int n,
                                int k, int sum)
{
    // Consider all blocks
    // starting with i.
    for (int i = 0; i < n - k + 1; i++)
    {

        int current_sum = 0;

        // Consider each
        // subarray of size k
        for (int j = 0; j < k; j++)
            current_sum = current_sum +
                          arr[i + j];

        if (current_sum == sum)
            return true;    
    }
    return false;
}

// Driver code
public static void main(String args[])
{
    int arr[] = new int[] { 1, 4, 2, 10, 2,
                            3, 1, 0, 20 };
    int k = 4;
    int sum = 18;

    int n = arr.length;

    if (checkSubarraySum(arr, n, k, sum))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python3 program to check
# if any Subarray of size
# K has a given Sum

# Function to check if
# any Subarray of size
# K, has a given Sum
def checkSubarraySum(arr, n, k, sum):

    # Consider all blocks
    # starting with i.
    for i in range (n - k + 1):

        current_sum = 0;

        # Consider each subarray
        # of size k
        for j in range(k):
            current_sum = (current_sum +
                            arr[i + j]);

        if (current_sum == sum):
            return True;    
    return False;

# Driver code
arr = [1, 4, 2, 10, 2,
          3, 1, 0, 20];
k = 4;
sum = 18;

n = len(arr);

if (checkSubarraySum(arr, n, k, sum)):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
// C# program to check if any
// Subarray of size K has a given Sum
using System;
class GFG
{

// Function to check if any Subarray
// of size K has a given Sum
static bool checkSubarraySum(int[] arr, int n,
                             int k, int sum)
{
    // Consider all blocks
    // starting with i.
    for (int i = 0; i < n - k + 1; i++)
    {

        int current_sum = 0;

        // Consider each
        // subarray of size k
        for (int j = 0; j < k; j++)
            current_sum = current_sum +
                            arr[i + j];

        if (current_sum == sum)
            return true;    
    }
    return false;
}

// Driver code
static void Main()
{
    int[] arr = new int[] { 1, 4, 2, 10,
                            2, 3, 1, 0, 20 };
    int k = 4;
    int sum = 18;

    int n = arr.Length;

    if (checkSubarraySum(arr, n, k, sum))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if any Subarray of size
// K has a given Sum

// Function to check if
// any Subarray of size
// K, has a given Sum
function checkSubarraySum($arr, $n,
                          $k, $sum)
{
    // Consider all blocks starting with i.
    for ($i = 0; $i < $n - $k + 1; $i++)
    {

        $current_sum = 0;

        // Consider each subarray of size k
        for ($j = 0; $j < $k; $j++)
            $current_sum = $current_sum +
                           $arr[$i + $j];

        if ($current_sum == $sum)
            return true;    
    }
    return false;
}

// Driver code
$arr = array(1, 4, 2, 10, 2,
             3, 1, 0, 20);
$k = 4;
$sum = 18;

$n = sizeof($arr);

if (checkSubarraySum($arr, $n,
                     $k, $sum))
    echo "YES";
else
    echo "NO";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if any
    // Subarray of size K has a given Sum

    // Function to check if any Subarray
    // of size K has a given Sum
    function checkSubarraySum(arr, n, k, sum)
    {

        // Consider all blocks
        // starting with i.
        for (let i = 0; i < n - k + 1; i++)
        {

            let current_sum = 0;

            // Consider each
            // subarray of size k
            for (let j = 0; j < k; j++)
                current_sum = current_sum + arr[i + j];

            if (current_sum == sum)
                return true;   
        }
        return false;
    }

    let arr = [ 1, 4, 2, 10, 2, 3, 1, 0, 20 ];
    let k = 4;
    let sum = 18;

    let n = arr.length;

    if (checkSubarraySum(arr, n, k, sum))
        document.write("YES");
    else
        document.write("NO");

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
YES
```