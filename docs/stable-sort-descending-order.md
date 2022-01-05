# 降序稳定排序

> 原文:[https://www.geeksforgeeks.org/stable-sort-descending-order/](https://www.geeksforgeeks.org/stable-sort-descending-order/)

给定一个由 n 个整数组成的数组，我们必须对数组元素进行反向排序，以便排序后相等的键是稳定的。
**例:**

```
Input : arr[] = {4, 2, 3, 2, 4}
Output : 4, 4, 3, 2, 2
```

前提:[排序算法中的稳定性](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)
**方法 1(编写自己的排序函数:** [**冒泡排序**](https://www.geeksforgeeks.org/bubble-sort/) **)**
我们知道像[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)[插入排序](https://www.geeksforgeeks.org/insertion-sort/)[合并排序](https://www.geeksforgeeks.org/merge-sort/)[计数排序](https://www.geeksforgeeks.org/counting-sort/)这样的排序算法是稳定的。我们在这里实现冒泡排序。
**解释**
**第一遍**
(4′、2′、3、2″、4″)->(2′、4′、3、4″、2″)这里算法比较最后两个元素和
交换自 2″ < 4″。
(2′、4′、3、4″、2″)->(2′、4′、4″、3、2″)交换自 3<4″
(2′、4′、4″、3、2″)->(2′、4′、4″、3、2″)
(2′、4′、4″、3、2″)->(4′、2′
**第二遍:**
(4′、2′、4″、3、2″)->(4′、2′、4″、3、2″)
(4′、2′、4″、3、2″)->(4′、2′、4″、3、2″)
(4′、2′、4″、3、2″)->(4′、4″ 2′，2″)交换自 2′<3
现在，数组按排序顺序排列，并且相同的元素与原始数组中的元素顺序相同。

## C++

```
// Bubble sort implementation to sort
// elements in descending order.
#include <iostream>
#include <vector>
using namespace std;

void print(vector<int> a, int n)
{
    for (int i = 0; i <= n; i++)
        cout << a[i] << " ";   
    cout << endl;
}

// Sorts a[] in descending order using
// bubble sort.
void sort(vector<int> a, int n)
{
    for (int i = n; i >= 0; i--)
        for (int j = n; j > n - i; j--)
            if (a[j] > a[j - 1])
                swap(a[j], a[j-1]);
    print(a, n);
}

// Driver code
int main()
{
    int n = 7;
    vector<int> a;
    a.push_back(2);
    a.push_back(4);
    a.push_back(3);
    a.push_back(2);
    a.push_back(4);
    a.push_back(5);
    a.push_back(3);
    sort(a, n - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Bubble sort implementation
// to sort elements in
// descending order.
import java.io.*;
import java.util.*;

class GFG
{
static void print(ArrayList<Integer> a,
                                 int n)
{
    for (int i = 0; i <= n; i++)
        System.out.print(a.get(i) + " ");
    System.out.println();
}

// Sorts a[] in descending
// order using bubble sort.
static void sort(ArrayList<Integer> a,
                                  int n)
{
    for (int i = n;
            i >= 0; i--)
        for (int j = n;
                j > n - i; j--)
            if (a.get(j) > a.get(j - 1))
            {
                int tempswap = a.get(j);
                a.remove(j);
                a.add(j, a.get(j - 1));
                a.remove(j - 1);
                a.add(j - 1, tempswap);
            }
    print(a, n);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    ArrayList<Integer> a = new ArrayList<Integer>();
    a.add(2);
    a.add(4);
    a.add(3);
    a.add(2);
    a.add(4);
    a.add(5);
    a.add(3);
    sort(a, n);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Bubble sort implementation to sort
# elements in descending order.

def print1(a, n):

    for i in range(0,n+1):
        print(a[i],end=" ")
    print("")

# Sorts a[] in descending order using
# bubble sort.
def sort(a, n):

    for i in range(n,0,-1):
        for j in range(n, n - i,-1):
            if (a[j] > a[j - 1]):
                a[j], a[j-1]=a[j-1], a[j]
    print1(a,n)

# Driver code
n = 7
a = [2,4,3,2,4,5,3]

sort(a, n-1)

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// Bubble sort implementation
// to sort elements in
// descending order.
using System;
using System.Collections.Generic;

class GFG
{
static void print(List<int> a,
                       int n)
{
    for (int i = 0; i <= n; i++)
        Console.Write(a[i] + " ");
    Console.WriteLine();
}

// Sorts a[] in descending
// order using bubble sort.
static void sort(List<int> a,
                      int n)
{
    for (int i = n;
             i >= 0; i--)
        for (int j = n;
                 j > n - i; j--)
            if (a[j] > a[j - 1])
            {
                int tempswap = a[j];
                a[j] = a[j - 1];
                a[j - 1] = tempswap;
            }
    print(a, n);
}

// Driver code
static void Main()
{
    int n = 6;
    List<int> a = new List<int>();
    a.Add(2);
    a.Add(4);
    a.Add(3);
    a.Add(2);
    a.Add(4);
    a.Add(5);
    a.Add(3);
    sort(a, n);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Bubble sort implementation
// to sort elements in
// descending order.

function swap(&$x, &$y)
{
    $x ^= $y ^= $x ^= $y;
}

function print1($a, $n)
{
    for ($i = 0; $i <= $n; $i++)
        echo ($a[$i] . " ");
    echo ("\n");
}

// Sorts a[] in descending
// order using bubble sort.
function sort1($a, $n)
{
    for ($i = $n;
         $i >= 0; $i--)
    {
        for ($j = $n;
             $j > $n - $i; $j--)
        {
            if ($a[$j] > $a[$j - 1])
                swap($a[$j],
                     $a[$j - 1]);
        }
    }
    print1($a, $n);
}

// Driver code
$n = 6;
$a = array();
array_push($a, 2);
array_push($a, 4);
array_push($a, 3);
array_push($a, 2);
array_push($a, 4);
array_push($a, 5);
array_push($a, 3);
sort1($a, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Bubble sort implementation
// to sort elements in
// descending order.

function print(a,n)
{
       for (let i = 0; i <= n; i++)
        document.write(a[i] + " ");
    document.write("<br>");
}

// Sorts a[] in descending
// order using bubble sort.
function sort(a,n)
{   
    for (let i = n;
            i >= 0; i--)
        for (let j = n;
                j > n - i; j--)
            if (a[j] > a[j-1]){
                let tempswap = a[j];
                a[j] = a[j - 1];
                a[j - 1] = tempswap;
            }
    print(a, n);

}

// Driver code
let n = 6;
let a=[];
a.push(2);
a.push(4);
a.push(3);
a.push(2);
a.push(4);
a.push(5);
a.push(3);
sort(a, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
5 4 4 3 3 2 2
```

**方法二(使用库函数)**
我们可以使用 [stable_sort](https://www.geeksforgeeks.org/stable_sort-c-stl/) 对元素进行稳定排序。

## C++

```
// C++ program to demonstrate descending order
// stable sort using greater<>().
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    stable_sort(arr, arr + n, greater<int>());

    cout << "Array after sorting : \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate descending order
// stable sort using greater<>().
import java.util.*;

class GFG
{
    static void reverse(int a[])
    {
        int i, k, n = a.length;
        int t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
        int n = arr.length;

        Arrays.sort(arr);
        reverse(arr);

        System.out.println("Array after sorting : \n");
        for (int i = 0; i < n; ++i)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to demonstrate
# descending order

if __name__ == "__main__":

    arr = [ 1, 5, 8, 9, 6,
            7, 3, 4, 2, 0 ]
    n = len(arr)

    arr.sort(reverse = True)

    print("Array after sorting : ")
    for i in range(n):
        print(arr[i], end = " ")

# This code is contributed by ita_c
```

## C#

```
// C# program to demonstrate descending order
using System;

class GFG
{
    static void reverse(int []a)
    {
        int i, k, n = a.Length;
        int t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
        int n = arr.Length;

        Array.Sort(arr);
        reverse(arr);

        Console.WriteLine("Array after sorting : \n");
        for (int i = 0; i < n; ++i)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to demonstrate descending order

    function reverse(a)
    {
        var i, k, n = a.length;
        var t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code

        var arr = [ 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 ] ;
        var n = arr.length;

        arr.sort();
        reverse(arr);

        document.write("Array after sorting : " + "<br>");
        for (var i = 0; i < n; ++i)
        {
            document.write(arr[i] + " ");
        }

        // This code is contributed by bunnyram19.
        </script>
```

**输出:**

```
Array after sorting : 
9 8 7 6 5 4 3 2 1 0 
```