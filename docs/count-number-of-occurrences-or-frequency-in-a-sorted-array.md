# 计数排序数组中的出现次数（或频率）

> 原文： [https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)

给定一个已排序的数组`arr[]`和一个数字`x`，编写一个函数计算`arr[]`中`x`的出现。 预期时间复杂度为`O(Logn)`。

**示例**：

```
  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 2
  Output: 4 // x (or 2) occurs 4 times in arr[]

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 3
  Output: 1 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 1
  Output: 2 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 4
  Output: -1 // 4 doesn't occur in arr[] 
```



**方法 1（线性搜索）**：

线性搜索`x`，计算`x`的出现次数并返回计数。

## C++ 

```cpp

// C++ program to count occurrences of an element 
#include<bits/stdc++.h> 
using namespace std; 

// Returns number of times x occurs in arr[0..n-1] 
int countOccurrences(int arr[], int n, int x) 
{ 
    int res = 0; 
    for (int i=0; i<n; i++) 
        if (x == arr[i]) 
          res++; 
    return res; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 2; 
    cout << countOccurrences(arr, n, x); 
    return 0; 
} 

```

## Java

```java
// Java program to count occurrences  
// of an element 
  
class Main 
{ 
    // Returns number of times x occurs in arr[0..n-1] 
    static int countOccurrences(int arr[], int n, int x) 
    { 
        int res = 0; 
        for (int i=0; i<n; i++) 
            if (x == arr[i]) 
              res++; 
        return res; 
    } 
      
    public static void main(String args[]) 
    { 
        int arr[] = {1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 }; 
        int n = arr.length; 
        int x = 2; 
        System.out.println(countOccurrences(arr, n, x)); 
    } 
}
```

## Python3

```py
# Python3 program to count  
# occurrences of an element 
  
# Returns number of times x  
# occurs in arr[0..n-1] 
def countOccurrences(arr, n, x): 
    res = 0
    for i in range(n): 
        if x == arr[i]: 
            res += 1
    return res 
   
# Driver code 
arr = [1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8] 
n = len(arr) 
x = 2
print (countOccurrences(arr, n, x))
```

## C#

```cs
// C# program to count occurrences  
// of an element 
using System; 
  
class GFG 
{ 
    // Returns number of times x 
    // occurs in arr[0..n-1] 
    static int countOccurrences(int []arr, 
                                int n, int x) 
    { 
        int res = 0; 
          
        for (int i = 0; i < n; i++) 
            if (x == arr[i]) 
            res++; 
              
        return res; 
    } 
      
    // driver code     
    public static void Main() 
    { 
        int []arr = {1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 }; 
        int n = arr.Length; 
        int x = 2; 
          
        Console.Write(countOccurrences(arr, n, x)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to count occurrences 
// of an element 
  
// Returns number of times x  
// occurs in arr[0..n-1] 
function countOccurrences($arr, $n, $x) 
{ 
    $res = 0; 
    for ($i = 0; $i < $n; $i++) 
        if ($x == $arr[$i]) 
        $res++; 
    return $res; 
} 
  
    // Driver code 
    $arr = array(1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 ); 
    $n = count($arr); 
    $x = 2; 
    echo countOccurrences($arr,$n, $x); 
      
// This code is contributed by Sam007 
?>
```

输出：

```
4
```

时间复杂度：`O(n)`。

方法 2（更好地使用二进制搜索）：

我们首先使用二进制搜索找到一个事件。 然后，我们向匹配的找到的索引的左侧和右侧进行匹配。

## C++

```cpp
// C++ program to count occurrences of an element 
#include <bits/stdc++.h> 
using namespace std; 
  
// A recursive binary search function. It returns 
// location of x in given array arr[l..r] is present, 
// otherwise -1 
int binarySearch(int arr[], int l, int r, int x) 
{ 
    if (r < l) 
        return -1; 
  
    int mid = l + (r - l) / 2; 
  
    // If the element is present at the middle 
    // itself 
    if (arr[mid] == x) 
        return mid; 
  
    // If element is smaller than mid, then 
    // it can only be present in left subarray 
    if (arr[mid] > x) 
        return binarySearch(arr, l, mid - 1, x); 
  
    // Else the element can only be present 
    // in right subarray 
    return binarySearch(arr, mid + 1, r, x); 
} 
  
// Returns number of times x occurs in arr[0..n-1] 
int countOccurrences(int arr[], int n, int x) 
{ 
    int ind = binarySearch(arr, 0, n - 1, x); 
  
    // If element is not present 
    if (ind == -1) 
        return 0; 
  
    // Count elements on left side. 
    int count = 1; 
    int left = ind - 1; 
    while (left >= 0 && arr[left] == x) 
        count++, left--; 
  
    // Count elements on right side. 
    int right = ind + 1; 
    while (right < n && arr[right] == x) 
        count++, right++; 
  
    return count; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 2, 2, 2, 3, 4, 7, 8, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int x = 2; 
    cout << countOccurrences(arr, n, x); 
    return 0; 
}
```

## Java

```java
// Java program to count  
// occurrences of an element 
class GFG  
{ 
  
    // A recursive binary search  
    // function. It returns location  
    // of x in given array arr[l..r]  
    // is present, otherwise -1 
    static int binarySearch(int arr[], int l, 
                            int r, int x) 
    { 
        if (r < l) 
            return -1; 
  
        int mid = l + (r - l) / 2; 
  
        // If the element is present  
        // at the middle itself 
        if (arr[mid] == x) 
            return mid; 
  
        // If element is smaller than  
        // mid, then it can only be  
        // present in left subarray 
        if (arr[mid] > x) 
            return binarySearch(arr, l,  
                                mid - 1, x); 
  
        // Else the element can 
        // only be present in 
        // right subarray 
        return binarySearch(arr, mid + 1, r, x); 
    } 
  
    // Returns number of times x 
    // occurs in arr[0..n-1] 
    static int countOccurrences(int arr[],  
                                int n, int x) 
    { 
        int ind = binarySearch(arr, 0,  
                               n - 1, x); 
  
        // If element is not present 
        if (ind == -1) 
            return 0; 
  
        // Count elements on left side. 
        int count = 1; 
        int left = ind - 1; 
        while (left >= 0 &&  
               arr[left] == x) 
        { 
            count++; 
            left--; 
        } 
  
        // Count elements  
        // on right side. 
        int right = ind + 1; 
        while (right < n &&  
               arr[right] == x) 
        { 
            count++; 
            right++; 
        } 
  
        return count; 
    } 
  
  
    // Driver code 
    public static void main(String[] args)  
    { 
        int arr[] = {1, 2, 2, 2, 2,  
                     3, 4, 7, 8, 8}; 
        int n = arr.length; 
        int x = 2; 
        System.out.print(countOccurrences(arr, n, x)); 
    } 
} 
  
// This code is contributed  
// by ChitraNayal
```

## Python 3

```
# Python 3 program to count  
# occurrences of an element 
  
# A recursive binary search  
# function. It returns location 
# of x in given array arr[l..r]  
# is present, otherwise -1 
def binarySearch(arr, l, r, x): 
    if (r < l): 
        return -1
  
    mid = int( l + (r - l) / 2) 
  
    # If the element is present  
    # at the middle itself 
    if arr[mid] == x: 
        return mid 
  
    # If element is smaller than  
    # mid, then it can only be 
    # present in left subarray 
    if arr[mid] > x: 
        return binarySearch(arr, l,  
                            mid - 1, x) 
  
    # Else the element  
    # can only be present 
    # in right subarray 
    return binarySearch(arr, mid + 1, 
                                r, x) 
  
# Returns number of times  
# x occurs in arr[0..n-1] 
def countOccurrences(arr, n, x): 
    ind = binarySearch(arr, 0, n - 1, x) 
  
    # If element is not present 
    if ind == -1: 
        return 0
  
    # Count elements  
    # on left side. 
    count = 1
    left = ind - 1
    while (left >= 0 and 
           arr[left] == x): 
        count += 1
        left -= 1
  
    # Count elements on 
    # right side. 
    right = ind + 1; 
    while (right < n and
           arr[right] == x): 
        count += 1
        right += 1
  
    return count 
  
# Driver code 
arr = [ 1, 2, 2, 2, 2,  
        3, 4, 7, 8, 8 ] 
n = len(arr) 
x = 2
print(countOccurrences(arr, n, x)) 
  
# This code is contributed  
# by ChitraNayal
```

## C#

```cs
// C# program to count  
// occurrences of an element 
using System; 
  
class GFG  
{ 
  
    // A recursive binary search  
    // function. It returns location 
    // of x in given array arr[l..r]  
    // is present, otherwise -1 
    static int binarySearch(int[] arr, int l,  
                            int r, int x) 
    { 
        if (r < l) 
            return -1; 
  
        int mid = l + (r - l) / 2; 
  
        // If the element is present  
        // at the middle itself 
        if (arr[mid] == x) 
            return mid; 
  
        // If element is smaller than  
        // mid, then it can only be  
        // present in left subarray 
        if (arr[mid] > x) 
            return binarySearch(arr, l,  
                                mid - 1, x); 
  
        // Else the element  
        // can only be present 
        // in right subarray 
        return binarySearch(arr, mid + 1, 
                                   r, x); 
    } 
  
    // Returns number of times x  
    // occurs in arr[0..n-1] 
    static int countOccurrences(int[] arr,  
                                int n, int x) 
    { 
        int ind = binarySearch(arr, 0,  
                               n - 1, x); 
  
        // If element is not present 
        if (ind == -1) 
            return 0; 
  
        // Count elements on left side. 
        int count = 1; 
        int left = ind - 1; 
        while (left >= 0 &&  
               arr[left] == x) 
        { 
            count++; 
            left--; 
        } 
  
        // Count elements on right side. 
        int right = ind + 1; 
        while (right < n &&  
               arr[right] == x) 
        { 
            count++; 
            right++; 
        } 
  
        return count; 
    } 
  
  
    // Driver code 
    public static void Main()  
    { 
        int[] arr = {1, 2, 2, 2, 2,  
                     3, 4, 7, 8, 8}; 
        int n = arr.Length; 
        int x = 2; 
        Console.Write(countOccurrences(arr, n, x)); 
    } 
} 
  
// This code is contributed  
// by ChitraNayal
```

## PHP

```php
<?php  
// PHP program to count  
// occurrences of an element 
  
// A recursive binary search  
// function. It returns location 
// of x in given array arr[l..r]  
// is present, otherwise -1 
function binarySearch(&$arr, $l,  
                         $r, $x) 
{ 
    if ($r < $l) 
        return -1; 
  
    $mid = $l + ($r - $l) / 2; 
  
    // If the element is present  
    // at the middle itself 
    if ($arr[$mid] == $x) 
        return $mid; 
  
    // If element is smaller than  
    // mid, then it can only be 
    // present in left subarray 
    if ($arr[$mid] > $x) 
        return binarySearch($arr, $l,    
                            $mid - 1, $x); 
  
    // Else the element 
    // can only be present 
    // in right subarray 
    return binarySearch($arr, $mid + 1,  
                                $r, $x); 
} 
  
// Returns number of times 
// x occurs in arr[0..n-1] 
function countOccurrences($arr, $n, $x) 
{ 
    $ind = binarySearch($arr, 0,  
                        $n - 1, $x); 
  
    // If element is not present 
    if ($ind == -1) 
        return 0; 
  
    // Count elements  
    // on left side. 
    $count = 1; 
    $left = $ind - 1; 
    while ($left >= 0 &&  
           $arr[$left] == $x) 
    {  
        $count++; 
        $left--; 
    } 
      
    // Count elements on right side. 
    $right = $ind + 1; 
    while ($right < $n &&  
           $arr[$right] == $x) 
    { 
        $count++; 
        $right++; 
    } 
    return $count; 
} 
  
// Driver code 
$arr = array( 1, 2, 2, 2, 2,  
              3, 4, 7, 8, 8 ); 
$n = sizeof($arr); 
$x = 2; 
echo countOccurrences($arr, $n, $x); 
  
// This code is contributed 
// by ChitraNayal 
?>
```

输出：

```
4
```

时间复杂度：`O(Log n + count)`，其中`count`是出现的次数。

 

方法 3（最佳使用改进的二进制搜索）：

1.  使用二进制搜索获取`x`在`arr[]`中首次出现的索引。 令第一次出现的索引为`i`。
2.  使用二进制搜索获取`x`在`arr[]`中最后一次出现的索引。 令最后一次出现的索引为`j`。
3.  返回`j – i + 1`；

## C++

```cpp
// C++ program to count occurrences of an element 
// in a sorted array. 
# include <bits/stdc++.h> 
using namespace std; 
  
/* if x is present in arr[] then returns the count 
    of occurrences of x, otherwise returns 0. */
int count(int arr[], int x, int n) 
{     
  /* get the index of first occurrence of x */
  int *low = lower_bound(arr, arr+n, x); 
  
  // If element is not present, return 0 
  if (low == (arr + n) || *low != x) 
     return 0; 
     
  /* Else get the index of last occurrence of x. 
     Note that we  are only looking in the  
     subarray after first occurrence */   
  int *high = upper_bound(low, arr+n, x);      
     
  /* return count */
  return high - low; 
} 
  
/* driver program to test above functions */
int main() 
{ 
  int arr[] = {1, 2, 2, 3, 3, 3, 3}; 
  int x =  3;  // Element to be counted in arr[] 
  int n = sizeof(arr)/sizeof(arr[0]); 
  int c = count(arr, x, n); 
  printf(" %d occurs %d times ", x, c); 
  return 0; 
}
```

## C

```c
# include <stdio.h> 
  
/* if x is present in arr[] then returns  
   the index of FIRST occurrence  
   of x in arr[0..n-1], otherwise returns -1 */
int first(int arr[], int low, int high, int x, int n) 
{ 
  if(high >= low) 
  { 
    int mid = (low + high)/2;  /*low + (high - low)/2;*/
    if( ( mid == 0 || x > arr[mid-1]) && arr[mid] == x) 
      return mid; 
    else if(x > arr[mid]) 
      return first(arr, (mid + 1), high, x, n); 
    else
      return first(arr, low, (mid -1), x, n); 
  } 
  return -1; 
} 
  
/* if x is present in arr[] then returns the 
   index of LAST occurrence of x in arr[0..n-1],  
   otherwise returns -1 */ 
int last(int arr[], int low, int high, int x, int n) 
{ 
  if (high >= low) 
  { 
    int mid = (low + high)/2;  /*low + (high - low)/2;*/
    if( ( mid == n-1 || x < arr[mid+1]) && arr[mid] == x ) 
      return mid; 
    else if(x < arr[mid]) 
      return last(arr, low, (mid -1), x, n); 
    else
      return last(arr, (mid + 1), high, x, n);       
  } 
  return -1; 
} 
  
/* if x is present in arr[] then returns the count 
   of occurrences of x, otherwise returns -1. */
int count(int arr[], int x, int n) 
{ 
  int i; // index of first occurrence of x in arr[0..n-1] 
  int j; // index of last occurrence of x in arr[0..n-1] 
      
  /* get the index of first occurrence of x */
  i = first(arr, 0, n-1, x, n); 
  
  /* If x doesn't exist in arr[] then return -1 */
  if(i == -1) 
    return i; 
     
  /* Else get the index of last occurrence of x.  
     Note that we are only looking in the subarray  
     after first occurrence */   
  j = last(arr, i, n-1, x, n);      
     
  /* return count */
  return j-i+1; 
} 
  
/* driver program to test above functions */
int main() 
{ 
  int arr[] = {1, 2, 2, 3, 3, 3, 3}; 
  int x =  3;  // Element to be counted in arr[] 
  int n = sizeof(arr)/sizeof(arr[0]); 
  int c = count(arr, x, n); 
  printf(" %d occurs %d times ", x, c); 
  getchar(); 
  return 0; 
}
```

## Java

```java
// Java program to count occurrences  
// of an element 
  
class Main 
{ 
    /* if x is present in arr[] then returns  
       the count of occurrences of x,  
       otherwise returns -1. */
    static int count(int arr[], int x, int n) 
    { 
      // index of first occurrence of x in arr[0..n-1]     
      int i;  
        
      // index of last occurrence of x in arr[0..n-1] 
      int j;  
           
      /* get the index of first occurrence of x */
      i = first(arr, 0, n-1, x, n); 
       
      /* If x doesn't exist in arr[] then return -1 */
      if(i == -1) 
        return i; 
          
      /* Else get the index of last occurrence of x.  
         Note that we are only looking in the  
         subarray after first occurrence */  
      j = last(arr, i, n-1, x, n);      
          
      /* return count */
      return j-i+1; 
    } 
       
    /* if x is present in arr[] then returns the  
       index of FIRST occurrence of x in arr[0..n-1],  
       otherwise returns -1 */
    static int first(int arr[], int low, int high, int x, int n) 
    { 
      if(high >= low) 
      { 
        /*low + (high - low)/2;*/  
        int mid = (low + high)/2;   
        if( ( mid == 0 || x > arr[mid-1]) && arr[mid] == x) 
          return mid; 
        else if(x > arr[mid]) 
          return first(arr, (mid + 1), high, x, n); 
        else
          return first(arr, low, (mid -1), x, n); 
      } 
      return -1; 
    } 
       
    /* if x is present in arr[] then returns the  
       index of LAST occurrence of x in arr[0..n-1],  
       otherwise returns -1 */
    static int last(int arr[], int low, int high, int x, int n) 
    { 
      if(high >= low) 
      { 
        /*low + (high - low)/2;*/      
        int mid = (low + high)/2;  
        if( ( mid == n-1 || x < arr[mid+1]) && arr[mid] == x ) 
          return mid; 
        else if(x < arr[mid]) 
          return last(arr, low, (mid -1), x, n); 
        else
          return last(arr, (mid + 1), high, x, n);       
      } 
      return -1; 
    } 
       
    public static void main(String args[]) 
    { 
        int arr[] = {1, 2, 2, 3, 3, 3, 3}; 
          
        // Element to be counted in arr[] 
        int x =  3;  
        int n = arr.length; 
        int c = count(arr, x, n); 
        System.out.println(x+" occurs "+c+" times"); 
    } 
}
```

## Python3

```py
# Python3 program to count 
# occurrences of an element 
  
# if x is present in arr[] then  
# returns the count of occurrences 
# of x, otherwise returns -1.  
def count(arr, x, n): 
  
    # get the index of first 
    # occurrence of x  
    i = first(arr, 0, n-1, x, n) 
   
    # If x doesn't exist in  
    # arr[] then return -1  
    if i == -1: 
        return i 
      
    # Else get the index of last occurrence 
    # of x. Note that we are only looking 
    # in the subarray after first occurrence    
    j = last(arr, i, n-1, x, n);      
      
    # return count  
    return j-i+1; 
  
# if x is present in arr[] then return 
# the index of FIRST occurrence of x in 
# arr[0..n-1], otherwise returns -1  
def first(arr, low, high, x, n): 
    if high >= low: 
  
        # low + (high - low)/2 
        mid = (low + high)//2      
          
    if (mid == 0 or x > arr[mid-1]) and arr[mid] == x: 
        return mid 
    elif x > arr[mid]: 
        return first(arr, (mid + 1), high, x, n) 
    else: 
        return first(arr, low, (mid -1), x, n) 
    return -1; 
   
# if x is present in arr[] then return 
# the index of LAST occurrence of x  
# in arr[0..n-1], otherwise returns -1  
def last(arr, low, high, x, n): 
    if high >= low: 
  
        # low + (high - low)/2 
        mid = (low + high)//2;  
   
    if(mid == n-1 or x < arr[mid+1]) and arr[mid] == x : 
        return mid 
    elif x < arr[mid]: 
        return last(arr, low, (mid -1), x, n) 
    else: 
        return last(arr, (mid + 1), high, x, n)      
    return -1
  
# driver program to test above functions  
arr = [1, 2, 2, 3, 3, 3, 3] 
x = 3  # Element to be counted in arr[] 
n = len(arr) 
c = count(arr, x, n) 
print ("%d occurs %d times "%(x, c))
```

## C#

```cs
// C# program to count occurrences  
// of an element 
using System; 
  
class GFG 
{ 
      
    /* if x is present in arr[] then returns  
    the count of occurrences of x,  
    otherwise returns -1. */
    static int count(int []arr, int x, int n) 
    { 
    // index of first occurrence of x in arr[0..n-1]  
    int i;  
          
    // index of last occurrence of x in arr[0..n-1] 
    int j;  
          
    /* get the index of first occurrence of x */
    i = first(arr, 0, n-1, x, n); 
      
    /* If x doesn't exist in arr[] then return -1 */
    if(i == -1) 
        return i; 
          
    /* Else get the index of last occurrence of x.  
        Note that we are only looking in the  
        subarray after first occurrence */
    j = last(arr, i, n-1, x, n);      
          
    /* return count */
    return j-i+1; 
    } 
      
    /* if x is present in arr[] then returns the  
    index of FIRST occurrence of x in arr[0..n-1],  
    otherwise returns -1 */
    static int first(int []arr, int low, int high,  
                                     int x, int n) 
    { 
    if(high >= low) 
    { 
        /*low + (high - low)/2;*/
        int mid = (low + high)/2;  
        if( ( mid == 0 || x > arr[mid-1])  
                            && arr[mid] == x) 
        return mid; 
        else if(x > arr[mid]) 
        return first(arr, (mid + 1), high, x, n); 
        else
        return first(arr, low, (mid -1), x, n); 
    } 
    return -1; 
    } 
      
    /* if x is present in arr[] then returns the  
    index of LAST occurrence of x in arr[0..n-1],  
    otherwise returns -1 */
    static int last(int []arr, int low, 
                        int high, int x, int n) 
    { 
    if(high >= low) 
    { 
        /*low + (high - low)/2;*/    
        int mid = (low + high)/2;  
        if( ( mid == n-1 || x < arr[mid+1]) 
                            && arr[mid] == x ) 
        return mid; 
        else if(x < arr[mid]) 
        return last(arr, low, (mid -1), x, n); 
        else
        return last(arr, (mid + 1), high, x, n);      
    } 
    return -1; 
    } 
      
    public static void Main() 
    { 
        int []arr = {1, 2, 2, 3, 3, 3, 3}; 
          
        // Element to be counted in arr[] 
        int x = 3;  
        int n = arr.Length; 
        int c = count(arr, x, n); 
          
        Console.Write(x + " occurs " + c + " times"); 
    } 
} 
// This code is contributed by Sam007
```

输出：

```
3 occurs 4 times
```

时间复杂度：`O(logn)`。

编程范式：分而治之。