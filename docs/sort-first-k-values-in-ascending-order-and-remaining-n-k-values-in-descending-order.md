# 按照升序对前 k 个值进行排序，按照降序对剩余的 n-k 个值进行排序

> 原文:[https://www . geeksforgeeks . org/sort-first-k-values-in-升序-restrict-n-k-values-in-降序/](https://www.geeksforgeeks.org/sort-first-k-values-in-ascending-order-and-remaining-n-k-values-in-descending-order/)

给定一个大小为 n 的数组，按升序排列数组的前 k 个元素，按降序排列剩余的 n-k 个元素。

**示例:**

> **输入:** arr[] = {5，4，6，2，1，3，8，9，-1}，k = 4
> **输出:** 2 4 5 6 9 8 3 1 -1
> 
> **输入:** arr[] = {5，4，6}，k = 2
> **输出:** 4 5 6

**算法:**

1.  将前 k 个元素存储在数组中，并按升序排序。
2.  将剩余的 n-k 个元素存储在一个数组中，并按降序排序。
3.  通过以相反的顺序添加第二个数组中的元素来合并两个数组。

## C++

```
// C++ program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
#include <bits/stdc++.h>
using namespace std;

// Function to sort the array
void printOrder(int arr[], int n, int k)
{
    int len1 = k, len2 = n - k;
    int arr1[k], arr2[n - k];

    // Store the k elements in an array
    for (int i = 0; i < k; i++)
        arr1[i] = arr[i];

    // Store the remaining n-k elements in an array
    for (int i = k; i < n; i++)
        arr2[i - k] = arr[i];

    // sorting the array from 0 to k-1 places
    sort(arr1, arr1 + len1);

    // sorting the array from k to n places
    sort(arr2, arr2 + len2);

    // storing the values in the final array arr
    for (int i = 0; i < n; i++) {
        if (i < k)
            arr[i] = arr1[i];

        else {
            arr[i] = arr2[len2 - 1];
            len2--;
        }
    }
    // printing the array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, -1 };
    int k = 4;

    int n = sizeof(arr) / sizeof(arr[0]);

    printOrder(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
import java.util.*;

class GFG {
    // function to print half of the array in
    // ascending order and the other half in
    // descending order
    static void printOrder(int[] arr, int n, int k)
    {
        int len1 = k, len2 = n - k;
        int[] arr1 = new int[k];
        int[] arr2 = new int[n - k];

        // Store the k elements in an array
        for (int i = 0; i < k; i++)
            arr1[i] = arr[i];

        // Store the remaining n-k elements in an array
        for (int i = k; i < n; i++)
            arr2[i - k] = arr[i];

        // sorting the array from 0 to k-1 places
        Arrays.sort(arr1, 0, k);

        // sorting the array from k to n places
        Arrays.sort(arr2, k, n - k);

        // storing the values in the final array arr
        for (int i = 0; i < n; i++) {
            if (i < k)
                arr[i] = arr1[i];

            else {
                arr[i] = arr2[len2 - 1];
                len2--;
            }
        }
        // printing the array
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, -1 };
        int k = 4;
        int n = arr.length;
        printOrder(arr, n, k);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to sort first
# k elements in increasing order
# and remaining n-k elements in
# decreasing

# Function to sort the array
def printOrder(arr, n, k):

    len1 = k
    len2 = n - k
    arr1 = [0] * k
    arr2 = [0] * (n - k)

    # Store the k elements
    # in an array
    for i in range(k):
        arr1[i] = arr[i]

    # Store the remaining n-k
    # elements in an array
    for i in range(k, n):
        arr2[i - k] = arr[i]

    # sorting the array from
    # 0 to k-1 places
    arr1.sort()

    # sorting the array from
    # k to n places
    arr2.sort()

    # storing the values in the
    # final array arr
    for i in range(n):
        if (i < k):
            arr[i] = arr1[i]

        else :
            arr[i] = arr2[len2 - 1]
            len2 -= 1

    # printing the array
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__":
    arr = [ 5, 4, 6, 2, 1,
            3, 8, 9, -1 ]
    k = 4

    n = len(arr)

    printOrder(arr, n, k)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
using System;

class GFG {
    // function to print half of the array in
    // ascending order and the other half in
    // descending order
    static void printOrder(int[] arr,
                           int n, int k)
    {
        int len2 = n - k;
        int[] arr1 = new int[k];
        int[] arr2 = new int[n - k];

        // Store the k elements in an array
        for (int i = 0; i < k; i++)
            arr1[i] = arr[i];

        // Store the remaining n-k
        // elements in an array
        for (int i = k; i < n; i++)
            arr2[i - k] = arr[i];

        // sorting the array from
        // 0 to k-1 places
        Array.Sort(arr1, 0, k);

        // sorting the array from k to n places
        Array.Sort(arr2, 0, n - k);

        // storing the values in
        // the final array arr
        for (int i = 0; i < n; i++) {
            if (i < k)
                arr[i] = arr1[i];

            else {
                arr[i] = arr2[len2 - 1];
                len2--;
            }
        }

        // printing the array
        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 5, 4, 6, 2, 1,
                      3, 8, 9, -1 };
        int k = 4;
        int n = arr.Length;
        printOrder(arr, n, k);
    }
}

// This code is contributed by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort first
// k elements in increasing order
// and remaining n-k elements in
// decreasing

// Function to sort the array
function printOrder($arr, $n, $k)
{
    $len1 = $k;
    $len2 = $n - $k;
    $arr1 = array_fill(0, $k, 0);
    $arr2 = array_fill(0, ($n - $k), 0);

    // Store the k elements
    // in an array
    for ($i = 0; $i < $k; $i++)
        $arr1[$i] = $arr[$i];

    // Store the remaining n-k
    // elements in an array
    for ($i = $k; $i < $n; $i++)
        $arr2[$i - $k] = $arr[$i];

    // sorting the array from
    // 0 to k-1 places
    sort($arr1);

    // sorting the array from
    // k to n places
    sort($arr2);

    // storing the values in the
    // final array arr
    for ($i = 0; $i < $n; $i++)
        if ($i < $k)
            $arr[$i] = $arr1[$i];

        else
        {
            $arr[$i] = $arr2[$len2 - 1];
            $len2 -= 1;
    }

    // printing the array
    for ($i = 0; $i < $n; $i++)
        print($arr[$i] . " ");
}

// Driver code
$arr = array( 5, 4, 6, 2, 1, 3, 8, 9, -1 );
$k = 4;

$n = count($arr);

printOrder($arr, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing   

// Function to print half of the array in
// ascending order and the other half in
// descending order
function printOrder(arr, n, k)
{
    let len1 = k, len2 = n - k;
    let arr1 = new Array(k);
    let arr2 = new Array(n - k);

    // Store the k elements in an array
    for(let i = 0; i < k; i++)
        arr1[i] = arr[i];

    // Store the remaining n-k
    // elements in an array
    for(let i = k; i < n; i++)
        arr2[i - k] = arr[i];

    // Sorting the array from 0 to k-1 places
     arr1.sort(function(a, b){return a - b;});

    // Sorting the array from k to n places
     arr2.sort(function(a, b){return a - b;});

    // Storing the values in the final array arr
    for(let i = 0; i < n; i++)
    {
        if (i < k)
            arr[i] = arr1[i];
        else
        {
            arr[i] = arr2[len2 - 1];
            len2--;
        }
    }

    // Printing the array
    for(let i = 0; i < n; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Driver code
let arr = [ 5, 4, 6, 2, 1, 3, 8, 9, -1 ];
let k = 4;
let n = arr.length;

printOrder(arr, n, k);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2 4 5 6 9 8 3 1 -1
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*

**高效途径:**思路简单，利用库函数将前 k 个元素按递增顺序排序，剩余 n-k 个元素按递减顺序排序。

## C++

```
// C++ program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
#include <bits/stdc++.h>
using namespace std;

// function to sort the array
void printOrder(int arr[], int n, int k)
{
    // Sort first k elements in ascending order
    sort(arr, arr + k);

    // Sort remaining n-k elements in descending order
    sort(arr + k, arr + n, greater<int>());
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, -1 };
    int k = 4;
    int n = sizeof(arr) / sizeof(arr[0]);

    printOrder(arr, n, k);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
import java.util.*;

public class SortExample {
    static void printOrder(Integer[] arr, int k)
    {
        int n = arr.length;

        // Sort first k elements in ascending order
        Arrays.sort(arr, 0, k);

        // Sort remaining n-k elements in descending order
        Arrays.sort(arr, k, n, Collections.reverseOrder());
    }

    public static void main(String[] args)
    {
        // Our arr contains 8 elements
        Integer[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, -1 };
        int k = 4;
        printOrder(arr, k);
        System.out.printf("%s", Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to sort first k elements
# in increasing order and remaining
# n-k elements in decreasing

# function to sort the array
def printOrder(arr, n, k):

    # Sort first k elements in ascending order
    a = arr[0:k];
    a.sort();

    # Sort remaining n-k elements in descending order
    b = arr[k:n];
    b.sort();
    b.reverse();
    return a + b;

# Driver code
arr = [ 5, 4, 6, 2, 1, 3, 8, 9, -1 ];
k = 4;
n = len(arr);

arr = printOrder(arr, n, k);

for i in range(n):
    print(arr[i], end =" ");

# This code is contributed by mits
```

## C#

```
// C# program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
using System;

public class SortExample {
    static void printOrder(int[] arr, int k)
    {
        int n = arr.Length;

        // Sort first k elements in ascending order
        Array.Sort(arr, 0, k);

        // Sort remaining n-k elements in descending order
        Array.Sort(arr, k, n - k);
        Array.Reverse(arr, k, n - k);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Our arr contains 8 elements
        int[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, -1 };
        int k = 4;
        printOrder(arr, k);
        Console.Write("{0}", String.Join(" ", arr));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing

// function to sort the array
function printOrder($arr, $n, $k)
{
    // Sort first k elements in ascending order
    $a= array_slice($arr, 0, $k);
    sort($a);

    // Sort remaining n-k elements in descending order
    $b = array_slice($arr, $k, $n);
    sort($b);
    $b = array_reverse($b);
    unset($arr);
    $arr = $a;
    return array_merge($arr, $b);
}

    // Driver code
    $arr = array( 5, 4, 6, 2, 1, 3, 8, 9, -1 );
    $k = 4;
    $n = count($arr);

    $arr=printOrder($arr, $n, $k);

    for ($i = 0; $i < $n; $i++)
        echo $arr[$i]." ";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to sort first k elements
// in increasing order and remaining
// n-k elements in decreasing
function printOrder(arr, k)
{
    let n = arr.length;

    // Sort first k elements in ascending order
    // Sort remaining n-k elements in descending order
    arr = arr.slice(0, k).sort(
        function(a, b){return a - b;}).concat(
        arr.slice(k, n).sort(function(a, b){return b - a;}));

    return arr;
}

// Driver code

// Our arr contains 8 elements
let arr = [ 5, 4, 6, 2, 1, 3, 8, 9, -1 ];
let k = 4;
arr = printOrder(arr, k);

document.write(arr.join(" "));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2 4 5 6 9 8 3 1 -1
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*