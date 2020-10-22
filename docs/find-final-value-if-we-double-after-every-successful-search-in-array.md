# 如果我们在数组中每次成功搜索后加倍，查找最终值

> 原文： [https://www.geeksforgeeks.org/find-final-value-if-we-double-after-every-successful-search-in-array/](https://www.geeksforgeeks.org/find-final-value-if-we-double-after-every-successful-search-in-array/)

给定一个数组和一个整数`k`，遍历该数组，如果数组中的元素为`k`，则将`k`的值加倍并继续遍历。 最后返回`k`值。

例子：

```
Input : arr[] = { 2, 3, 4, 10, 8, 1 }, k = 2
Output :16
First k = 2 is found, then we search for 4
which is also found, then we search for 8
which is also found, then we search for 16.

Input : arr[] = { 2, 4, 5, 6, 7 }, k = 3
Output :3

```



1.  如果`arr [i] == k`则遍历数组的每个元素，然后`k = 2 * k`

2.  重复相同的过程直到数组的最后一个元素

3.  最后返回`k`的值

## C++ 

```cpp

// CPP program to find value if we double  
// the value after every successful search 
#include <bits/stdc++.h> 
using namespace std; 

// Function to Find the value of k 
int findValue(int arr[], int n, int k) { 

  // Search for k. After every successful 
  // search, double k. 
  for (int i = 0; i < n; i++)  
    if (arr[i] == k) 
      k *= 2; 

  return k; 
} 

// Driver's Code 
int main() { 
  int arr[] = {2, 3, 4, 10, 8, 1}, k = 2; 
  int n = sizeof(arr) / sizeof(arr[0]); 
  cout << findValue(arr, n, k); 
  return 0; 
} 

```

## Java

```java
// Java program to find value  
// if we double  the value after  
// every successful search 
  
class GFG 
{ 
    // Function to Find the value of k 
    static int findValue(int arr[], int n, int k) { 
      
    // Search for k. After every successful 
    // search, double k. 
    for (int i = 0; i < n; i++)  
        if (arr[i] == k) 
        k *= 2; 
      
    return k; 
    } 
  
    // Driver Code 
    public static void main(String[] args)  
    { 
    int arr[] = {2, 3, 4, 10, 8, 1}, k = 2; 
    int n = arr.length; 
    System.out.print(findValue(arr, n, k)); 
    } 
} 
// This code is contriubted by 
// Smitha Dinesh Semwal
```

## Python3

```py
# Python program to find 
# value if we double  
# the value after every 
# successful search 
  
# Function to Find the value of k 
def findValue(arr,n,k): 
   
    # Search for k. 
    # After every successful 
    # search, double k. 
    for i in range(n):  
        if (arr[i] == k): 
            k =k* 2
     
    return k 
  
# Driver's Code 
  
arr = [2, 3, 4, 10, 8, 1] 
k = 2
n = len(arr) 
  
print(findValue(arr, n, k)) 
    
# This code is contributed 
# by Anant Agarwal.
```

## C#

```cs
// C# program to find value  
// if we double the value after  
// every successful search 
using System; 
  
class GFG { 
      
    // Function to Find the value of k 
    static int findValue(int []arr, int n, int k) { 
      
        // Search for k. After every successful 
        // search, double k. 
        for (int i = 0; i < n; i++)  
            if (arr[i] == k) 
                k *= 2; 
          
        return k; 
    } 
  
    // Driver Code 
    public static void Main()  
    { 
        int []arr = {2, 3, 4, 10, 8, 1}; 
        int k = 2; 
        int n = arr.Length; 
          
        Console.WriteLine(findValue(arr, n, k)); 
    } 
} 
  
// This code is contriubted by vt_m.
```

## PHP

```php
<?php 
// PHP program to find  
// value if we double  
// the value after every  
// successful search 
  
// Function to Find  
// the value of k 
function findValue($arr, $n, $k)  
{ 
  
    // Search for k. After every  
    // successful search, double k. 
    for ($i = 0; $i < $n; $i++)  
        if ($arr[$i] == $k) 
        $k *= 2; 
      
    return $k; 
} 
  
// Driver Code 
$arr = array(2, 3, 4, 10, 8, 1);  
$k = 2; 
$n = count($arr); 
echo findValue($arr, $n, $k); 
  
// This code is contriubted by anuj_67. 
?>
```

输出：

```
Output: 16 
```

时间复杂度：`O(n)`。

参考：

<https://www.geeksforgeeks.org/flipkart-interview-experience-set-35-on-campus-for-sde-1/>

