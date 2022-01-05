# 基于参考位置的元素重新分配

> 原文:[https://www . geeksforgeeks . org/基于引用位置的元素重新分配/](https://www.geeksforgeeks.org/reallocation-of-elements-based-on-locality-of-reference/)

考虑一个问题，在这个问题中，相同的元素可能会被一次又一次地搜索。高效执行搜索操作。
**例:**

```
Input : arr[] = {12 25 36 85 98 75 89 15 63 66
                               64 74 27 83 97}
          q[] = {63, 63, 86, 63, 78}
Output : Yes Yes No Yes No
We need one by one search items of q[] in arr[].
The element 63 is present, 78 and 86 are not present.
```

思路是**简单**，我们把搜索到的元素移到数组前面，这样下次就可以快速搜索到了。

## C++

```
// C++ program to implement search for an item
// that is searched again and again.
#include <bits/stdc++.h>
using namespace std;

// A function to perform sequential search.
bool search(int arr[], int n, int x)
{
    // Linearly search the element
    int res = -1;
    for (int i = 0; i < n; i++)
        if (x == arr[i])
        res = i;

    // If not found
    if (res == -1)
        return false;

    // Shift elements before one position
    int temp = arr[res];
    for (int i = res; i > 0; i--)
        arr[i] = arr[i - 1];

    arr[0] = temp;
    return true;
}

// Driver Code
int main()
{
    int arr[] = { 12, 25, 36, 85, 98, 75, 89, 15,
                    63, 66, 64, 74, 27, 83, 97 };
    int q[] = {63, 63, 86, 63, 78};
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = sizeof(q)/sizeof(q[0]);
    for (int i=0; i<m; i++)
    search(arr, n, q[i])? cout << "Yes "
                        : cout << "No ";    

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement search for an item
// that is searched again and again.
import java.util.*;

class solution
{

// A function to perform sequential search.
static boolean search(int[] arr, int n, int x)
{
    // Linearly search the element
    int res = -1;
    for (int i = 0; i < n; i++)
        if (x == arr[i])
        res = i;

    // If not found
    if (res == -1)
        return false;

    // Shift elements before one position
    int temp = arr[res];
    for (int i = res; i > 0; i--)
        arr[i] = arr[i - 1];

    arr[0] = temp;
    return true;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 12, 25, 36, 85, 98, 75, 89, 15,
                    63, 66, 64, 74, 27, 83, 97 };
    int []q = {63, 63, 86, 63, 78};
    int n = arr.length;
    int m = q.length;
    for (int i=0; i<m; i++)
    {
    if(search(arr, n, q[i]) == true)
        System.out.print("Yes ");
    else
        System.out.print("No ");
    }
}
}
// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python 3 program to implement search for
# an item that is searched again and again.

# A function to perform sequential search.
def search(arr, n, x):

    # Linearly search the element
    res = -1
    for i in range(0, n, 1):
        if (x == arr[i]):
            res = i

    # If not found
    if (res == -1):
        return False

    # Shift elements before
    # one position
    temp = arr[res]
    i = res
    while(i > 0):
        arr[i] = arr[i - 1]
        i -= 1

    arr[0] = temp
    return True

# Driver Code
if __name__ == '__main__':
    arr = [12, 25, 36, 85, 98, 75, 89,
           15, 63, 66, 64, 74, 27, 83, 97]
    q = [63, 63, 86, 63, 78]
    n = len(arr)
    m = len(q)
    for i in range(0, m, 1):
        if(search(arr, n, q[i])):
            print("Yes", end = " ")
        else:
            print("No", end = " ")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement search for an
// item that is searched again and again.
using System;

class GFG
{

// A function to perform sequential search.
static bool search(int[] arr, int n, int x)
{
    // Linearly search the element
    int res = -1;
    for (int i = 0; i < n; i++)
        if (x == arr[i])
        res = i;

    // If not found
    if (res == -1)
        return false;

    // Shift elements before one position
    int temp = arr[res];
    for (int i = res; i > 0; i--)
        arr[i] = arr[i - 1];

    arr[0] = temp;
    return true;
}

// Driver Code
public static void Main()
{
    int[] arr = { 12, 25, 36, 85, 98, 75, 89, 15,
                      63, 66, 64, 74, 27, 83, 97 };
    int[] q = {63, 63, 86, 63, 78};
    int n = arr.Length;
    int m = q.Length;
    for (int i = 0; i < m; i++)
    {
        if(search(arr, n, q[i]) == true)
            Console.Write("Yes ");
        else
            Console.Write("No ");
    }
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement search for an
// item that is searched again and again.

// A function to perform sequential search.
function search($arr, $n, $x)
{
    // Linearly search the element
    $res = -1;
    for ($i = 0; $i < $n; $i++)
        if ($x == $arr[$i])
        $res = $i;

    // If not found
    if ($res == -1)
        return false;

    // Shift elements before one position
    $temp = $arr[$res];
    for ($i = $res; $i > 0; $i--)
        $arr[$i] = $arr[$i - 1];

    $arr[0] = $temp;
    return true;
}

// Driver Code
$arr = array(12, 25, 36, 85, 98, 75, 89, 15,
                 63, 66, 64, 74, 27, 83, 97);
$q = array(63, 63, 86, 63, 78);
$n = sizeof($arr);
$m = sizeof($q);

for ($i = 0; $i < $m; $i++)
    if(search($arr, $n, $q[$i]))
        echo "Yes ";
    else
        echo "No ";    

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// Javascript program to implement search for an item
// that is searched again and again.

// A function to perform sequential search.
function search(arr, n, x)
{
    // Linearly search the element
    let res = -1;
    for (let i = 0; i < n; i++)
        if (x == arr[i])
        res = i;

    // If not found
    if (res == -1)
        return false;

    // Shift elements before one position
    let temp = arr[res];
    for (let i = res; i > 0; i--)
        arr[i] = arr[i - 1];

    arr[0] = temp;
    return true;
}

// Driver Code

    let arr = [ 12, 25, 36, 85, 98, 75, 89, 15,
                    63, 66, 64, 74, 27, 83, 97 ];
    let q = [63, 63, 86, 63, 78];
    let n = arr.length;
    let m = q.length;
    for (let i=0; i<m; i++)
    search(arr, n, q[i])? document.write("Yes ")
                        : document.write("No ");   

   // This code is contributed by _saurabh_jaiswal.                    
</script>
```

**输出:**

```
Yes Yes No Yes No 
```

**进一步思考:**我们可以通过使用链表做得更好。在链表中，将一个项目移到前面可以在 O(1)时间内完成。
最好的解决方案是使用[展开树](https://www.geeksforgeeks.org/splay-tree-set-1-insert/)(一种为此目的设计的数据结构)。显示树平均支持 O(Log n)时间内的插入、搜索和删除操作。另外，splay tree 是一个 BST，所以我们可以按照排序的顺序快速打印元素。