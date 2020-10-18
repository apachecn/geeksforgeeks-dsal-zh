# 排序数组的上界

> 原文： [https://www.geeksforgeeks.org/ceiling-in-a-sorted-array/](https://www.geeksforgeeks.org/ceiling-in-a-sorted-array/)

给定一个排序数组和一个值`x`，`x`的上限是数组中大于或等于`x`的最小元素，下限是小于或等于`x`的最大元素。 假设数组以非降序排序。 编写有效的函数以查找`x`的底和顶。

**示例**：

```
For example, let the input array be {1, 2, 8, 10, 10, 12, 19}
For x = 0:    floor doesn't exist in array,  ceil  = 1
For x = 1:    floor  = 1,  ceil  = 1
For x = 5:    floor  = 2,  ceil  = 8
For x = 20:   floor  = 19,  ceil doesn't exist in array

```

在以下方法中，我们仅实现了上限搜索功能。 楼层搜索可以以相同的方式实现。

**方法 1（线性搜索）**：

用于搜索`x`上限的算法：

1.  如果`x`小于或等于数组中的第一个元素，则返回 0（第一个元素的索引）

2.  其他线性搜索索引`i`，以使`x`介于`arr[i]`和`arr[i + 1]`之间。

3.  如果在步骤 2 中找不到索引`i`，则返回 -1

## C++ 

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Function to get index of ceiling of x in arr[low..high] */
int ceilSearch(int arr[], int low, int high, int x)  
{  

    int i;  

    /* If x is smaller than or equal to first element,  
        then return the first element */
    if(x <= arr[low])  
        return low;  

    /* Otherwise, linearly search for ceil value */
    for(i = low; i < high; i++)  
    {  
        if(arr[i] == x)  
        return i;  

        /* if x lies between arr[i] and arr[i+1] including  
        arr[i+1], then return arr[i+1] */
        if(arr[i] < x && arr[i+1] >= x)  
        return i+1;  
    }      

    /* If we reach here then x is greater than the last element  
        of the array, return -1 in this case */
    return -1;  
}  

/* Driver code*/
int main()  
{  
    int arr[] = {1, 2, 8, 10, 10, 12, 19};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    int x = 3;  
    int index = ceilSearch(arr, 0, n-1, x);  
    if(index == -1)  
        cout << "Ceiling of " << x << " doesn't exist in array ";  
    else
        cout << "ceiling of " << x << " is " << arr[index];  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c
#include<stdio.h> 
  
/* Function to get index of ceiling of x in arr[low..high] */
int ceilSearch(int arr[], int low, int high, int x) 
{ 
  int i;     
  
  /* If x is smaller than or equal to first element, 
    then return the first element */
  if(x <= arr[low]) 
    return low;   
  
  /* Otherwise, linearly search for ceil value */
  for(i = low; i < high; i++) 
  { 
    if(arr[i] == x) 
      return i; 
  
    /* if x lies between arr[i] and arr[i+1] including 
       arr[i+1], then return arr[i+1] */
    if(arr[i] < x && arr[i+1] >= x) 
       return i+1; 
  }          
  
  /* If we reach here then x is greater than the last element  
    of the array,  return -1 in this case */
  return -1; 
} 
  
  
/* Driver program to check above functions */
int main() 
{ 
   int arr[] = {1, 2, 8, 10, 10, 12, 19}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   int x = 3; 
   int index = ceilSearch(arr, 0, n-1, x); 
   if(index == -1) 
     printf("Ceiling of %d doesn't exist in array ", x); 
   else
     printf("ceiling of %d is %d", x, arr[index]); 
   getchar(); 
   return 0; 
} 
```

## Java

```java
class Main 
{ 
    /* Function to get index of ceiling  
       of x in arr[low..high] */
    static int ceilSearch(int arr[], int low, int high, int x) 
    { 
      int i;     
       
      /* If x is smaller than or equal to first  
         element,then return the first element */
      if(x <= arr[low]) 
        return low;   
       
      /* Otherwise, linearly search for ceil value */
      for(i = low; i < high; i++) 
      { 
        if(arr[i] == x) 
          return i; 
       
        /* if x lies between arr[i] and arr[i+1]  
        including arr[i+1], then return arr[i+1] */
        if(arr[i] < x && arr[i+1] >= x) 
           return i+1; 
      }          
       
      /* If we reach here then x is greater than the  
      last element of the array,  return -1 in this case */
      return -1; 
    } 
       
       
    /* Driver program to check above functions */
    public static void main (String[] args) 
    { 
       int arr[] = {1, 2, 8, 10, 10, 12, 19}; 
       int n = arr.length; 
       int x = 3; 
       int index = ceilSearch(arr, 0, n-1, x); 
       if(index == -1) 
         System.out.println("Ceiling of "+x+" doesn't exist in array"); 
       else
         System.out.println("ceiling of "+x+" is "+arr[index]); 
    }   
} 
```

## Python3

```py
# Function to get index of ceiling of x in arr[low..high] */ 
def ceilSearch(arr, low, high, x): 
  
    # If x is smaller than or equal to first element, 
    # then return the first element */ 
    if x <= arr[low]: 
        return low 
  
    # Otherwise, linearly search for ceil value */ 
    i = low 
    for i in range(high): 
        if arr[i] == x: 
            return i 
  
        # if x lies between arr[i] and arr[i+1] including 
        # arr[i+1], then return arr[i+1] */ 
        if arr[i] < x and arr[i+1] >= x: 
            return i+1
          
    # If we reach here then x is greater than the last element  
    # of the array,  return -1 in this case */ 
    return -1
  
# Driver program to check above functions */ 
arr = [1, 2, 8, 10, 10, 12, 19] 
n = len(arr) 
x = 3
index = ceilSearch(arr, 0, n-1, x); 
  
if index == -1: 
    print ("Ceiling of %d doesn't exist in array "% x) 
else: 
    print ("ceiling of %d is %d"%(x, arr[index])) 
  
# This code is contributed by Shreyanshi Arun 
```

## C#

```cs
// C# program to find celing 
// in a sorted array 
using System; 
  
class GFG { 
      
    // Function to get index of ceiling  
    // of x in arr[low..high]  
    static int ceilSearch(int[] arr, int low,  
                           int high, int x) 
    { 
        int i; 
  
        // If x is smaller than or equal 
        // to first element, then return 
        // the first element  
        if (x <= arr[low]) 
            return low; 
  
        // Otherwise, linearly search  
        // for ceil value  
        for (i = low; i < high; i++) { 
            if (arr[i] == x) 
                return i; 
  
            /* if x lies between arr[i] and  
            arr[i+1] including arr[i+1],  
            then return arr[i+1] */
            if (arr[i] < x && arr[i + 1] >= x) 
                return i + 1; 
        } 
  
        /* If we reach here then x is  
        greater than the last element  
        of the array, return -1 in  
        this case */
        return -1; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 8, 10, 10, 12, 19 }; 
        int n = arr.Length; 
        int x = 3; 
        int index = ceilSearch(arr, 0, n - 1, x); 
          
        if (index == -1) 
            Console.Write("Ceiling of " + x + 
                     " doesn't exist in array"); 
        else
            Console.Write("ceiling of " + x + 
                         " is " + arr[index]); 
    } 
} 
  
// This code is contributed by Sam007. 
```

## PHP

```php
<?php 
// Function to get index of  
// ceiling of x in arr[low..high]  
function ceilSearch($arr, $low, $high, $x) 
{ 
  
    // If x is smaller than or equal  
    // to first element, then return  
    // the first element  
    if($x <= $arr[$low]) 
        return $low;  
      
    // Otherwise, linearly search 
    // for ceil value  
    for($i = $low; $i < $high; $i++) 
    { 
        if($arr[$i] == $x) 
            return $i; 
      
        // if x lies between arr[i] and  
        // arr[i+1] including arr[i+1],  
        // then return arr[i+1]  
        if($arr[$i] < $x &&  
           $arr[$i + 1] >= $x) 
            return $i + 1; 
    }      
      
    // If we reach here then x is greater  
    // than the last element of the array, 
    // return -1 in this case  
    return -1; 
} 
  
// Driver Code 
$arr = array(1, 2, 8, 10, 10, 12, 19); 
$n = sizeof($arr); 
$x = 3; 
$index = ceilSearch($arr, 0, $n - 1, $x); 
if($index == -1) 
    echo("Ceiling of " . $x .  
         " doesn't exist in array "); 
else
    echo("ceiling of " . $x . " is " .  
                        $arr[$index]); 
  
// This code is contributed by Ajit. 
?> 
```

输出：

```
ceiling of 3 is 8
```

时间复杂度：`O(n)`。

方法 2（二进制搜索）：

此处不使用线性搜索，而是使用二进制搜索来查找索引。 二进制搜索将时间复杂度降低到`O(Logn)`。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std; 
  
/* Function to get index of  
   ceiling of x in arr[low..high]*/
int ceilSearch(int arr[], int low, int high, int x)  
{  
    int mid;      
      
    /* If x is smaller than  
       or equal to the first element,  
       then return the first element */
    if(x <= arr[low])  
        return low;  
      
    /* If x is greater than the last element,  
       then return -1 */
    if(x > arr[high])  
        return -1;  
      
    /* get the index of middle element of arr[low..high]*/
    mid = (low + high) / 2; /* low + (high - low)/2 */
      
    /* If x is same as middle element,  
       then return mid */
    if(arr[mid] == x)  
        return mid;  
          
    /* If x is greater than arr[mid],  
       then either arr[mid + 1] is ceiling of x  
       or ceiling lies in arr[mid+1...high] */
    else if(arr[mid] < x)  
    {  
        if(mid + 1 <= high && x <= arr[mid + 1])  
            return mid + 1;  
        else
            return ceilSearch(arr, mid + 1, high, x);  
    }  
      
    /* If x is smaller than arr[mid],  
       then either arr[mid] is ceiling of x  
       or ceiling lies in arr[low...mid-1] */
    else
    {  
        if(mid - 1 >= low && x > arr[mid - 1])  
            return mid;  
        else
            return ceilSearch(arr, low, mid - 1, x);  
    }  
}  
  
// Driver Code 
int main()  
{  
    int arr[] = {1, 2, 8, 10, 10, 12, 19};  
    int n = sizeof(arr) / sizeof(arr[0]);  
    int x = 20;  
    int index = ceilSearch(arr, 0, n-1, x);  
    if(index == -1)  
        cout << "Ceiling of " << x  
             << " doesn't exist in array ";  
    else
        cout << "ceiling of " << x  
             << " is " << arr[index];  
      
    return 0;  
}  
  
// This code is contributed by rathbhupendra 
```

## C

```c
#include<stdio.h> 
  
/* Function to get index of ceiling of x in arr[low..high]*/
int ceilSearch(int arr[], int low, int high, int x) 
{ 
  int mid;     
  
  /* If x is smaller than or equal to the first element, 
    then return the first element */
  if(x <= arr[low]) 
    return low;  
  
  /* If x is greater than the last element, then return -1 */
  if(x > arr[high]) 
    return -1;   
  
  /* get the index of middle element of arr[low..high]*/
  mid = (low + high)/2;  /* low + (high - low)/2 */
  
  /* If x is same as middle element, then return mid */
  if(arr[mid] == x) 
    return mid; 
      
  /* If x is greater than arr[mid], then either arr[mid + 1] 
    is ceiling of x or ceiling lies in arr[mid+1...high] */  
  else if(arr[mid] < x) 
  { 
    if(mid + 1 <= high && x <= arr[mid+1]) 
      return mid + 1; 
    else 
      return ceilSearch(arr, mid+1, high, x); 
  } 
  
  /* If x is smaller than arr[mid], then either arr[mid]  
     is ceiling of x or ceiling lies in arr[low...mid-1] */    
  else
  { 
    if(mid - 1 >= low && x > arr[mid-1]) 
      return mid; 
    else     
      return ceilSearch(arr, low, mid - 1, x); 
  } 
} 
  
/* Driver program to check above functions */
int main() 
{ 
   int arr[] = {1, 2, 8, 10, 10, 12, 19}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   int x = 20; 
   int index = ceilSearch(arr, 0, n-1, x); 
   if(index == -1) 
     printf("Ceiling of %d doesn't exist in array ", x); 
   else  
     printf("ceiling of %d is %d", x, arr[index]); 
   getchar(); 
   return 0; 
} 
```

## Java

```java
class Main 
{ 
    /* Function to get index of  
       ceiling of x in arr[low..high]*/
    static int ceilSearch(int arr[], int low, int high, int x) 
    { 
      int mid;     
        
      /* If x is smaller than or equal to the  
         first element, then return the first element */
      if(x <= arr[low]) 
        return low;  
       
      /* If x is greater than the last  
         element, then return -1 */
      if(x > arr[high]) 
        return -1;   
       
      /* get the index of middle element  
         of arr[low..high]*/
      mid = (low + high)/2;  /* low + (high - low)/2 */
       
      /* If x is same as middle element,  
         then return mid */
      if(arr[mid] == x) 
        return mid; 
           
      /* If x is greater than arr[mid], then  
         either arr[mid + 1] is ceiling of x or  
         ceiling lies in arr[mid+1...high] */ 
      else if(arr[mid] < x) 
      { 
        if(mid + 1 <= high && x <= arr[mid+1]) 
          return mid + 1; 
        else
          return ceilSearch(arr, mid+1, high, x); 
      } 
       
      /* If x is smaller than arr[mid],  
         then either arr[mid] is ceiling of x  
         or ceiling lies in arr[low...mid-1] */   
      else
      { 
        if(mid - 1 >= low && x > arr[mid-1]) 
          return mid; 
        else    
          return ceilSearch(arr, low, mid - 1, x); 
      } 
    } 
       
       
    /* Driver program to check above functions */
    public static void main (String[] args) 
    { 
       int arr[] = {1, 2, 8, 10, 10, 12, 19}; 
       int n = arr.length; 
       int x = 8; 
       int index = ceilSearch(arr, 0, n-1, x); 
       if(index == -1) 
         System.out.println("Ceiling of "+x+" doesn't exist in array"); 
       else 
         System.out.println("ceiling of "+x+" is "+arr[index]); 
    }   
} 
```

## Python3

```py
# Function to get index of ceiling of x in arr[low..high]*/ 
def ceilSearch(arr, low, high, x): 
  
    # If x is smaller than or equal to the first element, 
    # then return the first element */ 
    if x <= arr[low]: 
        return low  
  
    # If x is greater than the last element, then return -1 */ 
    if x > arr[high]: 
        return -1  
   
    # get the index of middle element of arr[low..high]*/ 
    mid = (low + high)/2;  # low + (high - low)/2 */ 
   
    # If x is same as middle element, then return mid */ 
    if arr[mid] == x: 
        return mid 
  
    # If x is greater than arr[mid], then either arr[mid + 1] 
    # is ceiling of x or ceiling lies in arr[mid+1...high] */  
    elif arr[mid] < x: 
        if mid + 1 <= high and x <= arr[mid+1]: 
            return mid + 1
        else: 
            return ceilSearch(arr, mid+1, high, x) 
   
    # If x is smaller than arr[mid], then either arr[mid]  
    # is ceiling of x or ceiling lies in arr[low...mid-1] */    
    else: 
        if mid - 1 >= low and x > arr[mid-1]: 
            return mid 
        else: 
            return ceilSearch(arr, low, mid - 1, x) 
   
# Driver program to check above functions */ 
arr = [1, 2, 8, 10, 10, 12, 19] 
n = len(arr) 
x = 20
index = ceilSearch(arr, 0, n-1, x); 
  
if index == -1: 
    print ("Ceiling of %d doesn't exist in array "% x) 
else: 
    print ("ceiling of %d is %d"%(x, arr[index])) 
  
# This code is contributed by Shreyanshi Arun 
```

## C#

```cs
// C# program to find celing 
// in a sorted array 
using System; 
  
class GFG { 
      
    // Function to get index of ceiling 
    // of x in arr[low..high] 
    static int ceilSearch(int[] arr, int low,  
                             int high, int x) 
    { 
        int mid; 
  
        // If x is smaller than or equal  
        // to the first element, then  
        // return the first element. 
        if (x <= arr[low]) 
            return low; 
  
        // If x is greater than the last  
        // element, then return -1  
        if (x > arr[high]) 
            return -1; 
  
        // get the index of middle   
        // element of arr[low..high] 
        mid = (low + high) / 2;  
        // low + (high - low)/2  
  
        // If x is same as middle   
        // element then return mid  
        if (arr[mid] == x) 
            return mid; 
  
        // If x is greater than arr[mid],   
        // then either arr[mid + 1] is 
        // ceiling of x or ceiling lies 
        // in arr[mid+1...high]  
        else if (arr[mid] < x) { 
            if (mid + 1 <= high && x <= arr[mid + 1]) 
                return mid + 1; 
            else
                return ceilSearch(arr, mid + 1, high, x); 
        } 
  
        // If x is smaller than arr[mid],  
        // then either arr[mid] is ceiling  
        // of x  or ceiling lies in  
        // arr[low...mid-1]  
        else { 
            if (mid - 1 >= low && x > arr[mid - 1]) 
                return mid; 
            else
                return ceilSearch(arr, low, mid - 1, x); 
        } 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 8, 10, 10, 12, 19 }; 
        int n = arr.Length; 
        int x = 8; 
        int index = ceilSearch(arr, 0, n - 1, x); 
        if (index == -1) 
            Console.Write("Ceiling of " + x + 
                      " doesn't exist in array"); 
        else
            Console.Write("ceiling of " + x +  
                            " is " + arr[index]); 
    } 
} 
  
// This code is contributed by Sam007. 
```

## PHP

```php
<?php 
// PHP Program for Ceiling in  
// a sorted array 
  
// Function to get index of ceiling 
// of x in arr[low..high] 
function ceilSearch($arr, $low,  
                    $high, $x) 
{ 
    $mid;  
      
    /* If x is smaller than or  
       equal to the first element, 
       then return the first element */
    if($x <= $arr[$low]) 
        return $low;  
      
    /* If x is greater than the 
       last element, then return 
       -1 */
    if($x > $arr[$high]) 
        return -1;  
      
    /* get the index of middle 
       element of arr[low..high] */
    // low + (high - low)/2 
    $mid = ($low + $high)/2;  
      
    /* If x is same as middle element, 
       then return mid */
    if($arr[$mid] == $x) 
        return $mid; 
          
    /* If x is greater than arr[mid], 
       then either arr[mid + 1]    is  
       ceiling of x or ceiling lies  
       in arr[mid+1...high] */
    else if($arr[$mid] < $x) 
    { 
        if($mid + 1 <= $high &&  
           $x <= $arr[$mid + 1]) 
            return $mid + 1; 
        else
            return ceilSearch($arr, $mid + 1,  
                              $high, $x); 
    } 
      
    /* If x is smaller than arr[mid], 
       then either arr[mid] is ceiling 
       of x or ceiling lies in  
       arr[low....mid-1] */
    else
    { 
        if($mid - 1 >= $low &&  
           $x > $arr[$mid - 1]) 
            return $mid; 
        else
         return ceilSearch($arr, $low,  
                           $mid - 1, $x); 
    } 
} 
  
// Driver Code 
$arr = array(1, 2, 8, 10, 10, 12, 19); 
$n = sizeof($arr); 
$x = 20; 
$index = ceilSearch($arr, 0, $n - 1, $x); 
if($index == -1) 
    echo("Ceiling of $x doesn't exist in array "); 
else
    echo("ceiling of $x is");  
    echo(isset($arr[$index])); 
  
// This code is contributed by nitin mittal. 
?> 
```

输出：

```
Ceiling of 20 doesn't exist in array 
```

时间复杂度：`O(Logn)`。
