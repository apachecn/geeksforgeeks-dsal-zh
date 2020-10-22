# 查找最小正整数值，它不能表示为给定数组的任何子集之和

> 原文： [https://www.geeksforgeeks.org/find-smallest-value-represented-sum-subset-given-array/](https://www.geeksforgeeks.org/find-smallest-value-represented-sum-subset-given-array/)

给定一个带正数的排序数组（以非降序排列），找到不能表示为给定集合的任何子集的元素之和的最小正整数值。

预期时间复杂度为`O(n)`。

例子：

```
Input:  arr[] = {1, 3, 6, 10, 11, 15};
Output: 2

Input:  arr[] = {1, 1, 1, 1};
Output: 5

Input:  arr[] = {1, 1, 3, 4};
Output: 10

Input:  arr[] = {1, 2, 5, 10, 20, 40};
Output: 4

Input:  arr[] = {1, 2, 3, 4, 5, 6};
Output: 22

```



**简单解决方案**是从值 1 开始，并逐一检查所有值是否可以求和到给定数组中的值。 该解决方案效率很低，因为它简化为[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)，这是众所周知的 [NP 完全问题](https://www.geeksforgeeks.org/np-completeness-set-1/)。

我们可以使用一个简单的循环在`O(n)`时间中解决此问题。 令输入数组为`arr[0..n-1]`。 我们将结果初始化为 1（最小可能的结果）并遍历给定的数组。 让无法用索引 0 到`i-1`的元素表示的最小元素为`res`，当我们考虑索引`i`的元素时，有以下两种可能性：

1.  **我们认为`res`是最终结果**：如果`arr[i]`大于`res`，则我们发现差距为`res`，因为`arr[i]`之后的元素也将大于`res`。

2.  **考虑了`arr[i]`之后，`res`的值增加**：`res`的值增加`arr[i]`（为什么？如果从 0 到`i-1`的元素可以表示 1 到`res-1`，然后从 0 到`i`的元素可以表示从 1 到`res + arr [i] – 1`，将`arr[i]`加到表示 1 到`res`的所有子集中）

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to find the smallest positive value that cannot be 
// represented as sum of subsets of a given sorted array 
#include <bits/stdc++.h> 
using namespace std; 

// Returns the smallest number that cannot be represented as sum 
// of subset of elements from set represented by sorted array arr[0..n-1] 
int findSmallest(int arr[], int n) 
{ 
   int res = 1; // Initialize result 

   // Traverse the array and increment 'res' if arr[i] is 
   // smaller than or equal to 'res'. 
   for (int i = 0; i < n && arr[i] <= res; i++) 
       res = res + arr[i]; 

   return res; 
} 

// Driver program to test above function 
int main() 
{ 
   int arr1[] = {1, 3, 4, 5}; 
   int n1 = sizeof(arr1)/sizeof(arr1[0]); 
   cout << findSmallest(arr1, n1) << endl; 

   int arr2[] = {1, 2, 6, 10, 11, 15}; 
   int n2 = sizeof(arr2)/sizeof(arr2[0]); 
   cout << findSmallest(arr2, n2) << endl; 

   int arr3[] = {1, 1, 1, 1}; 
   int n3 = sizeof(arr3)/sizeof(arr3[0]); 
   cout << findSmallest(arr3, n3) << endl; 

   int arr4[] = {1, 1, 3, 4}; 
   int n4 = sizeof(arr4)/sizeof(arr4[0]); 
   cout << findSmallest(arr4, n4) << endl; 

   return 0; 
} 

```

## Java

```java
// Java program to find the smallest positive value that cannot be 
// represented as sum of subsets of a given sorted array 
class FindSmallestInteger  
{ 
    // Returns the smallest number that cannot be represented as sum 
    // of subset of elements from set represented by sorted array arr[0..n-1] 
    int findSmallest(int arr[], int n)  
    { 
        int res = 1; // Initialize result 
  
        // Traverse the array and increment 'res' if arr[i] is 
        // smaller than or equal to 'res'. 
        for (int i = 0; i < n && arr[i] <= res; i++) 
            res = res + arr[i]; 
  
        return res; 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args)  
    { 
        FindSmallestInteger small = new FindSmallestInteger(); 
        int arr1[] = {1, 3, 4, 5}; 
        int n1 = arr1.length; 
        System.out.println(small.findSmallest(arr1, n1)); 
  
        int arr2[] = {1, 2, 6, 10, 11, 15}; 
        int n2 = arr2.length; 
        System.out.println(small.findSmallest(arr2, n2)); 
  
        int arr3[] = {1, 1, 1, 1}; 
        int n3 = arr3.length; 
        System.out.println(small.findSmallest(arr3, n3)); 
  
        int arr4[] = {1, 1, 3, 4}; 
        int n4 = arr4.length; 
        System.out.println(small.findSmallest(arr4, n4)); 
  
    } 
} 
  
// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## Python3

```py
# Python3 program to find the smallest 
# positive value that cannot be 
# represented as sum of subsets  
# of a given sorted array 
  
# Returns the smallest number  
# that cannot be represented as sum 
# of subset of elements from set 
# represented by sorted array arr[0..n-1] 
def findSmallest(arr, n): 
  
    res = 1 #Initialize result 
  
    # Traverse the array and increment 
    # 'res' if arr[i] is smaller than 
    # or equal to 'res'. 
    for i in range (0, n ): 
        if arr[i] <= res: 
            res = res + arr[i] 
        else: 
            break
    return res 
  
  
# Driver program to test above function 
arr1 = [1, 3, 4, 5] 
n1 = len(arr1) 
print(findSmallest(arr1, n1)) 
  
arr2= [1, 2, 6, 10, 11, 15] 
n2 = len(arr2) 
print(findSmallest(arr2, n2)) 
  
arr3= [1, 1, 1, 1] 
n3 = len(arr3) 
print(findSmallest(arr3, n3)) 
  
arr4 = [1, 1, 3, 4] 
n4 = len(arr4) 
print(findSmallest(arr4, n4)) 
  
# This code is.contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find the smallest 
// positive value that cannot be 
// represented as sum of subsets  
// of a given sorted array 
using System; 
  
class GFG { 
      
    // Returns the smallest number that 
    // cannot be represented as sum 
    // of subset of elements from set  
    // represented by sorted array 
    // arr[0..n-1] 
    static int findSmallest(int []arr, int n)  
    { 
         // Initialize result 
         int res = 1; 
  
        // Traverse the array and  
        // increment 'res' if arr[i] is 
        // smaller than or equal to 'res'. 
        for (int i = 0; i < n &&  
             arr[i] <= res; i++) 
            res = res + arr[i]; 
  
        return res; 
    } 
  
    // Driver code 
    public static void Main()  
    { 
        int []arr1 = {1, 3, 4, 5}; 
        int n1 = arr1.Length; 
        Console.WriteLine(findSmallest(arr1, n1)); 
  
        int []arr2 = {1, 2, 6, 10, 11, 15}; 
        int n2 = arr2.Length; 
        Console.WriteLine(findSmallest(arr2, n2)); 
  
        int []arr3 = {1, 1, 1, 1}; 
        int n3 = arr3.Length; 
        Console.WriteLine(findSmallest(arr3, n3)); 
  
        int []arr4 = {1, 1, 3, 4}; 
        int n4 = arr4.Length; 
        Console.WriteLine(findSmallest(arr4, n4)); 
  
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find the smallest 
// positive value that cannot be 
// represented as sum of subsets 
// of a given sorted array 
  
// Returns the smallest number that 
// cannot be represented as sum of  
// subset of elements from set 
// represented by sorted array  
// arr[0..n-1] 
function findSmallest($arr, $n) 
{ 
      
    // Initialize result 
    $res = 1;  
      
    // Traverse the array and  
    // increment 'res' if arr[i] is 
    // smaller than or equal to 'res'. 
    for($i = 0; $i < $n and $arr[$i] <= $res; $i++) 
        $res = $res + $arr[$i]; 
      
    return $res; 
} 
  
// Driver Code 
$arr1 = array(1, 3, 4, 5); 
$n1 = count($arr1); 
echo findSmallest($arr1, $n1),"\n"; 
  
$arr2 = array(1, 2, 6, 10, 11, 15); 
$n2 = count($arr2); 
echo findSmallest($arr2, $n2),"\n" ; 
  
$arr3 = array(1, 1, 1, 1); 
$n3 = count($arr3); 
echo findSmallest($arr3, $n3),"\n"; 
  
$arr4 = array(1, 1, 3, 4); 
$n4 = count($arr4); 
echo findSmallest($arr4, $n4); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
2
4
5
10
```

上述程序的时间复杂度为`O(n)`。