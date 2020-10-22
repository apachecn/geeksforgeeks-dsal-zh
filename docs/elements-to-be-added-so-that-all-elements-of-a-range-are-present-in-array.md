# 要添加的元素，以便数组中存在某个范围的所有元素

> 原文： [https://www.geeksforgeeks.org/elements-to-be-added-so-that-all-elements-of-a-range-are-present-in-array/](https://www.geeksforgeeks.org/elements-to-be-added-so-that-all-elements-of-a-range-are-present-in-array/)

给定大小为`N`的数组。令`A`和`B`分别为数组中的最小值和最大值。 任务是查找应将给定数组添加多少个数字，以使`[A, B]`范围内的所有元素在数组中至少出现一次。

**示例**：

```
Input : arr[] = {4, 5, 3, 8, 6}
Output : 1
Only 7 to be added in the list.

Input : arr[] = {2, 1, 3}
Output : 0

```



**方法 1（排序）**：

1.  对数组进行排序。

2.  比较`arr[i] == arr[i + 1] - 1`。 如果不是，则更新计数为`arr[i + 1] - arr[i] -1`。

3.  返回计数。

## C++ 

```cpp

// C++ program for above implementation 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count numbers to be added 
int countNum(int arr[], int n) 
{ 
    int count = 0; 

    // Sort the array 
    sort(arr, arr + n); 

    // Check if elements are consecutive 
    //  or not. If not, update count 
    for (int i = 0; i < n - 1; i++) 
        if (arr[i] != arr[i+1] &&  
            arr[i] != arr[i + 1] - 1) 
            count += arr[i + 1] - arr[i] - 1; 

    return count; 
} 

// Drivers code 
int main() 
{ 
    int arr[] = { 3, 5, 8, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << countNum(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java
// java program for above implementation 
import java.io.*; 
import java.util.*; 
  
public class GFG { 
      
    // Function to count numbers to be added 
    static int countNum(int []arr, int n) 
    { 
        int count = 0; 
      
        // Sort the array 
        Arrays.sort(arr); 
      
        // Check if elements are consecutive 
        // or not. If not, update count 
        for (int i = 0; i < n - 1; i++) 
            if (arr[i] != arr[i+1] &&  
                arr[i] != arr[i + 1] - 1) 
                count += arr[i + 1] - arr[i] - 1; 
      
        return count; 
    } 
      
    // Drivers code 
    static public void main (String[] args) 
    { 
          
        int []arr = { 3, 5, 8, 6 }; 
        int n = arr.length; 
          
        System.out.println(countNum(arr, n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```py
# python program for above implementation 
  
# Function to count numbers to be added 
def countNum(arr, n):  
      
    count = 0
  
    # Sort the array 
    arr.sort() 
  
    # Check if elements are consecutive 
    # or not. If not, update count 
    for i in range(0, n-1): 
        if (arr[i] != arr[i+1] and
            arr[i] != arr[i + 1] - 1): 
            count += arr[i + 1] - arr[i] - 1; 
  
    return count 
  
# Drivers code 
arr = [ 3, 5, 8, 6 ] 
n = len(arr) 
print(countNum(arr, n)) 
  
# This code is contributed by Sam007
```

## C#

```cs
// C# program for above implementation 
using System; 
  
public class GFG { 
      
    // Function to count numbers to be added 
    static int countNum(int []arr, int n) 
    { 
        int count = 0; 
      
        // Sort the array 
        Array.Sort(arr); 
      
        // Check if elements are consecutive 
        // or not. If not, update count 
        for (int i = 0; i < n - 1; i++) 
            if (arr[i] != arr[i+1] &&  
                arr[i] != arr[i + 1] - 1) 
                count += arr[i + 1] - arr[i] - 1; 
      
        return count; 
    } 
      
    // Drivers code 
    static public void Main () 
    { 
          
        int []arr = { 3, 5, 8, 6 }; 
        int n = arr.Length; 
          
        Console.WriteLine(countNum(arr, n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program for  
// above implementation 
  
// Function to count  
// numbers to be added 
function countNum($arr, $n) 
{ 
  
    $count = 0; 
  
    // Sort the array 
    sort($arr); 
  
    // Check if elements are  
    // consecutive or not.  
    // If not, update count 
    for ($i = 0; $i < $n - 1; $i++) 
        if ($arr[$i] != $arr[$i + 1] &&  
            $arr[$i] != $arr[$i + 1] - 1) 
            $count += $arr[$i + 1] -  
                      $arr[$i] - 1; 
  
    return $count; 
} 
  
// Driver code 
$arr = array(3, 5, 8, 6); 
$n = count($arr); 
echo countNum($arr, $n) ; 
  
// This code is contributed 
// by anuj_67. 
?>
```

输出：

```
2
```

时间复杂度：`O(n log n)`。

方法 2（使用哈希）：

1.  维护数组元素的哈希。
2.  存储最小和最大元素。
3.  从哈希中的最小到最大元素遍历，并计算元素是否不在哈希中。
4.  返回计数。

## C++

```cpp
// C++ program for above implementation 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to count numbers to be added 
int countNum(int arr[], int n) 
{ 
    unordered_set<int> s; 
    int count = 0, maxm = INT_MIN, minm = INT_MAX; 
  
    // Make a hash of elements 
    // and store minimum and maximum element 
    for (int i = 0; i < n; i++) { 
        s.insert(arr[i]); 
        if (arr[i] < minm) 
            minm = arr[i]; 
        if (arr[i] > maxm) 
            maxm = arr[i]; 
    } 
  
    // Traverse all elements from minimum 
    // to maximum and count if it is not 
    // in the hash 
    for (int i = minm; i <= maxm; i++) 
        if (s.find(arr[i]) == s.end()) 
            count++; 
    return count; 
} 
  
// Drivers code 
int main() 
{ 
    int arr[] = { 3, 5, 8, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << countNum(arr, n) << endl; 
    return 0; 
}
```

## Java

```java
// Java implementation of the approach 
import java.util.HashSet; 
  
class GFG  
{ 
  
// Function to count numbers to be added 
static int countNum(int arr[], int n) 
{ 
    HashSet<Integer> s = new HashSet<>(); 
    int count = 0,  
        maxm = Integer.MIN_VALUE,  
        minm = Integer.MAX_VALUE; 
  
    // Make a hash of elements 
    // and store minimum and maximum element 
    for (int i = 0; i < n; i++)  
    { 
        s.add(arr[i]); 
        if (arr[i] < minm) 
            minm = arr[i]; 
        if (arr[i] > maxm) 
            maxm = arr[i]; 
    } 
  
    // Traverse all elements from minimum 
    // to maximum and count if it is not 
    // in the hash 
    for (int i = minm; i <= maxm; i++) 
        if (!s.contains(i)) 
            count++; 
    return count; 
} 
  
// Drivers code 
public static void main(String[] args)  
{ 
    int arr[] = { 3, 5, 8, 6 }; 
    int n = arr.length; 
    System.out.println(countNum(arr, n)); 
} 
} 
  
// This code is contributed by Rajput-Ji
```

## Python3

```py
# Function to count numbers to be added 
def countNum(arr, n): 
  
    s = dict() 
    count, maxm, minm = 0, -10**9, 10**9
  
    # Make a hash of elements and store  
    # minimum and maximum element 
    for i in range(n): 
        s[arr[i]] = 1
        if (arr[i] < minm): 
            minm = arr[i] 
        if (arr[i] > maxm): 
            maxm = arr[i] 
      
    # Traverse all elements from minimum 
    # to maximum and count if it is not 
    # in the hash 
    for i in range(minm, maxm + 1): 
        if i not in s.keys(): 
            count += 1
    return count 
  
# Driver code 
arr = [3, 5, 8, 6 ] 
n = len(arr) 
print(countNum(arr, n)) 
      
# This code is contributed by mohit kumar
```

## C#

```cs
// C# implementation of the approach 
using System; 
using System.Collections.Generic; 
  
class GFG  
{ 
  
// Function to count numbers to be added 
static int countNum(int []arr, int n) 
{ 
    HashSet<int> s = new HashSet<int>(); 
    int count = 0,  
        maxm = int.MinValue,  
        minm = int.MaxValue; 
  
    // Make a hash of elements 
    // and store minimum and maximum element 
    for (int i = 0; i < n; i++)  
    { 
        s.Add(arr[i]); 
        if (arr[i] < minm) 
            minm = arr[i]; 
        if (arr[i] > maxm) 
            maxm = arr[i]; 
    } 
  
    // Traverse all elements from minimum 
    // to maximum and count if it is not 
    // in the hash 
    for (int i = minm; i <= maxm; i++) 
        if (!s.Contains(i)) 
            count++; 
    return count; 
} 
  
// Drivers code 
public static void Main(String[] args)  
{ 
    int []arr = { 3, 5, 8, 6 }; 
    int n = arr.Length; 
    Console.WriteLine(countNum(arr, n)); 
} 
} 
  
// This code is contributed by Rajput-Ji
```

输出：

```
2
```

时间复杂度：`O(max – min + 1)`。

