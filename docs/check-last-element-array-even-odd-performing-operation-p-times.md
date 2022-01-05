# 执行 p 次运算后检查数组的最后一个元素是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-last-element-array-偶数-奇数-执行-operation-p-times/](https://www.geeksforgeeks.org/check-last-element-array-even-odd-performing-operation-p-times/)

给定的是 n 个非负整数的数组。操作是在数组中插入一个严格大于数组当前总和的数字。执行 p 次运算后，找出数组的最后一个元素是偶数还是奇数。
示例:

```
Input : arr[] = {2, 3}
        P = 3
Output : EVEN
For p = 1, Array sum = 2 + 3 = 5\. 
So, we insert 6.
For p = 2, Array sum = 5 + 6 = 11\. 
So, we insert 12.
For p = 3, Array sum = 11 + 12 = 23\. 
So, we insert 24 (which is even).

Input : arr[] = {5, 7, 10}
        p = 1
Output : ODD
For p = 1, Array sum  = 5 + 7 + 10 = 22.
So, we insert 23 (which is odd).
```

**天真方法:**首先求给定数组的和。这可以在单个循环中完成。现在制作另一个大小为 P + N 的数组。这个数组将表示要插入的元素，最后一个元素将是我们需要的答案。在任何一步，如果数组元素之和的奇偶性为“偶数”，则插入元素的奇偶性为“奇数”。
**高效方法:**假设数组的和为偶数，下一个插入的元素为奇数。现在数组的和将是奇数，所以下一个插入的元素将是偶数，现在数组的和变成奇数，所以我们插入一个偶数，以此类推。我们可以推广，如果数组的和为偶数，那么对于 P = 1，最后插入的数为奇数，否则为偶数。
现在考虑数组的和为奇数的情况。下一个插入的元素将是偶数，现在数组的和将变成奇数，所以下一个插入的元素将是偶数，现在数组的和将是奇数，再加上另一个偶数，以此类推。在这种情况下，我们可以归纳出最后插入的数字总是偶数。
以下是上述方法的实现:

## C++

```
// CPP program to check whether the last
// element of the array is even or odd
// after performing the operation p times.
#include <bits/stdc++.h>
using namespace std;

string check_last(int arr[], int n, int p)
{
    int sum = 0;

    // sum of the array.
    for (int i = 0; i < n; i++)
        sum = sum + arr[i];

    if (p == 1) {

        // if sum is even
        if (sum % 2 == 0)
            return "ODD";
        else
            return "EVEN";
    }
    return "EVEN";
}

// driver code
int main()
{
    int arr[] = { 5, 7, 10 }, p = 1;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << check_last(arr, n, p) << endl;   
    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to check whether the last
# element of the array is even or odd
# after performing the operation p times.

def check_last (arr, n, p):
    _sum = 0

    # sum of the array.
    for i in range(n):
        _sum = _sum + arr[i]
    if p == 1:

        # if sum is even
        if _sum % 2 == 0:
            return "ODD"
        else:
            return "EVEN"
    return "EVEN"

# driver code
arr = [5, 7, 10]
p = 1
n = len(arr)
print(check_last (arr, n, p))

# This code is contributed by "Abhishek Sharma 44"
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the last
// element of the array is even or odd
// after performing the operation p times.
import java.util.*;

class Even_odd{

    public static String check_last(int arr[], int n, int p)
    {
        int sum = 0;

        // sum of the array.
        for (int i = 0; i < n; i++)
            sum = sum + arr[i];

        if (p == 1) {

            // if sum is even
            if (sum % 2 == 0)
                return "ODD";
            else
                return "EVEN";
        }  
        return "EVEN";
    }

    public static void main(String[] args)
    {
        int arr[] = { 5, 7, 10 }, p = 1;
        int n = 3;
        System.out.print(check_last(arr, n, p));
    }
}

//This code is contributed by rishabh_jain
```

## C#

```
// C# program to check whether the last
// element of the array is even or odd
// after performing the operation p times.
using System;

class GFG {

    public static string check_last(int []arr, int n, int p)
    {
        int sum = 0;

        // sum of the array.
        for (int i = 0; i < n; i++)
            sum = sum + arr[i];

        if (p == 1) {

            // if sum is even
            if (sum % 2 == 0)
                return "ODD";
            else
                return "EVEN";
        }

        return "EVEN";
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 5, 7, 10 };
        int p = 1;
        int n = arr.Length;

        Console.WriteLine(check_last(arr, n, p));
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether the last
// element of the array is even or odd
// after performing the operation p times.

function check_last($arr, $n, $p)
{
    $sum = 0;

    // sum of the array.
    for ( $i = 0; $i < $n; $i++)
        $sum = $sum + $arr[$i];

    if ($p == 1) {

        // if sum is even
        if ($sum % 2 == 0)
            return "ODD";
        else
            return "EVEN";
    }
    return "EVEN";
}

    // Driver Code
    $arr = array(5, 7, 10);
    $p = 1;
    $n = count($arr);
    echo check_last($arr, $n, $p);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check whether the last
    // element of the array is even or odd
    // after performing the operation p times.

    function check_last(arr, n, p)
    {
        let sum = 0;

        // sum of the array.
        for (let i = 0; i < n; i++)
            sum = sum + arr[i];

        if (p == 1) {

            // if sum is even
            if (sum % 2 == 0)
                return "ODD";
            else
                return "EVEN";
        }
        return "EVEN";
    }

    let arr = [ 5, 7, 10 ], p = 1;
    let n = arr.length;
    document.write(check_last(arr, n, p));

    // This code is contributed by divyesh072019.
</script>
```

输出:

```
ODD
```

**时间复杂度:** O(n)