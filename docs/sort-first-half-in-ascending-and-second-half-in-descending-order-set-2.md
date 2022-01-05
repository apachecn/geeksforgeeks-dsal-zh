# 前半部分按升序排序，后半部分按降序排序|设置 2

> 原文:[https://www . geesforgeks . org/sort-升序前半部分和降序后半部分-set-2/](https://www.geeksforgeeks.org/sort-first-half-in-ascending-and-second-half-in-descending-order-set-2/)

给定一个整数数组，将数组的前半部分按升序排序，后半部分按降序排序。

**示例:**

```
Input : arr[] = {10, 20, 30, 40}
Output : arr[] = {10, 20, 40, 30}

Input : arr[] = {5, 4, 6, 2, 1, 3, 8, 9, 7 }
Output : arr[] = {2, 4, 5, 6, 9, 8, 7, 3, 1 }
```

我们已经讨论了一个解决方案，它只在[中打印所需的顺序，前半部分按升序排序，后半部分按降序排序|设置 1](https://www.geeksforgeeks.org/sort-first-half-in-ascending-and-second-half-in-descending-order/)

**Simple Approach**
思路很简单，我们用库函数把前半部分按照递增的顺序排序，后半部分按照递减的顺序排序。像 Java、C++这样的大多数语言都提供了按指定顺序对子数组进行排序的功能。在这篇文章中，讨论了一个不同的解决方案，它修改了原始数组。

## C++

```
// C++ program to sort first half in increasing
// order and second half in decreasing
#include<bits/stdc++.h>
using namespace std;

void mySort(int arr[], int n)
{
    sort(arr, arr+n/2);
    sort(arr+n/2, arr+n, greater<int>());
}

int main()
{
    int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
    int n = sizeof(arr)/sizeof(arr[0]);
    mySort(arr, n);
    cout << "Modified Array : \n";
    for (int i=0; i<n; i++)
       cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort first half in increasing
// order and second half in decreasing
import java.util.*;

public class SortExample {
    static void mySort(Integer[] arr)
    {
        int n = arr.length;

        // Sort subarray from index 1 to 4, i.e.,
        // only sort subarray {7, 6, 45, 21} and
        // keep other elements as it is.
        Arrays.sort(arr, 0, n / 2);
        Arrays.sort(arr, n / 2, n, Collections.reverseOrder());
    }

    public static void main(String[] args)
    {
        // Our arr contains 8 elements
        Integer[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
        mySort(arr);
        System.out.printf("Modified arr[] : %s",
                          Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to sort first half in increasing
# order and second half in decreasing

# required sorting function
def mySort( arr, n):

    arr1 = arr[:n//2]
    arr2 = arr[n//2:]
    arr1.sort()
    arr2.sort(reverse=True)
    return arr1+arr2

# driving function
if __name__=='__main__':
    arr= [5, 4, 6, 2, 1, 3, 8, 9, 7 ]
    n = len(arr)
    arr=mySort(arr, n)
    print( "Modified Array : ")
    print(arr)

# this code is contributed by ash264
```

## C#

```
// C# program to sort first half in increasing
// order and second half in decreasing
using System;

public class SortExample
{
    static void mySort(int[] arr)
    {
        int n = arr.Length;

        // Sort subarray from index 1 to 4, i.e.,
        // only sort subarray {7, 6, 45, 21} and
        // keep other elements as it is.
        Array.Sort(arr, 0, n / 2);
        Array.Sort(arr, n / 2, (n/2)+1);
        Array.Reverse(arr, n / 2, (n/2)+1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Our arr contains 8 elements
        int[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
        mySort(arr);
        Console.Write("Modified arr[] : {0}",
                        String.Join(" ",arr));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort first half in increasing
// order and second half in decreasing

function mySort(&$arr, $n)
{
    $array1 = array_slice($arr, 0,
                    floor($n / 2));
    $array2 = array_slice($arr, $n / 2);
    sort($array1);
    rsort($array2);
    $arr = array_merge($array1, $array2);
}

// Driver Code
$arr = array(5, 4, 6, 2, 1, 3, 8, 9, 7);
$n = sizeof($arr);
mySort($arr, $n);

echo "Modified array :\n";
for($i = 0; $i < $n; $i++)
    echo $arr[$i] . " ";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to sort
// first half in increasing
// order and second half in decreasing

    function mySort(arr)
    {
        let n = arr.length;

        // Sort subarray from index 1 to 4, i.e.,
        // only sort subarray {7, 6, 45, 21} and
        // keep other elements as it is.

        let arr1=arr.slice(0,Math.floor(n/2)).
        sort(function(a,b){return a-b;});
        let arr2=arr.slice(Math.floor(n/2),
        Math.floor(n/2)+n).sort(function(a,b)
        {return b-a;})
        return arr1.concat(arr2)
    }

    // Our arr contains 8 elements
    let arr=[5, 4, 6, 2, 1, 3, 8, 9, 7];
    arr=mySort(arr);
    document.write("Modified arr : <br>"+arr.join(" "));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Modified array :
2 4 5 6 9 8 7 3 1 
```

**交替解**
1)将整个数组按升序排序。
2)分拣后反转后半部分。

## C++

```
// C++ program to sort first half in increasing
// order and second half in decreasing
#include<bits/stdc++.h>
using namespace std;

void mySort(int arr[], int n)
{
    // Sort the first half
    sort(arr, arr+n/2);
    sort(arr+n/2, arr+n);

    reverse(arr+n/2, arr+n);
}

int main()
{
    int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
    int n = sizeof(arr)/sizeof(arr[0]);
    mySort(arr, n);
    cout << "Modified Array : \n";
    for (int i=0; i<n; i++)
       cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort first half in increasing
// order and second half in decreasing
import java.util.*;

public class SortExample {
    static void mySort(Integer[] arr)
    {
        int n = arr.length;

        // Sort the whole array
        Arrays.sort(arr, 0, n/2);
        Arrays.sort(arr, n/2, n);

        // Reverse the second half
        int low = n/2, high = n-1;
        while (low < high)
        {
            Integer temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++; high--;
        } 
    }

    public static void main(String[] args)
    {
        // Our arr contains 8 elements
        Integer[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
        mySort(arr);
        System.out.printf("Modified arr[] : %s",
                          Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to sort first half in increasing
# order and second half in decreasing
def mySort(arr):
    n = len(arr);

    # Sort the whole array
    arr1 = arr[:n // 2]
    arr2 = arr[n // 2:]
    arr1.sort()
    arr2.sort()
    arr = arr1 + arr2

    # Reverse the second half
    low = n // 2;
    high = n - 1;
    while (low < high):
        temp = arr[low];
        arr[low] = arr[high];
        arr[high] = temp;
        low += 1;
        high -= 1;
    return arr;

# Driver code
if __name__ == '__main__':

    # Our arr contains 8 elements
    arr = [5, 4, 6, 2, 1, 3, 8, 9, 7];
    arr = mySort(arr);
    print("Modified Array : ")
    print(arr)

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to sort first half in increasing
// order and second half in decreasing
using System;

public class SortExample
{
    static void mySort(int[] arr)
    {
        int n = arr.Length;

        // Sort the whole array
        Array.Sort(arr, 0, n/2);
        Array.Sort(arr, n/2, n/2+1);

        // Reverse the second half
        int low = n/2, high = n-1;
        while (low < high)
        {
            int temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++; high--;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Our arr contains 8 elements
        int[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
        mySort(arr);
        Console.WriteLine("Modified arr[] : {0}",
                        String.Join(", ",arr));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to sort first half in increasing
// order and second half in decreasing

    function mySort(arr)
    {
        let n = arr.length;

         // Sort the whole array  
        let arr1=arr.slice(0,Math.floor(n/2)).sort(function(a,b){return a-b;});
        let arr2=arr.slice(Math.floor(n/2),n).sort(function(a,b){return a-b;});
        arr=arr1.concat(arr2);

        // Reverse the second half
        let low = Math.floor(n/2), high = n-1;
        while (low < high)
        {
            let temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++; high--;
        }
        return arr;
    }

    let arr=[5, 4, 6, 2, 1, 3, 8, 9, 7 ];
    arr=mySort(arr);
    document.write("Modified arr : "+arr.join(" "));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Modified arr[] : [2, 4, 5, 6, 9, 8, 7, 3, 1]
```

两种方法的时间复杂度均为 0(n ^ Log n)