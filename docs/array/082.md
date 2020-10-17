# 查找数组中至少有两个大元素的所有元素

> 原文： [https://www.geeksforgeeks.org/find-elements-array-least-two-greater-elements/](https://www.geeksforgeeks.org/find-elements-array-least-two-greater-elements/)

给定`n`个不同元素的数组，任务是查找数组中所有元素至少比其大两个元素。

**示例**：

```
Input : arr[] = {2, 8, 7, 1, 5};
Output : 2  1  5  
The output three elements have two or
more greater elements

Input  : arr[] = {7, -2, 3, 4, 9, -1};
Output : -2  3  4 -1  

```



**方法 1（简单）**：

朴素的方法是运行两个循环并逐个检查数组元素，以检查数组元素至少有两个大于其自身的元素。 如果为`true`，则打印数组元素。

## C++ 

```cpp

// Simple C++ program to find 
// all elements in array which  
// have at-least two greater  
// elements itself. 
#include<bits/stdc++.h> 
using namespace std; 

void findElements(int arr[], int n) 
{ 
    // Pick elements one by one and  
    // count greater elements. If  
    // count is more than 2, print  
    // that element. 
    for (int i = 0; i < n; i++) 
    { 
        int count = 0; 
        for (int j = 0; j < n; j++) 
            if (arr[j] > arr[i]) 
                count++; 

        if (count >= 2) 
            cout << arr[i] << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 2, -6 ,3 , 5, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findElements(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find all  
// elements in array which  
// have at-least two greater 
// elements itself. 
import java.util.*; 
import java.io.*; 
  
class GFG 
{ 
      
static void findElements(int arr[],  
                            int n) 
{ 
    // Pick elements one by one  
    // and count greater elements.  
    // If count is more than 2,  
    // print that element. 
    for (int i = 0; i < n; i++) 
    { 
        int count = 0; 
          
        for (int j = 0; j < n; j++) 
            if (arr[j] > arr[i]) 
                count++; 
  
        if (count >= 2) 
        System.out.print(arr[i] + " "); 
    } 
} 
  
// Driver code 
public static void main(String args[]) 
{ 
    int arr[] = { 2, -6 ,3 , 5, 1}; 
    int n = arr.length; 
    findElements(arr, n); 
} 
} 
  
// This code is contributed by Sahil_Bansall 
```

## Python3

```py
# Python3 program to find 
# all elements in array 
# which have at-least two 
# greater elements itself. 
  
def findElements( arr, n): 
  
    # Pick elements one by 
        # one and count greater 
    # elements. If count 
        # is more than 2, print 
    # that element. 
  
    for i in range(n): 
        count = 0
        for j in range(0, n): 
            if arr[j] > arr[i]: 
                count = count + 1
                  
                  
                  
        if count >= 2 : 
            print(arr[i], end=" ") 
              
  
# Driver code 
arr = [ 2, -6 ,3 , 5, 1] 
n = len(arr) 
findElements(arr, n) 
      
# This code is contributed by sunnysingh 
```

## C#

```cs
// C# program to find all elements in 
// array which have at least two greater 
// elements itself. 
using System; 
  
class GFG 
{ 
      
static void findElements(int []arr, int n) 
{ 
    // Pick elements one by one and count  
    // greater elements. If count is more  
    // than 2, print that element. 
    for (int i = 0; i < n; i++) 
    { 
        int count = 0; 
          
        for (int j = 0; j < n; j++) 
            if (arr[j] > arr[i]) 
                count++; 
  
        if (count >= 2) 
    Console.Write(arr[i] + " "); 
    } 
} 
  
// Driver code 
public static void Main(String []args) 
{ 
    int []arr = {2, -6 ,3 , 5, 1}; 
    int n = arr.Length; 
    findElements(arr, n); 
  
} 
} 
  
// This code is contributed by Parashar. 
```

## PHP

```php
<?php 
// Simple PHP program to find  
// all elements in array which 
// have at-least two greater 
// elements itself. 
  
function findElements($arr, $n) 
{ 
    // Pick elements one by one and 
    // count greater elements. If  
    // count is more than 2,  
    // print that element. 
    for ($i = 0; $i < $n; $i++) 
    { 
        $count = 0; 
        for ($j = 0; $j < $n; $j++) 
            if ($arr[$j] > $arr[$i]) 
                $count++; 
  
        if ($count >= 2) 
            echo $arr[$i]." "; 
    } 
} 
  
// Driver code 
$arr = array( 2, -6 ,3 , 5, 1); 
$n = sizeof($arr); 
findElements($arr, $n); 
  
?> 
```

方法 2（使用排序）：

我们首先以递增顺序对数组进行排序，然后打印第`n-2`个元素，其中`n`是数组的大小。

## C++

```cpp
// Sorting based C++ program to  
// find all elements in array  
// which have atleast two greater  
// elements itself. 
#include<bits/stdc++.h> 
using namespace std; 
  
void findElements(int arr[], int n) 
{ 
    sort(arr, arr + n); 
  
    for (int i = 0; i < n - 2; i++) 
    cout << arr[i] << " "; 
} 
  
// Driver Code 
int main() 
{ 
    int arr[] = { 2, -6 ,3 , 5, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findElements(arr, n); 
    return 0; 
} 
```

## Java

```java
// Sorting based Java program to find  
// all elements in array which have  
// atleast two greater elements itself. 
import java.util.*; 
import java.io.*; 
  
class GFG 
{ 
  
static void findElements(int arr[], int n) 
{ 
    Arrays.sort(arr); 
  
    for (int i = 0; i < n - 2; i++) 
    System.out.print(arr[i] + " "); 
} 
  
// Driver code 
public static void main(String args[]) 
{ 
    int arr[] = { 2, -6 ,3 , 5, 1}; 
    int n = arr.length; 
    findElements(arr, n); 
  
} 
} 
  
// This code is contributed by Sahil_Bansall 
```

## Python3

```py
# Sorting based Python 3 program 
# to find all elements in array  
# which have atleast two greater  
# elements itself. 
  
def findElements(arr, n): 
  
    arr.sort() 
  
    for i in range(0, n-2): 
        print(arr[i], end =" ") 
  
# Driven source 
arr = [2, -6, 3, 5, 1] 
n = len(arr) 
findElements(arr, n) 
  
# This code is contributed  
# by Smitha Dinesh Semwal 
```

## C#

```cs
// Sorting based C# program to find  
// all elements in array which have  
// atleast two greater elements itself. 
using System; 
  
class GFG 
{ 
  
static void findElements(int []arr, int n) 
{ 
    Array.Sort(arr); 
  
    for (int i = 0; i < n-2; i++) 
        Console.Write(arr[i] + " "); 
} 
  
// Driver code 
public static void Main(String []args) 
{ 
    int []arr = { 2, -6 ,3 , 5, 1}; 
    int n = arr.Length; 
    findElements(arr, n); 
  
} 
} 
  
// This code is contributed by parashar 
```

## PHP

```php
<?php 
// Sorting based PHP program to  
// find all elements in array  
// which have atleast two greater 
// elements itself. 
  
function findElements( $arr, $n) 
{ 
    sort($arr); 
  
    for ($i = 0; $i < $n - 2; $i++) 
    echo $arr[$i] , " "; 
} 
  
// Driver Code 
$arr = array( 2, -6 ,3 , 5, 1); 
$n = count($arr); 
findElements($arr, $n);  
  
// This code is contributed by anuj_67. 
?>; 
```

输出：

```
-6 1 2
```

时间复杂度：`O(n Log n)`。

方法 3（高效）：

在第二种方法中，我们只需计算数组的第二个最大元素，然后打印所有小于或等于第二个最大元素的元素。

## C++

```cpp
// C++ program to find all elements 
// in array which have atleast two  
// greater elements itself. 
#include<bits/stdc++.h> 
using namespace std; 
  
void findElements(int arr[], int n) 
{ 
    int first = INT_MIN,  
        second = INT_MIN; 
    for (int i = 0; i < n; i++) 
    { 
        /* If current element is smaller  
        than first then update both first  
        and second */
        if (arr[i] > first) 
        { 
            second = first; 
            first = arr[i]; 
        } 
  
        /* If arr[i] is in between first  
        and second then update second */
        else if (arr[i] > second) 
            second = arr[i]; 
    } 
  
    for (int i = 0; i < n; i++) 
        if (arr[i] < second) 
            cout << arr[i] << " "; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 2, -6, 3, 5, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findElements(arr, n); 
    return 0; 
} 
```

## Java

```java
// Java program to find all elements 
// in array which have atleast 
// two greater elements itself. 
import java.util.*; 
import java.io.*; 
  
class GFG 
{ 
      
static void findElements(int arr[], int n) 
{ 
    int first = Integer.MIN_VALUE; 
    int second = Integer.MAX_VALUE; 
      
    for (int i = 0; i < n; i++) 
    { 
        // If current element is smaller  
        // than first then update both 
        // first and second  
        if (arr[i] > first) 
        { 
            second = first; 
            first = arr[i]; 
        } 
  
        /* If arr[i] is in between  
        first and second 
        then update second */
        else if (arr[i] > second) 
            second = arr[i]; 
    } 
  
    for (int i = 0; i < n; i++) 
        if (arr[i] < second) 
            System.out.print(arr[i] + " ") ; 
} 
// Driver code 
public static void main(String args[]) 
{ 
    int arr[] = { 2, -6, 3, 5, 1}; 
    int n = arr.length; 
    findElements(arr, n); 
} 
} 
  
// This code is contributed by Sahil_Bansall 
```

## Python3

```py
# Python 3 program to find all elements 
# in array which have atleast two  
# greater elements itself. 
import sys 
  
def findElements(arr, n): 
  
    first = -sys.maxsize 
    second = -sys.maxsize 
  
    for i in range(0, n): 
      
        # If current element is smaller 
        # than first then update both 
        # first and second  
        if (arr[i] > first): 
          
            second = first 
            first = arr[i] 
          
        # If arr[i] is in between first 
        # and second then update second  
        elif (arr[i] > second): 
            second = arr[i] 
      
    for i in range(0, n): 
        if (arr[i] < second): 
            print(arr[i], end =" ") 
  
  
# Driver code 
arr = [2, -6, 3, 5, 1] 
n = len(arr) 
findElements(arr, n) 
  
# This code is contributed 
# by Smitha Dinesh Semwal 
```

## C#

```cs
// C# program to find all elements 
// in array which have atleast 
// two greater elements itself. 
using System; 
  
class GFG 
{ 
    static void findElements(int []arr,  
                            int n) 
    { 
    int first = int.MinValue; 
    int second = int.MaxValue; 
      
    for (int i = 0; i < n; i++) 
    { 
        // If current element is smaller  
        // than first then update both  
        // first and second  
        if (arr[i] > first) 
        { 
            second = first; 
            first = arr[i]; 
        } 
  
        /* If arr[i] is in between  
        first and second 
        then update second */
        else if (arr[i] > second) 
            second = arr[i]; 
    } 
  
    for (int i = 0; i < n; i++) 
        if (arr[i] < second) 
            Console.Write(arr[i] + " ") ; 
} 
// Driver code 
public static void Main(String []args) 
{ 
    int []arr = { 2, -6, 3, 5, 1}; 
    int n = arr.Length; 
    findElements(arr, n); 
} 
} 
  
// This code is contributed by parashar... 
```

## PHP

```php
<?php 
// PHP program to find all elements 
// in  array which have atleast two  
// greater elements itself. 
  
function findElements($arr, $n) 
{ 
      
    $first = PHP_INT_MIN;  
    $second =  PHP_INT_MIN; 
    for ($i = 0; $i < $n; $i++) 
    { 
          
            /* If current element is smaller  
            than first then update both first  
            and second */
            if ($arr[$i] > $first) 
            { 
                $second = $first; 
                $first = $arr[$i]; 
              
      
            } 
  
        /* If arr[i] is in between first  
           and second then update second */
        else if ($arr[$i] > $second) 
            $second = $arr[$i]; 
    } 
  
    for($i = 0; $i < $n; $i++) 
        if ($arr[$i] < $second) 
            echo $arr[$i] , " "; 
} 
  
    // Driver code 
    $arr = array(2, -6, 3, 5, 1); 
    $n = count($arr); 
    findElements($arr, $n); 
  
// This code is contributed by vishal tripathi. 
?> 
```

输出：

```
2  -6  1
```

时间复杂度：`O(n)`。