# 将阵列中的完美正方形排列在它们的相对位置

> 原文:[https://www . geeksforgeeks . org/sort-完美阵列中相对位置的正方形/](https://www.geeksforgeeks.org/sort-perfect-squares-in-an-array-at-their-relative-positions/)

给定一个整数数组![arr ](img/30cc397b6188b98ce45d51c03c5400b3.png "Rendered by QuickLaTeX.com")，任务是只对在数组中相对位置为完美正方形的元素进行排序(不得影响其他元素的位置)。
**例:**

> **输入:** arr[] = {2，64，9，8，1，4}
> **输出:** 2 1 4 8 9 64
> 1，4，9 和 64 是数组中唯一的完美方块。
> **输入:** arr[] = {1，49，2，36}
> **输出:** 1 36 2 49

**进场:**

*   初始化两个空向量，[从左到右遍历数组](https://www.geeksforgeeks.org/loops-in-c/)。
*   取一个整数和一个浮点变量，对于数组存储的每个元素，它都是这两个变量的平方根。
*   如果两个变量相等，那么在第一个向量中推这个元素的索引，在第二个向量中推元素本身。
*   对第二个向量进行排序。
*   现在，我们有了第一个向量中所有必需元素的索引，也有了第二个向量中所有按排序的必需元素的索引。
*   因此，将第二个向量的元素逐个插入数组中第一个向量的索引处。

以下是上述方法的实现:

## C++

```
// C++ program to sort all the elements that are
// perfect squares in their relative positions
#include <bits/stdc++.h>
using namespace std;

// function to sort all the elements that are
// perfect squares in their relative positions
void sortPerfectSquare(int arr[], int n)
{
    int a;
    float b;

    // v1 will contain index of perfect squares
    // v2 will contain each perfect square
    vector<int> v1;
    vector<int> v2;

    for (int i = 0; i < n; i++) {
        b = sqrt(arr[i]);
        a = b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b) {
            v1.push_back(i);
            v2.push_back(arr[i]);
        }
    }

    // sort second vector
    sort(v2.begin(), v2.end());

    // put the sorted perfect square
    // back into the array
    int j = 0;
    for (int i = 0; i < n; i++) {
        if (v1[j] == i) {
            arr[i] = v2[j];
            j++;
        }
    }

    // print final array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 9, 44, 100, 81, 21, 64 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortPerfectSquare(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort all the elements that are
// perfect squares in their relative positions
import java.util.*;

class GFG
{

// function to sort all the elements that are
// perfect squares in their relative positions
static void sortPerfectSquare(int arr[], int n)
{
    int a;
    float b;

    // v1 will contain index of perfect squares
    // v2 will contain each perfect square
    Vector<Integer> v1 = new Vector<Integer>();
    Vector<Integer> v2 = new Vector<Integer>();

    for (int i = 0; i < n; i++)
    {
        b = (float) Math.sqrt(arr[i]);
        a = (int) b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
        {
            v1.add(i);
            v2.add(arr[i]);
        }
    }

    // sort second vector
    Collections.sort(v2);

    // put the sorted perfect square
    // back into the array
    int j = 0;
    for (int i = 0; i < n; i++)
    {
        if (v1.get(j) == i)
        {
            arr[i] = v2.get(j);
            j++;
        }
    }

    // print final array
    for (int i = 0; i < n; i++)
            System.out.print(arr[i]+" ");
}

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 9, 44, 100, 81, 21, 64 };
        int n = arr.length;

        sortPerfectSquare(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to sort all
# the elements that are perfect
# squares in their relative positions

# import sqrt() from math lib
from math import sqrt

# function to sort all the elements
# that are perfect squares in their
# relative positions
def sortPerfectSquare(arr, n) :

    # v1 will contain index of
    # perfect squares and v2 will
    # contain each perfect square
    v1 = []
    v2 = []

    for i in range(n):
        b = sqrt(arr[i])
        a = int(b)

        # if both a and b are equal then
        # arr[i] is a perfect square
        if a == b :
            v1.append(i)
            v2.append(arr[i])

    # sort second list
    v2.sort()

    j = 0

    # put the sorted perfect square
    # back into the array
    for i in range(n) :
        if v1[j] == i :
            arr[i] = v2[j]
            j += 1

    # print final array
    for i in range(n) :
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__" :
    arr = [9, 44, 100, 81, 21, 64]
    n = len(arr)

    sortPerfectSquare(arr, n);

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to sort all the elements that are
// perfect squares in their relative positions
using System;
using System.Collections.Generic;

class GFG
{

// function to sort all the elements that are
// perfect squares in their relative positions
static void sortPerfectSquare(int []arr, int n)
{
    int a;
    float b;

    // v1 will contain index of perfect squares
    // v2 will contain each perfect square
    List<int> v1 = new List<int>();
    List<int>v2 = new List<int>();

    for (int i = 0; i < n; i++)
    {
        b = (float) Math.Sqrt(arr[i]);
        a = (int) b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
        {
            v1.Add(i);
            v2.Add(arr[i]);
        }
    }

    // sort second vector
    v2.Sort();

    // put the sorted perfect square
    // back into the array
    int j = 0;
    for (int i = 0; i < n; i++)
    {
        if (v1[j] == i)
        {
            arr[i] = v2[j];
            j++;
        }
    }

    // print final array
    for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 9, 44, 100, 81, 21, 64 };
    int n = arr.Length;

    sortPerfectSquare(arr, n);
}
}

// This code is contributed by
// PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort all the elements that are
// perfect squares in their relative positions

// function to sort all the elements that are
// perfect squares in their relative positions
function sortPerfectSquare($arr, $n)
{
    // v1 will contain index of perfect squares
    // v2 will contain each perfect square
    $v1 = array();
    $v2 = array();

    for ( $i = 0; $i < $n; $i++)
    {
        $b = sqrt($arr[$i]);
        $a = (int)$b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if ($a == $b)
        {
            array_push($v1, $i);
            array_push($v2, $arr[$i]);
        }
    }

    // sort second vector
    sort($v2);

    // put the sorted perfect square
    // back into the array
    $j = 0;
    for ( $i = 0; $i < $n; $i++)
    {
        if ($v1[$j] == $i)
        {
            $arr[$i] = $v2[$j];
            $j++;
        }
    }

    // print final array
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Driver Code
$arr = array( 9, 44, 100, 81, 21, 64 );
$n = count($arr);
sortPerfectSquare($arr, $n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program to sort all the elements that are
// perfect squares in their relative positions

// function to sort all the elements that are
// perfect squares in their relative positions
function sortPerfectSquare(arr, n)
{
    var a;
    var b;

    // v1 will contain index of perfect squares
    // v2 will contain each perfect square
    var v1 = [];
    var v2 = [];

    for (var i = 0; i < n; i++) {
        b = Math.sqrt(arr[i]);
        a = parseInt(b);

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b) {
            v1.push(i);
            v2.push(arr[i]);
        }
    }

    // sort second vector
    v2.sort((a,b) => a-b)

    // put the sorted perfect square
    // back into the array
    var j = 0;
    for (var i = 0; i < n; i++) {
        if (v1[j] == i) {
            arr[i] = v2[j];
            j++;
        }
    }

    // print final array
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Driver code
var arr = [9, 44, 100, 81, 21, 64 ];
var n = arr.length;
sortPerfectSquare(arr, n);

</script>
```

**Output:** 

```
9 44 64 81 21 100
```