# 使给定集合的 MEX 等于 x 的最小操作

> 原文:[https://www . geesforgeks . org/round-1-能力倾向测验-2 小时-这一轮被分成 2 个部分-能力倾向和技术部分-能力倾向-问题-仅包含-流程图-基于问题-技术问题-包含-sql/](https://www.geeksforgeeks.org/round-1-aptitude-test-2hrs-this-round-was-divided-into-2-sections-aptitude-and-technical-sections-aptitude-questions-contained-only-flowcharts-based-questions-technical-questions-included-sql/)

给定一组 n 个整数，执行最少次数的操作(可以在集合中插入/删除元素)，使集合的 **MEX** 等于 x(即给定的)。
**注:-** 一组整数的 **MEX** 是其中不存在的最小非负整数。例如，集合{0，2，4}的 **MEX** 为 1，集合{1，2，3}的 **MEX** 为 0。
**举例:**

```
Input : n = 5, x = 3
        0 4 5 6 7
Output : 2
The MEX of the set {0, 4, 5, 6, 7} is 1 which is 
not equal to 3\. So, we should add 1 and 2 to the
set. After adding 1 and 2, the set becomes 
{0, 1, 2, 4, 5, 6, 7} and 3 is the minimum
non-negative integer that doesn't exist in it.
So, the MEX of this set is 3 which is equal to
x i.e. 3\. So, the output of this example is 2 
as we inserted 1 and 2 in the set.

Input : n = 1, x = 0
        1
Output : 0
In this example, the MEX of the given set {1}
is already 0\. So, we do not need to perform 
any operation. So, the output is 0.
```

**方法:**
方法是看到最终集合中所有小于 x 的元素都应该存在，x 不应该存在，任何大于 x 的元素都无所谓。因此，我们将计算初始集合中不存在的小于 x 的元素的数量，并将其添加到答案中。如果 x 存在，我们将在答案中加上 1，因为 x 应该被去掉。
以下是上述办法的实施:

## C++

```
// CPP program to perform minimal number
// of operations to make the MEX of the
// set equal to the given number x.
#include <bits/stdc++.h>
using namespace std;

// function to find minimum number of
// operations required
int minOpeartions(int arr[], int n, int x)
{
    int k = x, i = 0;
    while (n--) {

        // if the element is less than x.
        if (arr[n] < x)
            k--;

        // if the element equals to x.
        if (arr[n] == x)
            k++;
    }
    return k;
}

// driver function
int main()
{
    int arr[] = { 0, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 3;
    // output
    cout << minOpeartions(arr, n, x) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform minimal number
// of operations to make the MEX of the
// set equal to the given number x.
import java.io.*;

class GFG {

    // function to find minimum number of
    // operations required
    static int minOpeartions(int arr[], int n, int x)
    {

        int k = x, i = 0;
        n--;

        while (n > -1) {

            // if the element is less than x.
            if (arr[n] < x)
                k--;

            // if the element equals to x.
            if (arr[n] == x)
                k++;

            n--;
        }

        return k;
    }

    // driver function
    public static void main(String args[])
    {
        int arr[] = { 0, 4, 5, 6, 7 };
        int n = arr.length;
        int x = 3;

        // output
        System.out.println(minOpeartions(arr, n, x));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python 3 program to perform minimal number
# of operations to make the MEX of the
# set equal to the given number x.

# function to find minimum number of
# operations required
def minOpeartions(arr, n, x) :

    k = x
    i = 0
    n = n-1
    while (n>-1) :

        # if the element is less than x.
        if (arr[n] < x) :
            k = k - 1

        # if the element equals to x.
        if (arr[n] == x) :
            k = k + 1
        n = n - 1

    return k

# driver function
arr = [ 0, 4, 5, 6, 7 ]
n = len(arr)
x = 3

# output
print( minOpeartions(arr, n, x))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to perform minimal number
// of operations to make the MEX of the
// set equal to the given number x.
using System;

class GFG {

    // function to find minimum number
    // of operations required
    static int minOpeartions(int[] arr,
                           int n, int x)
    {

        int k = x;
        n--;

        while (n > -1) {

            // if the element is less
            // than x.
            if (arr[n] < x)
                k--;

            // if the element equals
            // to x.
            if (arr[n] == x)
                k++;

            n--;
        }

        return k;
    }

    // driver function
    public static void Main()
    {
        int[] arr = { 0, 4, 5, 6, 7 };
        int n = arr.Length;
        int x = 3;

        // output
        Console.WriteLine(
            minOpeartions(arr, n, x));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to perform minimal
// number of operations to make
// the MEX of the set equal to
// the given number x.

// function to find minimum number
// of operations required
function minOpeartions( $arr, $n, $x)
{
    $k = $x; $i = 0;
    while ($n--)
    {

        // if the element is
        // less than x.
        if ($arr[$n] < $x)
            $k--;

        // if the element equals to x.
        if ($arr[$n] == $x)
            $k++;
    }
    return $k;
}

// Driver Code
$arr = array(0, 4, 5, 6, 7);
$n = count($arr);
$x = 3;

echo minOpeartions($arr, $n, $x) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript program to perform minimal number
    // of operations to make the MEX of the
    // set equal to the given number x.

    // function to find minimum number of
    // operations required
    function minOpeartions(arr, n, x)
    {
        let k = x, i = 0;
        while (n-- > 0) {

            // if the element is less than x.
            if (arr[n] < x)
                k--;

            // if the element equals to x.
            if (arr[n] == x)
                k++;
        }
        return k;
    }

    let arr = [ 0, 4, 5, 6, 7 ];
    let n = arr.length;
    let x = 3;
    // output
    document.write(minOpeartions(arr, n, x));

</script>
```

**输出:**

```
2
```