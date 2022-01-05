# 在给定的索引范围内对数组进行排序

> 原文:[https://www . geeksforgeeks . org/给定索引范围内的排序数组/](https://www.geeksforgeeks.org/sort-the-array-in-a-given-index-range/)

给定一个由 **N** 个整数组成的数组**arr【】**和一个索引范围**【a，b】**。任务是在给定的索引范围内对数组进行排序，即将数组中的元素从**arr【a】**排序到**arr【b】**，同时保持其他元素的位置不变，并打印修改后的数组。
**注:**a 和 **b** 之间没有关系，即 **a** 可以小于、等于或大于 **b** 。另外， **0 ≤ a，b < N**

**示例:**

> **输入:** arr[] = {7，8，4，5，2}，a = 1，b = 4
> **输出:** 7 2 4 5 8
> 对于索引范围【1，4】我们得到元素 8，4，5 和 2
> 在对这些元素进行排序时，我们得到 2，4，5 和 8。
> 所以数组修改为{7，2，4，5，8}
> 
> **输入:** arr[] = {20，10，3，8}，a = 3，b = 1
> **输出:** 20 3 8 10

**进场:**

1.  为数组的给定索引范围创建元素的临时数组。
2.  对这个临时数组进行排序。
3.  现在用给定索引范围的临时数组的这些排序元素修改原始数组。

下面是上述方法的实现:

## C++

```
// C++ program to sort the
// array in a given index range

#include <bits/stdc++.h>
using namespace std;

// Function to sort the elements of the array
// from index a to index b
void partSort(int arr[], int N, int a, int b)
{
    // Variables to store start and
    // end of the index range
    int l = min(a, b);
    int r = max(a, b);

    // Temporary array
    int temp[r - l + 1];
    int j = 0;
    for (int i = l; i <= r; i++) {
        temp[j] = arr[i];
        j++;
    }

    // Sort the temporary array
    sort(temp, temp + r - l + 1);

    // Modifying original array with
    // temporary array elements
    j = 0;
    for (int i = l; i <= r; i++) {
            arr[i] = temp[j];
            j++;
    }

    // Print the modified array
    for (int i = 0; i < N; i++) {
            cout << arr[i] << " " ;
        }

}

// Driver code
int main()
{
    int arr[] = { 7, 8, 4, 5, 2 } ;
    int a = 1 ;
    int b = 4;

    // length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    partSort(arr, N, a, b);
    return 0;
}
// This code is contributed by Ryuga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort the array in a given index range
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // Function to sort the elements of the array
    // from index a to index b
    static void partSort(int[] arr, int N, int a, int b)
    {
        // Variables to store start and end of the index range
        int l = Math.min(a, b);
        int r = Math.max(a, b);

        // Temporary array
        int[] temp = new int[r - l + 1];
        int j = 0;
        for (int i = l; i <= r; i++) {
            temp[j] = arr[i];
            j++;
        }

        // Sort the temporary array
        Arrays.sort(temp);

        // Modifying original array with temporary array elements
        j = 0;
        for (int i = l; i <= r; i++) {
            arr[i] = temp[j];
            j++;
        }

        // Print the modified array
        for (int i = 0; i < N; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int[] arr = { 7, 8, 4, 5, 2 };
        int a = 1, b = 4;

        // length of the array
        int N = arr.length;

        partSort(arr, N, a, b);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to sort the
# array in a given index range

# Function to sort the elements of
# the array from index a to index b
def partSort(arr, N, a, b):

    # Variables to store start and
    # end of the index range
    l = min(a, b)
    r = max(a, b)

    # Temporary array
    temp = [0 for i in range(r - l + 1)]
    j = 0
    for i in range(l, r + 1, 1):
        temp[j] = arr[i]
        j += 1

    # Sort the temporary array
    temp.sort(reverse = False)

    # Modifying original array with
    # temporary array elements
    j = 0
    for i in range(l, r + 1, 1):
            arr[i] = temp[j]
            j += 1

    # Print the modified array
    for i in range(0, N, 1):
            print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [7, 8, 4, 5, 2]
    a = 1
    b = 4

    # length of the array
    N = len(arr)

    partSort(arr, N, a, b)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to sort the array in a given index range
using System;
class GFG {

    // Function to sort the elements of the array
    // from index a to index b
    static void partSort(int[] arr, int N, int a, int b)
    {
        // Variables to store start and end of the index range
        int l = Math.Min(a, b);
        int r = Math.Max(a, b);

        // Temporary array
        int[] temp = new int[r - l + 1];
        int j = 0;
        for (int i = l; i <= r; i++) {
            temp[j] = arr[i];
            j++;
        }

        // Sort the temporary array
        Array.Sort(temp);

        // Modifying original array with temporary array elements
        j = 0;
        for (int i = l; i <= r; i++) {
            arr[i] = temp[j];
            j++;
        }

        // Print the modified array
        for (int i = 0; i < N; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 7, 8, 4, 5, 2 };
        int a = 1, b = 4;

        // length of the array
        int N = arr.Length;

        partSort(arr, N, a, b);
    }
}
// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
# PHP program to sort the
# array in a given index range

// Function to sort the elements of the array
// from index a to index b
function partSort( $arr, $N, $a, $b)
{
    // Variables to store start and
    // end of the index range
    $l = min($a, $b);
     $r = max($a, $b);

    // Temporary array
    $temp = array();
    $j = 0;
    for ($i = $l; $i <= $r; $i++) {
        $temp[$j] = $arr[$i];
        $j++;
    }

    // Sort the temporary array
    sort($temp);

    // Modifying original array with
    // temporary array elements
    $j = 0;
    for ($i = $l; $i <= $r; $i++) {
            $arr[$i] = $temp[$j];
            $j++;
    }

    // Print the modified array
    for ($i = 0; $i < $N; $i++) {
            echo $arr[$i]." " ;
        }

}

    $arr = array( 7, 8, 4, 5, 2 ) ;
    $a = 1 ;
    $b = 4;

    // length of the array
    $N = count($arr);

    partSort($arr, $N, $a, $b);
    //This code is contributed by 29AjayKumar
    ?>
```

## java 描述语言

```
<script>
    // Javascript program to sort the array in a given index range

    // Function to sort the elements of the array
    // from index a to index b
    function partSort(arr, N, a, b)
    {
        // Variables to store start and end of the index range
        let l = Math.min(a, b);
        let r = Math.max(a, b);

        // Temporary array
        let temp = new Array(r - l + 1);
        temp.fill(0);
        let j = 0;
        for (let i = l; i <= r; i++) {
            temp[j] = arr[i];
            j++;
        }

        // Sort the temporary array
        temp.sort(function(a, b){return a - b});

        // Modifying original array with temporary array elements
        j = 0;
        for (let i = l; i <= r; i++) {
            arr[i] = temp[j];
            j++;
        }

        // Print the modified array
        for (let i = 0; i < N; i++) {
            document.write(arr[i] + " ");
        }
    }

    let arr = [ 7, 8, 4, 5, 2 ];
    let a = 1, b = 4;

    // length of the array
    let N = arr.length;

    partSort(arr, N, a, b);

</script>
```

**Output:** 

```
7 2 4 5 8
```

下面是使用[数组的直接解决方案](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)

## C++

```
// C++ program to sort the array in a given index range
#include<bits/stdc++.h>
using namespace std;

    // Function to sort the elements of the array
    // from index a to index b
    void partSort(int arr[], int N, int a, int b)
    {
        // Variables to store start and end
        // of the index range
        int l = min(a, b);
        int r = max(a, b);

        vector<int> v(arr, arr + N);

        // Sort the subarray from arr[l] to
        // arr[r]
        sort(v.begin() + l, v.begin() + r + 1);

        // Print the modified array
        for (int i = 0; i < N; i++)
            cout << v[i] << " ";
    }

    // Driver code
    int main()
    {
        int arr[] = { 7, 8, 4, 5, 2 };
        int a = 1, b = 4;
        int N = sizeof(arr)/sizeof(arr[0]);
        partSort(arr, N, a, b);
    }

// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort the array in a given index range
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // Function to sort the elements of the array
    // from index a to index b
    static void partSort(int[] arr, int N, int a, int b)
    {
        // Variables to store start and end
        // of the index range
        int l = Math.min(a, b);
        int r = Math.max(a, b);

        // Sort the subarray from arr[l] to
        // arr[r]
        Arrays.sort(arr, l, r + 1);

        // Print the modified array
        for (int i = 0; i < N; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int[] arr = { 7, 8, 4, 5, 2 };
        int a = 1, b = 4;
        int N = arr.length;
        partSort(arr, N, a, b);
    }
}
```

## 蟒蛇 3

```
# Python3 program to sort the
# array in a given index range

# Function to sort the elements of
# the array from index a to index b
def partSort(arr, N, a, b):

    # Variables to store start and
    # end of the index range
    l = min(a, b)
    r = max(a, b)

    arr = (arr[0 : l] +
    sorted(arr[l : r + 1]) +
           arr[r : N])

    # Print the modified array
    for i in range(0, N, 1):
            print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':

    arr = [ 7, 8, 4, 5, 2 ]
    a = 1
    b = 4

    # Length of the array
    N = len(arr)

    partSort(arr, N, a, b)

# This code is contributed by grand_master
```

## C#

```
// C# program to sort the array in a given index range
using System;

class GFG {

    // Function to sort the elements of the array
    // from index a to index b
    static void partSort(int[] arr, int N, int a, int b)
    {
        // Variables to store start and end
        // of the index range
        int l = Math.Min(a, b);
        int r = Math.Max(a, b);

        // Sort the subarray from arr[l] to
        // arr[r]
        Array.Sort(arr, l, r);

        // Print the modified array
        for (int i = 0; i < N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    static void Main()
    {
        int[] arr = { 7, 8, 4, 5, 2 };
        int a = 1, b = 4;
        int N = arr.Length;
        partSort(arr, N, a, b);
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// javascript program to sort the array in a given index range
// Function to sort the elements of the array
// from index a to index b
function swap(arr, xp, yp)
{
    var temp = arr[xp];
    arr[xp] = arr[yp];
    arr[yp] = temp;
}
    function partSort(arr , N , a , b)
    {

        // Variables to store start and end
        // of the index range
        var l = Math.min(a, b);
        var r = Math.max(a, b);

        // Sort the subarray from arr[l] to
        // arr[r]
        //.sort(arr, l, r + 1);
        var i, j;
        for (i = l; i < r + 1 + 1; i++)
        {
            for (j = l; j < r - i + 1; j++)
            {
        if (arr[j] > arr[j + 1])
        {
        swap(arr, j, j + 1);

        }
    }

}

        // Print the modified array
        for (i = 0; i < N; i++)
            document.write(arr[i] + " ");
    }

    // Driver code
        var arr = [ 7, 8, 4, 5, 2 ];
        var a = 1, b = 4;
        var N = arr.length;
        partSort(arr, N, a, b);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
7 2 4 5 8
```