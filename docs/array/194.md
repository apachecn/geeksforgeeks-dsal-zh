# 对包含 1 到`n`个值的数组进行排序

> 原文： [https://www.geeksforgeeks.org/sort-array-contain-1-n-values/](https://www.geeksforgeeks.org/sort-array-contain-1-n-values/)

您给定了一个包含 1 到`n`个元素的数组，您的任务是以一种有效的方式对该数组进行排序，而无需替换为 1 到`n`个数字。

**示例**：

```
Input : arr[] = {10, 7, 9, 2, 8, 
                 3, 5, 4, 6, 1};
Output : 1 2 3 4 5 6 7 8 9 10

```



**本机方法**：

使用任何类型的排序方法对该数组进行排序。 最少需要`O(nLogn)`时间。

**高效方法**：

将每个元素替换为其位置。 它需要`O(n)`有效时间，并为您提供排序后的数组。 让我们通过下面的代码了解这种方法。

## C++ 

```cpp

// Efficient C++ program to sort an array of 
// numbers in range from 1 to n. 
#include <bits/stdc++.h> 

using namespace std; 

// function for sort array 
void sortit(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) { 
      arr[i]=i+1; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 10, 7, 9, 2, 8, 3, 5, 4, 6, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // for sort an array 
    sortit(arr, n); 

    // for print all the element in sorted way 
    for (int i = 0; i < n; i++)  
        cout << arr[i] << " ";     
} 

```

## Java

```java

// Efficient Java program to sort an  
// array of numbers in range from 1 
// to n. 
import java.io.*; 
import java.util.*; 

public class GFG { 

    // function for sort array 
    static void sortit(int []arr, int n) 
    { 
        for (int i = 0; i < n; i++)  
        { 
            arr[i]=i+1; 

        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int []arr = {10, 7, 9, 2, 8,  
                            3, 5, 4, 6, 1}; 
        int n = arr.length; 

        // for sort an array 
        sortit(arr, n); 

        // for print all the  
        // element in sorted way 
        for (int i = 0; i < n; i++)  
            System.out.print(arr[i] + " ");  
    } 
} 

// This code is contributed by Manish Shaw  
// (manishshaw1) 

```

## Python3

```py

# Python3 program to sort an array of  
# numbers in range from 1 to n.  

# function for sort array  
def sortit(arr,n): 
    for i in range(n): 
        arr[i] = i+1

# Driver code 
if __name__=='__main__': 
    arr = [10, 7, 9, 2, 8, 3, 5, 4, 6, 1 ] 
    n = len(arr) 

    # for sort an array  
    sortit(arr,n) 

    # for print all the element  
    # in sorted way  
    for i in range(n): 
        print(arr[i],end=" ") 

# This code is contributed by  
# Shrikant13  

```

## C# 

```cs

// Efficient C# program to sort an array of 
// numbers in range from 1 to n. 
using System; 
using System.Collections.Generic; 

class GFG { 

    // function for sort array 
    static void sortit(int []arr, int n) 
    { 
        for (int i = 0; i < n; i++)  
        { 

            arr[i]=i+1; 
        } 
    } 

    // Driver code 
    public static void Main() 
    { 
        int []arr = {10, 7, 9, 2, 8,  
                      3, 5, 4, 6, 1}; 
        int n = arr.Length; 

        // for sort an array 
        sortit(arr, n); 

        // for print all the  
        // element in sorted way 
        for (int i = 0; i < n; i++)  
            Console.Write(arr[i] + " ");  
    } 
} 

// This code is contributed by  
// Manish Shaw (manishshaw1) 

```

## PHP

```php

<?php 
// Efficient PHP program to sort an  
// array of numbers in range from 1 to n. 

// function for sort array 
function sortit(&$arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++)  
    { 

        $arr[$i]=$i+1;   
    } 
} 

// Driver code 
$arr = array(10, 7, 9, 2, 8,  
             3, 5, 4, 6, 1); 
$n = count($arr); 

// for sort an array 
sortit($arr, $n); 

// for print all the 
// element in sorted way 
for ($i = 0; $i < $n; $i++)  
    echo $arr[$i]." "; 

//This code is contributed by Manish Shaw 
//(manishshaw1) 
?> 

```

**输出**：

```
1 2 3 4 5 6 7 8 9 10

```



* * *

* * *



