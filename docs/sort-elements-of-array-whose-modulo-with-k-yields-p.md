# 对以 K 为模得到 P 的数组元素进行排序

> 原文:[https://www . geeksforgeeks . org/sort-elements-of-of-array-with-k-模产生-p/](https://www.geeksforgeeks.org/sort-elements-of-array-whose-modulo-with-k-yields-p/)

给定一个整数数组和一个数字 K。任务是只对数组中那些被 K 除后产生余数 P 的元素进行排序。排序必须只在它们的**相对位置**进行，而不影响任何其他元素。
**示例** :

> **输入** : arr[] = {10，3，2，6，12}，K = 4，P = 2
> **输出** : 2 3 6 10 12
> **输入** : arr[] = {3，4，5，10，11，1}，K = 3，P = 1
> **输出** : 3 1 5 4 11 10

**进场:**

*   初始化两个空的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。
*   遍历数组，从左到右，用 k 检查每个元素的模
*   在第一个向量中，插入产生余数 p 的所有元素的索引
*   在第二个向量中，插入产生余数 p 的元素
*   对第二个向量进行排序。
*   现在，我们有了所有必需元素的索引，也有了所有必需元素的排序顺序。
*   因此，将第二个向量的元素逐个插入数组中第一个向量的索引处。

以下是上述方法的实现:

## C++

```
// C++ program for sorting array elements
// whose modulo with K yields P

#include <bits/stdc++.h>
using namespace std;

// Function to sort elements
// whose modulo with K yields P
void sortWithRemainderP(int arr[], int n, int k, int p)
{
    // initialise two vectors
    vector<int> v1, v2;

    for (int i = 0; i < n; i++) {
        if (arr[i] % k == p) {

            // first vector contains indices of
            // required element
            v1.push_back(i);

            // second vector contains
            // required elements
            v2.push_back(arr[i]);
        }
    }

    // sorting the elements in second vector
    sort(v2.begin(), v2.end());

    // replacing the elements whose modulo with K yields P
    // with the sorted elements
    for (int i = 0; i < v1.size(); i++)
        arr[v1[i]] = v2[i];

    // printing the new sorted array elements
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 8, 255, 16, 2, 4, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    int p = 0;

    sortWithRemainderP(arr, n, k, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for sorting array elements
// whose modulo with K yields P
import java.util.*;
class GFG
{

// Function to sort elements
// whose modulo with K yields P
static void sortWithRemainderP(int arr[], int n, int k, int p)
{
    // initialise two vectors
    Vector<Integer> v1 = new Vector<Integer>();
    Vector<Integer> v2 = new Vector<Integer>();

    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == p)
        {

            // first vector contains indices of
            // required element
            v1.add(i);

            // second vector contains
            // required elements
            v2.add(arr[i]);
        }
    }

    // sorting the elements in second vector
    Collections.sort(v2);

    // replacing the elements whose modulo with K yields P
    // with the sorted elements
    for (int i = 0; i < v1.size(); i++)
        arr[v1.get(i)] = v2.get(i);

    // printing the new sorted array elements
    for (int i = 0; i < n; i++)
            System.out.print(arr[i]+" ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 255, 16, 2, 4, 0 };
    int n = arr.length;
    int k = 2;
    int p = 0;

    sortWithRemainderP(arr, n, k, p);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for sorting array
# elements whose modulo with K yields P

# Function to sort elements whose modulo
# with K yields P
def sortWithRemainderP(arr, n, k, p):

    # initialise two vectors
    v1 = []
    v2 = []

    for i in range(0, n, 1):
        if (arr[i] % k == p):

            # first vector contains indices
            # of required element
            v1.append(i)

            # second vector contains
            # required elements
            v2.append(arr[i])

    # sorting the elements in second vector
    v2.sort(reverse = False)

    # replacing the elements whose modulo
    # with K yields P with the sorted elements
    for i in range(0, len(v1), 1):
        arr[v1[i]] = v2[i]

    # printing the new sorted array elements
    for i in range(0, n, 1):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [8, 255, 16, 2, 4, 0]
    n = len(arr)
    k = 2
    p = 0

    sortWithRemainderP(arr, n, k, p)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program for sorting array elements
// whose modulo with K yields P
using System;
using System.Collections.Generic;

class GFG
{

// Function to sort elements
// whose modulo with K yields P
static void sortWithRemainderP(int []arr, int n,
                               int k, int p)
{
    // initialise two vectors
    List<int> v1 = new List<int>();
    List<int> v2 = new List<int>();

    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == p)
        {

            // first vector contains indices of
            // required element
            v1.Add(i);

            // second vector contains
            // required elements
            v2.Add(arr[i]);
        }
    }

    // sorting the elements in second vector
    v2.Sort();

    // replacing the elements whose modulo with
    // K yields P with the sorted elements
    for (int i = 0; i < v1.Count; i++)
        arr[v1[i]] = v2[i];

    // printing the new sorted array elements
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 255, 16, 2, 4, 0 };
    int n = arr.Length;
    int k = 2;
    int p = 0;

    sortWithRemainderP(arr, n, k, p);
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for sorting array elements
// whose modulo with K yields P

// Function to sort elements
// whose modulo with K yields P
function sortWithRemainderP($arr, $n, $k, $p)
{
    // initialise two vectors
    $v1 = array();
    $v2 = array();

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] % $k == $p)
        {

            // first vector contains indices of
            // required element
            array_push($v1, $i);

            // second vector contains
            // required elements
            array_push($v2, $arr[$i]);
        }
    }

    // sorting the elements in second vector
    sort($v2);

    // replacing the elements whose modulo with K
    // yields P with the sorted elements
    for ($i = 0; $i < count($v1); $i++)
        $arr[$v1[$i]] = $v2[$i];

    // printing the new sorted array elements
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Driver code
$arr = array( 8, 255, 16, 2, 4, 0 );
$n = count($arr);
$k = 2;
$p = 0;

sortWithRemainderP($arr, $n, $k, $p);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for sorting array elements
// whose modulo with K yields P

// Function to sort elements
// whose modulo with K yields P
function sortWithRemainderP(arr, n, k, p)
{
    // initialise two vectors
    var v1 = [], v2 = [];

    for (var i = 0; i < n; i++) {
        if (arr[i] % k == p) {

            // first vector contains indices of
            // required element
            v1.push(i);

            // second vector contains
            // required elements
            v2.push(arr[i]);
        }
    }

    // sorting the elements in second vector
    v2.sort((a,b)=> a-b)

    // replacing the elements whose modulo with K yields P
    // with the sorted elements
    for (var i = 0; i < v1.length; i++)
        arr[v1[i]] = v2[i];

    // printing the new sorted array elements
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Driver code
var arr = [8, 255, 16, 2, 4, 0 ];
var n = arr.length;
var k = 2;
var p = 0;
sortWithRemainderP(arr, n, k, p);

</script>
```

**Output:** 

```
0 255 2 4 8 16
```

**时间复杂度:** O(nlogn)