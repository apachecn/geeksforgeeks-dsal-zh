# 检查给定数组是否完美

> 原文:[https://www . geesforgeks . org/check-when-given-array-perfect-not/](https://www.geeksforgeeks.org/check-whether-given-array-perfect-not/)

有一个数组包含一些非负整数。检查数组是否完美。如果一个数组首先是严格递增的，然后是常数，最后是严格递减的，那么这个数组就叫做完美数组。三个部分中的任何一个都可以是空的。
**例:**

```
Input : arr[] = {1, 8, 8, 8, 3, 2}
Output : Yes
The array is perfect as it is first
increasing, then constant and finally
decreasing.

Input : arr[] = {1, 1, 2, 2, 1}
Output : No
The first part is not strictly increasing

Input : arr[] = {4, 4, 4, 4}
Output : Yes
```

方法是从左到右迭代数组，并增加 I(最初为 1)，而下一个元素严格来说比前面的更多。然后，从左向右迭代数组，并在两个相邻元素相等时增加 I。最后，从左到右迭代数组，并在下一个元素严格小于前一个元素时增加 I。如果我们通过这个过程到达终点，我们说这个阵列是完美的。

## C++

```
// CPP program to check whether the given array
// is perfect or not.
#include <iostream>
using namespace std;

int checkUnimodal(int arr[], int n)
{
    // Cover first strictly increasing part
    int i = 1;
    while (arr[i] > arr[i - 1] && i < n)
        ++i;

    // Cover middle equal part
    while (arr[i] == arr[i - 1] && i < n)
        ++i;

    // Cover last decreasing part
    while (arr[i] < arr[i - 1] && i < n)
        ++i;

    // Return true if we reached end.
    return (i == n);
}

int main()
{
    int arr[] = { 1, 5, 5, 5, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (checkUnimodal(arr, n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the given array
// is perfect or not.
import java.util.*;

class Node
{

static boolean checkUnimodal(int arr[], int n)
{
    // Cover first strictly increasing part
    int i = 1;
    while (i < n && arr[i] > arr[i - 1])
        ++i;

    // Cover middle equal part
    while (i < n && arr[i] == arr[i - 1])
        ++i;

    // Cover last decreasing part
    while (i < n &&arr[i] < arr[i - 1])
        ++i;

    // Return true if we reached end.
    return (i == n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 5, 5, 4, 2 };
    int n = arr.length;
    if (checkUnimodal(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to check whether the
# given array is perfect or not.

def checkUnimodal(arr, n):

    # Cover first strictly increasing part
    i = 1
    while (i < n and arr[i] > arr[i - 1]):
        i += 1

    # Cover middle equal part
    while (i < n and arr[i] == arr[i - 1]):
        i += 1

    # Cover last decreasing part
    while (i < n and arr[i] < arr[i - 1]):
        i += 1

    # Return true if we reached end.
    return (i == n)

# Driver Code
if __name__ == '__main__':
    arr = [1, 5, 5, 5, 4, 2 ]
    n = len(arr)
    if (checkUnimodal(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check whether the given array
// is perfect or not.
using System;

class GFG
{
    static bool checkUnimodal(int []arr, int n)
{
    // Cover first strictly increasing part
    int i = 1;
    while (i < n && arr[i] > arr[i - 1])
        ++i;

    // Cover middle equal part
    while (i < n && arr[i] == arr[i - 1])
        ++i;

    // Cover last decreasing part
    while (i < n &&arr[i] < arr[i - 1])
        ++i;

    // Return true if we reached end.
    return (i == n);
}

// Driver code
static public void Main ()
{
    int []arr = { 1, 5, 5, 5, 4, 2 };
    int n = arr.Length;
    if (checkUnimodal(arr, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ajit..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether the
// given array is perfect or not.

function check($arr, $n)
{
    // Cover first strictly increasing part
    $i = 1;
    while ($arr[$i] > $arr[$i - 1] && $i < $n)
        ++$i;

    // Cover middle equal part
    while ($arr[$i] == $arr[$i - 1] && $i < $n)
        ++$i;

    // Cover last decreasing part
    while ($arr[$i] < $arr[$i - 1] && $i < $n)
        ++$i;

    // Return true if we reached end
    return ($i == $n);
}

// Driver Code
$arr = array(1, 5, 5, 5, 4, 2);
$n = sizeof($arr);
if (check($arr, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to check whether the given array
    // is perfect or not.

    function checkUnimodal(arr, n)
    {
        // Cover first strictly increasing part
        let i = 1;
        while (arr[i] > arr[i - 1] && i < n)
            ++i;

        // Cover middle equal part
        while (arr[i] == arr[i - 1] && i < n)
            ++i;

        // Cover last decreasing part
        while (arr[i] < arr[i - 1] && i < n)
            ++i;

        // Return true if we reached end.
        return (i == n);
    }

    let arr = [ 1, 5, 5, 5, 4, 2 ];
    let n = arr.length;
    if (checkUnimodal(arr, n))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**输出:**

```
YES
```