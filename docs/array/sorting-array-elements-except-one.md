# 对除一个以外的所有数组元素进行排序

> 原文： [https://www.geeksforgeeks.org/sorting-array-elements-except-one/](https://www.geeksforgeeks.org/sorting-array-elements-except-one/)

给定正整数数组`A`，请按升序对数组进行排序，以使未排序数组中索引`K`处的元素保持不动，并对所有其他元素进行排序。

**示例**：

```
Input : arr[] = {10, 4, 11, 7, 6, 20}
            k = 2;
Output : arr[] = {4, 6, 11, 7, 10, 20}

Input : arr[] = {30, 20, 10}
         k = 0
Output : arr[] = {30, 10, 20}

```



**简单解决方案**是将除第`k`个给定数组之外的所有元素复制到另一个数组。 然后使用排序算法对另一个数组进行排序。 最后再次将排序后的数组复制到原始数组。 复制时，跳过第`k`个元素。

以下是**有效解决方案**。

1.  将第`k`个元素与最后一个元素交换。

2.  排序除最后一个之外的所有元素。

3.  对于第`k + 1`个元素至最后一个元素，将它们向前移动一个位置。

4.  将第`k`个元素复制回位置`k`。

## C++ 

```cpp

// CPP program to sort all elements except 
// element at index k. 
#include <bits/stdc++.h> 
using namespace std; 

int sortExceptK(int arr[], int k, int n) 
{ 
    // Move k-th element to end 
    swap(arr[k], arr[n-1]); 

    // Sort all elements except last 
    sort(arr, arr + n - 1); 

    // Store last element (originally k-th) 
    int last = arr[n-1]; 

    // Move all elements from k-th to one 
    // position ahead. 
    for (int i=n-1; i>k; i--) 
       arr[i] = arr[i-1]; 

    // Restore k-th element 
    arr[k] = last; 
} 

// Driver code 
int main() 
{ 
    int a[] = {10, 4, 11, 7, 6, 20 }; 
    int k = 2; 
    int n = sizeof(a) / sizeof(a[0]); 
    sortExceptK(a, k, n); 
    for (int i = 0; i < n; i++) 
        cout << a[i] << " "; 
} 

```

## Java

```java

// Java program to sort all elements except 
// element at index k. 
import java.util.Arrays; 

class GFG { 

    static int sortExceptK(int arr[], int k, int n) 
    { 

        // Move k-th element to end 
        int temp = arr[k]; 
        arr[k] = arr[n-1]; 
        arr[n-1] = temp; 

        // Sort all elements except last 
        Arrays.sort(arr, 0, n-1); 

        // Store last element (originally k-th) 
        int last = arr[n-1]; 

        // Move all elements from k-th to one 
        // position ahead. 
        for (int i = n-1; i > k; i--) 
        arr[i] = arr[i-1]; 

        // Restore k-th element 
        arr[k] = last; 
        return 0; 
    } 

    //Driver code 
    public static void main (String[] args) 
    { 
        int a[] = {10, 4, 11, 7, 6, 20 }; 
        int k = 2; 
        int n = a.length; 

        sortExceptK(a, k, n); 

        for (int i = 0; i < n; i++) 
            System.out.print(a[i] + " "); 
    } 
} 

//This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to sort all elements except 
# element at index k. 
def sortExcept(arr, k, n): 

    # Move k-th element to end 
    arr[k], arr[-1] = arr[-1], arr[k] 

    # Sort all elements except last 
    arr = sorted(arr, key = lambda i: (i is arr[-1], i)) 

    # Store last element (originally k-th) 
    last = arr[-1] 

    # Move all elements from k-th to one 
    # position ahead. 
    i = n - 1
    while i > k: 
        arr[i] = arr[i - 1] 
        i -= 1

    # Restore k-th element 
    arr[k] = last 
    return arr 

# Driver code 
if __name__ == '__main__': 
    a = [10, 4, 11, 7, 6, 20] 
    k = 2
    n = len(a) 
    a = sortExcept(a, k, n) 
    print(" ".join(list(map(str, a)))) 

# This code is contributed by Shivam Singh. 

```

## C# 

```cs

// C# program to sort all elements except 
// element at index k. 
using System; 

public class GFG { 

    static int sortExceptK(int[] arr, int k, int n) 
    { 
        // Move k-th element to end 
        int temp = arr[k]; 
        arr[k] = arr[n - 1]; 
        arr[n - 1] = temp; 

        // Sort all elements except last 
        Array.Sort(arr, 0, n - 1); 

        // Store last element (originally k-th) 
        int last = arr[n - 1]; 

        // Move all elements from k-th to one 
        // position ahead. 
        for (int i = n - 1; i > k; i--) 
            arr[i] = arr[i - 1]; 

        // Restore k-th element 
        arr[k] = last; 

        return 0; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] a = { 10, 4, 11, 7, 6, 20 }; 
        int k = 2; 
        int n = a.Length; 

        sortExceptK(a, k, n); 

        for (int i = 0; i < n; i++) 
        Console.Write(a[i] + " "); 
    } 
} 

// This article is contributed by shiv_bhakt 

```

## PHP

```php

<?php 
// PHP program to sort all  
// elements except element 
// at index k. 
function sortExceptK(&$arr, $k, $n) 
{ 
    // Move k-th element to end 
    $t = $arr[$k]; 
    $arr[$k] = $arr[$n - 1]; 
    $arr[$n - 1] = $t; 

    // Sort all elements  
    // except last 
    $t = $arr[count($arr) - 1]; 
    $arr = array_slice($arr, 0, -1); 
    sort($arr); 
    array_push($arr, $t); 

    // Store last element 
    // (originally k-th) 
    $last = $arr[$n - 1]; 

    // Move all elements from  
    // k-th to one position ahead. 
    for ($i = $n - 1; $i > $k; $i--) 
    $arr[$i] = $arr[$i - 1]; 

    // Restore k-th element 
    $arr[$k] = $last; 
} 

// Driver code 
$a = array(10, 4, 11,  
            7, 6, 20 ); 
$k = 2; 
$n = count($a); 
sortExceptK($a, $k, $n); 

for ($i = 0; $i < $n; $i++) 
    echo ($a[$i]." "); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
4 6 11 7 10 20 

```



* * *

* * *



