# 最大化`arr [i] * i`的总和

> 原文： [https://www.geeksforgeeks.org/maximize-sum-arrii/](https://www.geeksforgeeks.org/maximize-sum-arrii/)

给定`N`个整数的数组。 您可以重新排列数组的元素。 任务是找到`Σarr[i] * i`的最大值，其中`i = 0, 1, 2, …, n – 1`。

例子：

```
Input : N = 4, arr[] = { 3, 5, 6, 1 }
Output : 31
If we arrange arr[] as { 1, 3, 5, 6 }. 
Sum of arr[i]*i is 1*0 + 3*1 + 5*2 + 6*3 
= 31, which is maximum

Input : N = 2, arr[] = { 19, 20 }
Output : 20

```



**简单解决方案**是[生成给定数组的所有排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)。 对于每个排列，计算`Σarr[i] * i`的值，最后返回最大值。

**有效解决方案**基于以下事实：应将最大值缩放为最大值，将最小值缩放为最小值。 因此，我们将`i`的最小值乘以`arr[i]`的最小值。 因此，以升序对给定的数组进行排序，并计算`ari * i`的总和，其中`i = 0`至`n-1`。

以下是此方法的实现：

## C++ 

```cpp

// CPP program to find the maximum value 
// of i*arr[i] 
#include<bits/stdc++.h> 
using namespace std; 

int maxSum(int arr[], int n) 
{   
  // Sort the array 
  sort(arr, arr + n); 

  // Finding the sum of arr[i]*i 
  int sum = 0; 
  for (int i = 0; i < n; i++) 
    sum += (arr[i]*i); 

  return sum; 
} 

// Driven Program 
int main() 
{ 
  int arr[] = { 3, 5, 6, 1 }; 
  int n = sizeof(arr)/sizeof(arr[0]); 

  cout << maxSum(arr, n) << endl; 
  return 0; 
}  

```

## Java

```java
// Java program to find the 
// maximum value of i*arr[i] 
import java.util.*; 
  
class GFG { 
  
    static int maxSum(int arr[], int n) 
    {     
    // Sort the array 
    Arrays.sort(arr); 
  
    // Finding the sum of arr[i]*i 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        sum += (arr[i] * i); 
  
    return sum; 
    } 
  
    // Driven Program 
    public static void main(String[] args) 
    { 
    int arr[] = { 3, 5, 6, 1 }; 
    int n = arr.length; 
  
    System.out.println(maxSum(arr, n)); 
  
    } 
} 
// This code is contributed by Prerna Saini
```

## Python3

```py
# Python program to find the 
# maximum value of i*arr[i] 
def maxSum(arr,n): 
  
    #  Sort the array 
    arr.sort() 
  
    # Finding the sum of  
    # arr[i]*i 
    sum = 0
    for i in range(n): 
        sum += arr[i] * i 
          
    return sum
  
# Driver Program 
arr = [3,5,6,1] 
n = len(arr) 
print(maxSum(arr,n)) 
  
# This code is contributed 
# by Shrikant13
```

## C#

```cs
// C# program to find the 
// maximum value of i*arr[i] 
using System; 
  
class GFG { 
      
    // Function to find the 
    // maximum value of i*arr[i] 
    static int maxSum(int[] arr, int n) 
    {  
          
        // Sort the array 
        Array.Sort(arr); 
      
        // Finding the sum of arr[i]*i 
        int sum = 0; 
        for (int i = 0; i < n; i++) 
            sum += (arr[i] * i); 
      
        return sum; 
    } 
  
    // Driver code 
    static public void Main() 
    { 
        int[] arr = {3, 5, 6, 1}; 
        int n = arr.Length; 
      
        Console.WriteLine(maxSum(arr, n)); 
  
    } 
} 
  
// This code is contributed by Ajit.
```

## PHP

```php
<?php 
// PHP program to find the  
// maximum value of i*arr[i] 
  
// function returns the  
// maximum value of i*arr[i] 
function maxSum($arr, $n) 
{  
    // Sort the array 
    sort($arr); 
      
    // Finding the sum  
    // of arr[i]*i 
    $sum = 0; 
    for ($i = 0; $i < $n; $i++) 
        $sum += ($arr[$i] * $i); 
      
    return $sum; 
} 
  
// Driver Code 
$arr = array( 3, 5, 6, 1 ); 
$n = count($arr); 
  
echo maxSum($arr, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
31
```

时间复杂度：`O(n Log n)`。

