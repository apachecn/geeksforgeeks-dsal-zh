# 检查是否可以从给定数组形成算术级数

> 原文： [https://www.geeksforgeeks.org/check-whether-arithmetic-progression-can-formed-given-array/](https://www.geeksforgeeks.org/check-whether-arithmetic-progression-can-formed-given-array/)

给定`n`个整数的数组。 任务是检查是否可以使用所有给定元素形成算术级数。 如果可能，打印`Yes`，否则打印`No`。

**示例**：

```
Input : arr[] = {0, 12, 4, 8}
Output : Yes
Rearrange given array as {0, 4, 8, 12} 
which forms an arithmetic progression.

Input : arr[] = {12, 40, 11, 20}
Output : No

```



**方法 1（简单）**：

一个简单的解决方案是先找到最小的元素，然后找到第二个最小的元素，然后找出这两者之间的差。 将此差设为`d`。 找到差异后，找到第三最小，第四最小，依此类推。 在找到每第`i`个最小值（从第 3 个开始）之后，找到当前元素的值与前一个元素的值之间的差。 如果差异与`d`不同，则返回`false`。 如果所有元素都相同，则返回`true`。 该解决方案的时间复杂度为 `O(n^2)`。

**方法 2（使用排序）**：

这个想法是对给定的数组进行排序。 排序后，检查连续元素之间的差异是否相同。 如果所有差异都相同，则可以进行算术级数运算。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to check if a given array 
// can form arithmetic progression 
#include<bits/stdc++.h> 
using namespace std; 

// Returns true if a permutation of arr[0..n-1] 
// can form arithmetic progression 
bool checkIsAP(int arr[], int n) 
{ 
  if (n == 1) 
    return true; 

  // Sort array 
  sort(arr, arr + n); 

  // After sorting, difference between 
  // consecutive elements must be same. 
  int d = arr[1] - arr[0]; 
  for (int i=2; i<n; i++) 
    if (arr[i] - arr[i-1] != d) 
      return false; 

  return true; 
} 

// Driven Program 
int main() 
{ 
  int arr[] = { 20, 15, 5, 0, 10 }; 
  int n = sizeof(arr)/sizeof(arr[0]); 

  (checkIsAP(arr, n))? (cout << "Yes" << endl) : 
                       (cout << "No" << endl); 

  return 0; 
} 

```

## Java

```java
// Java program to check if a given array 
// can form arithmetic progression 
import java.util.Arrays; 
  
class GFG { 
          
    // Returns true if a permutation of  
    // arr[0..n-1] can form arithmetic  
    // progression 
    static boolean checkIsAP(int arr[], int n) 
    { 
        if (n == 1) 
            return true; 
          
        // Sort array 
        Arrays.sort(arr); 
          
        // After sorting, difference between 
        // consecutive elements must be same. 
        int d = arr[1] - arr[0]; 
        for (int i = 2; i < n; i++) 
            if (arr[i] - arr[i-1] != d) 
                return false; 
          
        return true; 
    } 
      
    //driver code 
    public static void main (String[] args) 
    { 
        int arr[] = { 20, 15, 5, 0, 10 }; 
        int n = arr.length; 
      
        if(checkIsAP(arr, n)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 program to check if a given  
# array can form arithmetic progression 
  
# Returns true if a permutation of arr[0..n-1] 
# can form arithmetic progression 
def checkIsAP(arr, n): 
    if (n == 1): return True
  
    # Sort array 
    arr.sort() 
  
    # After sorting, difference between 
    # consecutive elements must be same. 
    d = arr[1] - arr[0] 
    for i in range(2, n): 
        if (arr[i] - arr[i-1] != d): 
            return False
  
    return True
  
# Driver code 
arr = [ 20, 15, 5, 0, 10 ] 
n = len(arr) 
print("Yes") if(checkIsAP(arr, n)) else print("No") 
  
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# program to check if a given array 
// can form arithmetic progression 
using System; 
  
class GFG { 
          
    // Returns true if a permutation of  
    // arr[0..n-1] can form arithmetic  
    // progression 
    static bool checkIsAP(int []arr, int n) 
    { 
        if (n == 1) 
            return true; 
          
        // Sort array 
        Array.Sort(arr); 
          
        // After sorting, difference between 
        // consecutive elements must be same. 
        int d = arr[1] - arr[0]; 
        for (int i = 2; i < n; i++) 
            if (arr[i] - arr[i - 1] != d) 
                return false; 
          
        return true; 
    } 
      
    //Driver Code 
    public static void Main () 
    { 
        int []arr = {20, 15, 5, 0, 10}; 
        int n = arr.Length; 
      
        if(checkIsAP(arr, n)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to check if  
// a given array can form 
// arithmetic progression 
  
// Returns true if a permutation  
// of arr[0..n-1] can form  
// arithmetic progression 
function checkIsAP($arr, $n) 
{ 
    if ($n == 1) 
        return true; 
      
    // Sort array 
    sort($arr); 
      
    // After sorting, difference 
    // between consecutive elements 
    // must be same. 
    $d = $arr[1] - $arr[0]; 
    for ($i = 2; $i < $n; $i++) 
        if ($arr[$i] -  
            $arr[$i - 1] != $d) 
        return false; 
      
    return true; 
} 
  
// Driver Code 
$arr = array(20, 15, 5, 0, 10); 
$n = count($arr); 
  
if(checkIsAP($arr, $n)) 
echo "Yes";  
else
echo "No"; 
                          
// This code is contributed  
// by Sam007 
?>
```

输出：

```
Yes
```

时间复杂度：`O(n Log n)`。

方法 3（使用散列）：

1.  找出最小和第二小的元素。
2.  在两个元素之间找到不同。 `d =`第二最小减最小。
3.  将所有元素存储在哈希映射中，如果找到重复的元素，则返回`NO`（可以与步骤 1 一起完成）。
4.  现在从“第二个最小元素`+ d`”开始，然后在哈希映射中逐一检查`n-2`项算术级数。 如果缺少级数值，则返回`false`。
5.  循环结束后返回`YES`。

时间复杂度：`O（n）`。

辅助空间：`O（n）`。

感谢 Chenna Rao 提出了这种方法，

方法 4（使用计数排序）：

如果可以修改给定的数组，我们可以减少方法 3 中所需的空间。

1.  查找最小和第二最小的元素。
2.  找出`d =`第二最小减最小。
3.  从所有元素中减去最小的元素。
4.  现在，如果给定的数组表示 AP，则所有元素都应为`i * d`形式，其中`i`从 0 到`n-1`不等。
5.  用`d`一一除以所有归约元素。 如果任何元素不能被d整除，则返回`false`。
6.  现在，如果数组代表 AP，则它必须是从 0 到`n-1`的数字排列。 我们可以使用计数排序轻松地检查这一点。

