# 检查一个数组中完美平方的和是否能被 x 整除

> 原文:[https://www . geeksforgeeks . org/check-如果数组中的完美平方和被 x 整除/](https://www.geeksforgeeks.org/check-if-the-sum-of-perfect-squares-in-an-array-is-divisible-by-x/)

给定一个数组 **arr[]** 和一个整数 **x** ，任务是检查数组中所有完美平方的和是否能被 **x** 整除。如果可分，则打印**是**否则打印**否**。
**举例:**

> **输入:** arr[] = {2，3，4，6，9，10}，x = 13
> **输出:**是
> 4 和 9 是数组中唯一的完美正方形
> 和= 4 + 9 = 13(可被 13 整除)
> **输入:**arr[= { 2，4，25，49，3，8}，x = 9
> **输出:**否

**方法:**从 **i** 到**n–1**运行一个循环，检查**arr【I】**是否是完美的正方形。如果 **arr[i]** 是一个完美的正方形，那么更新 **sum = sum + arr[i]** 。如果最后**总和% x = 0** 则打印**是**否则打印**否**。要检查一个元素是否是完美的正方形，请遵循以下步骤:

> 假设 **num** 是一个整数元素
> float sq = sqrt(x)
> 如果 **floor(sq) = ceil(sq)** 那么 **num** 就是一个完美的正方形，否则就不是。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the sum of all the
// perfect squares of the given array are divisible by x
bool check(int arr[], int x, int n)
{
    long long sum = 0;
    for (int i = 0; i < n; i++) {
        double x = sqrt(arr[i]);

        // If arr[i] is a perfect square
        if (floor(x) == ceil(x)) {
            sum += arr[i];
        }
    }

    if (sum % x == 0)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 9, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 13;

    if (check(arr, x, n)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG{

    // Function that returns true if the the sum of all the
    // perfect squares of the given array is divisible by x
    static boolean check(int arr[], int x, int n)
    {
        long sum = 0;
        for (int i = 0; i < n; i++) {
            double y = Math.sqrt(arr[i]);

            // If arr[i] is a perfect square
            if (Math.floor(y) == Math.ceil(y)) {
                sum += arr[i];
            }
        }

        if (sum % x == 0)
            return true;
        else
            return false;
    }

    // Driver Code
    public static void main(String []args){
        int arr[] = { 2, 3, 4, 9, 10 };
        int n = arr.length ;
        int x = 13;

        if (check(arr, x, n)) {
            System.out.println("Yes");
        }
        else {
           System.out.println("No");
        }
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function that returns true if the the sum of all the
# perfect squares of the given array is divisible by x
def check (a, y):
    sum = 0
    for i in range(len(a)):

        x = math.sqrt(a[i])

        # If a[i] is a perfect square
        if (math.floor(x) == math.ceil(x)):
            sum = sum + a[i]

    if (sum % y == 0):
        return True
    else:
        return False

# Driver code
a = [2, 3, 4, 9, 10]
x = 13

if check(a, x) :
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach

using System;
public class GFG{

    // Function that returns true if the the sum of all the
    // perfect squares of the given array is divisible by x
    static bool check(int[] arr, int x, int n)
    {
        long sum = 0;
        for (int i = 0; i < n; i++) {
            double y = Math.Sqrt(arr[i]);

            // If arr[i] is a perfect square
            if (Math.Floor(y) == Math.Ceiling(y)) {
                sum += arr[i];
            }
        }

        if (sum % x == 0)
            return true;
        else
            return false;
    }

    // Driver Code
    public static void Main(){
        int[] arr = { 2, 3, 4, 9, 10 };
        int n = arr.Length ;
        int x = 13;

        if (check(arr, x, n)) {
            Console.Write("Yes");
        }
        else {
           Console.Write("No");
        }
    }   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if the
// sum of all the perfect squares of
// the given array is divisible by x
function check($arr, $x, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $x = sqrt($arr[$i]);

        // If arr[i] is a perfect square
        if (floor($x) == ceil($x))
        {
            $sum += $arr[$i];
        }
    }

    if (($sum % $x) == 0)
        return true;
    else
        return false;
}

// Driver code
$arr = array( 2, 3, 4, 9, 10 );
$n = sizeof($arr);
$x = 13;

if (!check($arr, $x, $n))
{
    echo "Yes";
}
else
{
    echo "No";
}

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function that returns true if the the sum of all the
    // perfect squares of the given array is divisible by x
    function check(arr,x,n)
    {
        let sum = 0;
        for (let i = 0; i < n; i++) {
            let y = Math.sqrt(arr[i]);

            // If arr[i] is a perfect square
            if (Math.floor(y) == Math.ceil(y)) {
                sum += arr[i];
            }
        }

        if (sum % x == 0)
            return true;
        else
            return false;
    }
    // Driver Code

    let arr=[ 2, 3, 4, 9, 10];
    let n = arr.length ;
    let x = 13;
    if (check(arr, x, n)) {
        document.write("Yes");
    }
    else {
       document.write("No");
    }

    // This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```