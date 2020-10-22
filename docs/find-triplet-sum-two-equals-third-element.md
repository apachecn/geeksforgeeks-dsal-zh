# 找到一个三元组，使得两个和等于第三元素

> 原文： [https://www.geeksforgeeks.org/find-triplet-sum-two-equals-third-element/](https://www.geeksforgeeks.org/find-triplet-sum-two-equals-third-element/)

给定一个整数数组，您必须找到三个数字，以使两个元素的总和等于第三个元素。

**示例**：

```
Input : {5, 32, 1, 7, 10, 50, 19, 21, 2}
Output : 21, 2, 19

Input : {5, 32, 1, 7, 10, 50, 19, 21, 0}
Output : no such triplet exist

```

问题源： [Arcesium 面试经历 | 系列 7（校园实习）](https://www.geeksforgeeks.org/arcesium-interview-experience-set-7-campus-internship/)



**简单方法**：运行三个循环，检查是否存在三元组，以使两个元素的总和等于第三个元素。

**时间复杂度**：`O(n ^ 3)`。

**高效方法**：这个想法类似于[这里](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)。

*   首先对给定的数组进行排序。

*   从后面开始固定三个中的最大元素，并遍历数组以找到其他两个数字，它们合计为第三个元素。

*   取两个指针`j`（从前面开始）和`k`（最初为`i-1`）以找到两个数字中的最小值，并从`i-1`中找到两个剩余数字中的最大值。

*   如果两个数字的和仍小于`A[i]`，则需要增加两个数字之和的值，从而增加`j`指针，从而增加`A[j] + A[k]`的值。

*   如果两个数字的总和大于`A[i]`，则我们需要减小两个数字之和的值，从而减小`k`指针，从而减小`A[j] + A[k]`的值。

下图是上述方法的模拟：

![](img/8998b8458e6a532ef3167166086ec076.png)

下面是上述方法的实现：

## C++ 

```cpp

// CPP program to find three numbers 
// such that sum of two makes the 
// third element in array 
#include <bits/stdc++.h> 
using namespace std; 

// Utility function for finding 
// triplet in array 
void findTriplet(int arr[], int n) 
{ 
    // sort the array 
    sort(arr, arr + n); 

    // for every element in arr 
    // check if a pair exist(in array) whose 
    // sum is equal to arr element 
    for (int i = n - 1; i >= 0; i--) { 
        int j = 0; 
        int k = i - 1; 

        // Iterate forward and backward to find 
        // the other two elements 
        while (j < k) { 

            // If the two elements sum is 
            // equal to the third element 
            if (arr[i] == arr[j] + arr[k]) { 

                // pair found 
                cout << "numbers are " << arr[i] << " "
                     << arr[j] << " " << arr[k] << endl; 
                return; 
            } 

            // If the element is greater than 
            // sum of both the elements, then try 
            // adding a smaller number to reach the 
            // equality 
            else if (arr[i] > arr[j] + arr[k]) 
                j += 1; 

            // If the element is smaller, then 
            // try with a smaller number 
            // to reach equality, so decrease K 
            else
                k -= 1; 
        } 
    } 

    // No such triplet is found in array 
    cout << "No such triplet exists"; 
} 

// driver program 
int main() 
{ 
    int arr[] = { 5, 32, 1, 7, 10, 50, 19, 21, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    findTriplet(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find three numbers 
// such that sum of two makes the 
// third element in array 
import java.util.Arrays; 

public class GFG { 

    // utility function for finding 
    // triplet in array 
    static void findTriplet(int arr[], int n) 
    { 
        // sort the array 
        Arrays.sort(arr); 

        // for every element in arr 
        // check if a pair exist(in array) whose 
        // sum is equal to arr element 
        for (int i = n - 1; i >= 0; i--) { 
            int j = 0; 
            int k = i - 1; 
            while (j < k) { 
                if (arr[i] == arr[j] + arr[k]) { 

                    // pair found 
                    System.out.println("numbers are " + arr[i] + " "
                                       + arr[j] + " " + arr[k]); 

                    return; 
                } 
                else if (arr[i] > arr[j] + arr[k]) 
                    j += 1; 
                else
                    k -= 1; 
            } 
        } 

        // no such triplet is found in array 
        System.out.println("No such triplet exists"); 
    } 

    // driver program 
    public static void main(String args[]) 
    { 
        int arr[] = { 5, 32, 1, 7, 10, 50, 19, 21, 2 }; 
        int n = arr.length; 
        findTriplet(arr, n); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python

```py

# Python program to find three numbers 
# such that sum of two makes the 
# third element in array 

# utility function for finding 
# triplet in array 
def findTriplet(arr, n): 

    # sort the array 
    arr.sort() 

    # for every element in arr 
    # check if a pair exist(in array) whose 
    # sum is equal to arr element 
    i = n - 1
    while(i >= 0): 
        j = 0
        k = i - 1
        while (j < k): 
            if (arr[i] == arr[j] + arr[k]): 

                # pair found 
                print "numbers are ", arr[i], arr[j], arr[k] 
                return
            elif (arr[i] > arr[j] + arr[k]): 
                j += 1
            else: 
                k -= 1
        i -= 1

    # no such triplet is found in array 
    print "No such triplet exists"

# driver program 
arr = [ 5, 32, 1, 7, 10, 50, 19, 21, 2 ] 
n = len(arr) 
findTriplet(arr, n) 

# This code is contributed by Sachin Bisht 

```

## C# 

```cs

// C# program to find three numbers 
// such that sum of two makes the 
// third element in array 
using System; 

public class GFG { 

    // utility function for finding 
    // triplet in array 
    static void findTriplet(int[] arr, int n) 
    { 

        // sort the array 
        Array.Sort(arr); 

        // for every element in arr 
        // check if a pair exist(in 
        // array) whose sum is equal 
        // to arr element 
        for (int i = n - 1; i >= 0; i--) { 
            int j = 0; 
            int k = i - 1; 
            while (j < k) { 
                if (arr[i] == arr[j] + arr[k]) { 

                    // pair found 
                    Console.WriteLine("numbers are "
                                      + arr[i] + " " + arr[j] 
                                      + " " + arr[k]); 

                    return; 
                } 
                else if (arr[i] > arr[j] + arr[k]) 
                    j += 1; 
                else
                    k -= 1; 
            } 
        } 

        // no such triplet is found in array 
        Console.WriteLine("No such triplet exists"); 
    } 

    // driver program 
    public static void Main() 
    { 
        int[] arr = { 5, 32, 1, 7, 10, 50, 
                      19, 21, 2 }; 
        int n = arr.Length; 

        findTriplet(arr, n); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find three 
// numbers such that sum of  
// two makes the third 
// element in array 

// utility function for  
// finding triplet in array 
function findTriplet($arr, $n) 
{ 
    // sort the array 
    sort($arr); 

    // for every element in  
    // arr check if a pair  
    // exist(in array) whose 
    // sum is equal to arr element 
    for ($i = $n - 1; $i >= 0; $i--) 
    { 
        $j = 0; 
        $k = $i - 1; 
        while ($j < $k)  
        { 
            if ($arr[$i] == $arr[$j] + $arr[$k])  
            { 

                // pair found 
                echo "numbers are ", $arr[$i], " ",  
                                      $arr[$j], " ",  
                                      $arr[$k]; 
                return; 
            }  
            else if ($arr[$i] > $arr[$j] +  
                                $arr[$k]) 
                $j += 1; 
            else
                $k -= 1; 
        } 
    } 

    // no such triplet  
    // is found in array 
    echo "No such triplet exists"; 
} 

// Driver Code 
$arr = array(5, 32, 1, 7, 10,  
             50, 19, 21, 2 ); 
$n = count($arr); 

findTriplet($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
numbers are 21 2 19

```

**时间复杂度**：`O(N ^ 2)`。



