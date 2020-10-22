# 在先增加然后减少的数组中找到最大元素

> 原文： [https://www.geeksforgeeks.org/find-the-maximum-element-in-an-array-which-is-first-increasing-and-then-decreasing/](https://www.geeksforgeeks.org/find-the-maximum-element-in-an-array-which-is-first-increasing-and-then-decreasing/)

给定一个整数数组，该数组最初是递增的，然后递减的，请在该数组中找到最大值。

**示例**：

```
Input: arr[] = {8, 10, 20, 80, 100, 200, 400, 500, 3, 2, 1}
Output: 500

Input: arr[] = {1, 3, 50, 10, 9, 7, 6}
Output: 50

Corner case (No decreasing part)
Input: arr[] = {10, 20, 30, 40, 50}
Output: 50

Corner case (No increasing part)
Input: arr[] = {120, 100, 80, 20, 0}
Output: 120

```



**方法 1（线性搜索）**：

我们可以遍历数组并跟踪最大值和元素。 最后返回最大元素。

## C++ 

```cpp

// C++ program to find maximum  
// element  
#include <bits/stdc++.h> 
using namespace std; 

// function to find the maximum element  
int findMaximum(int arr[], int low, int high)  
{  
    int max = arr[low];  
    int i;  
    for (i = low + 1; i <= high; i++)  
    {  
        if (arr[i] > max)  
            max = arr[i];  

        // break when once an element is smaller than  
        // the max then it will go on decreasing  
        // and no need to check after that  
        else
            break;  
    }  
    return max;  
}  

/* Driver code*/
int main()  
{  
    int arr[] = {1, 30, 40, 50, 60, 70, 23, 20};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    cout << "The maximum element is " << findMaximum(arr, 0, n-1);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## Java

```java
// java program to find maximum 
// element 
  
class Main 
{    
    // function to find the  
    // maximum element 
    static int findMaximum(int arr[], int low, int high) 
    { 
       int max = arr[low]; 
       int i; 
       for (i = low; i <= high; i++) 
       { 
           if (arr[i] > max) 
              max = arr[i]; 
       } 
       return max; 
    } 
      
    // main function 
    public static void main (String[] args)  
    { 
        int arr[] = {1, 30, 40, 50, 60, 70, 23, 20}; 
        int n = arr.length; 
        System.out.println("The maximum element is "+  
                            findMaximum(arr, 0, n-1)); 
    } 
}
```

## Python3

```py
# Python3 program to find  
# maximum element 
  
def findMaximum(arr, low, high): 
    max = arr[low] 
    i = low 
    for i in range(high+1): 
        if arr[i] > max: 
            max = arr[i] 
    return max
  
# Driver program to check above functions */ 
arr = [1, 30, 40, 50, 60, 70, 23, 20] 
n = len(arr) 
print ("The maximum element is %d"% 
        findMaximum(arr, 0, n-1)) 
  
# This code is contributed by Shreyanshi Arun.
```

## C#

```cs
// C# program to find maximum 
// element 
using System; 
  
class GFG 
{ 
    // function to find the  
    // maximum element 
    static int findMaximum(int []arr, int low, int high) 
    { 
        int max = arr[low]; 
        int i; 
        for (i = low; i <= high; i++) 
        { 
            if (arr[i] > max) 
                max = arr[i]; 
        } 
        return max; 
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int []arr = {1, 30, 40, 50, 60, 70, 23, 20}; 
        int n = arr.Length; 
        Console.Write("The maximum element is "+  
                        findMaximum(arr, 0, n-1)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to Find the maximum  
// element in an array which is first 
// increasing and then decreasing 
  
function findMaximum($arr, $low, $high) 
{ 
$max = $arr[$low]; 
$i; 
for ($i = $low; $i <= $high; $i++) 
{ 
    if ($arr[$i] > $max) 
        $max = $arr[$i]; 
} 
return $max; 
} 
  
// Driver Code 
$arr = array(1, 30, 40, 50,  
             60, 70, 23, 20); 
$n = count($arr); 
echo "The maximum element is ",  
      findMaximum($arr, 0, $n-1); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
The maximum element is 70
```

时间复杂度：`O(n)`。

方法 2（二进制搜索）：

我们可以为给定类型的数组修改标准的二进制搜索算法。

1.  如果`mid`元素大于其两个相邻元素，则`mid`是最大值。
2.  如果`mid`元素大于其下一个元素且小于前一个元素，则最大值位于`mid`的左侧。 数组示例：`{3, 50, 10, 9, 7, 6}`。
3.  如果`mid`元素小于其下一个元素且大于前一个元素，则最大值位于`mid`的右侧。 数组示例：`{2, 4, 6, 8, 10, 3, 1}`。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std; 
  
int findMaximum(int arr[], int low, int high)  
{  
  
    /* Base Case: Only one element is present in arr[low..high]*/
    if (low == high)  
        return arr[low];  
      
    /* If there are two elements and first is greater then  
        the first element is maximum */
    if ((high == low + 1) && arr[low] >= arr[high])  
        return arr[low];  
      
    /* If there are two elements and second is greater then  
        the second element is maximum */
    if ((high == low + 1) && arr[low] < arr[high])  
        return arr[high];  
      
    int mid = (low + high)/2; /*low + (high - low)/2;*/
      
    /* If we reach a point where arr[mid] is greater than both of  
        its adjacent elements arr[mid-1] and arr[mid+1], then arr[mid]  
        is the maximum element*/
    if ( arr[mid] > arr[mid + 1] && arr[mid] > arr[mid - 1])  
        return arr[mid];  
      
    /* If arr[mid] is greater than the next 
        element and smaller than the previous  
        element then maximum lies on left side of mid */
    if (arr[mid] > arr[mid + 1] && arr[mid] < arr[mid - 1])  
        return findMaximum(arr, low, mid-1);  
          
        // when arr[mid] is greater than arr[mid-1] 
        // and smaller than arr[mid+1] 
    else 
        return findMaximum(arr, mid + 1, high);  
}  
  
/* Driver code */
int main()  
{  
    int arr[] = {1, 3, 50, 10, 9, 7, 6};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    cout << "The maximum element is " << findMaximum(arr, 0, n-1);  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra
```

## C

```c
#include <stdio.h> 
  
int findMaximum(int arr[], int low, int high) 
{ 
  
   /* Base Case: Only one element is present in arr[low..high]*/
   if (low == high) 
     return arr[low]; 
  
   /* If there are two elements and first is greater then 
      the first element is maximum */
   if ((high == low + 1) && arr[low] >= arr[high]) 
      return arr[low]; 
  
   /* If there are two elements and second is greater then 
      the second element is maximum */
   if ((high == low + 1) && arr[low] < arr[high]) 
      return arr[high]; 
  
   int mid = (low + high)/2;   /*low + (high - low)/2;*/
  
   /* If we reach a point where arr[mid] is greater than both of 
     its adjacent elements arr[mid-1] and arr[mid+1], then arr[mid] 
     is the maximum element*/
   if ( arr[mid] > arr[mid + 1] && arr[mid] > arr[mid - 1]) 
      return arr[mid]; 
  
   /* If arr[mid] is greater than the next element and smaller than the previous  
    element then maximum lies on left side of mid */
   if (arr[mid] > arr[mid + 1] && arr[mid] < arr[mid - 1]) 
     return findMaximum(arr, low, mid-1); 
   else // when arr[mid] is greater than arr[mid-1] and smaller than arr[mid+1] 
     return findMaximum(arr, mid + 1, high); 
} 
  
/* Driver program to check above functions */
int main() 
{ 
   int arr[] = {1, 3, 50, 10, 9, 7, 6}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   printf("The maximum element is %d", findMaximum(arr, 0, n-1)); 
   getchar(); 
   return 0; 
}
```

## Java

```java
// java program to find maximum 
// element 
  
class Main 
{    
    // function to find the  
    // maximum element 
    static int findMaximum(int arr[], int low, int high) 
    { 
       
       /* Base Case: Only one element is  
          present in arr[low..high]*/
       if (low == high) 
         return arr[low]; 
       
       /* If there are two elements and  
          first is greater then the first  
          element is maximum */
       if ((high == low + 1) && arr[low] >= arr[high]) 
          return arr[low]; 
       
       /* If there are two elements and  
          second is greater then the second  
          element is maximum */
       if ((high == low + 1) && arr[low] < arr[high]) 
          return arr[high]; 
          
       /*low + (high - low)/2;*/
       int mid = (low + high)/2;    
       
       /* If we reach a point where arr[mid]  
          is greater than both of its adjacent  
          elements arr[mid-1] and arr[mid+1],  
          then arr[mid] is the maximum element*/
       if ( arr[mid] > arr[mid + 1] && arr[mid] > arr[mid - 1]) 
          return arr[mid]; 
       
       /* If arr[mid] is greater than the next  
          element and smaller than the previous  
          element then maximum lies on left side  
          of mid */
       if (arr[mid] > arr[mid + 1] && arr[mid] < arr[mid - 1]) 
         return findMaximum(arr, low, mid-1); 
       else 
         return findMaximum(arr, mid + 1, high); 
    } 
      
    // main function 
    public static void main (String[] args)  
    { 
        int arr[] = {1, 3, 50, 10, 9, 7, 6}; 
        int n = arr.length; 
        System.out.println("The maximum element is "+  
                            findMaximum(arr, 0, n-1)); 
    } 
}
```

## Python3

```py
def findMaximum(arr, low, high): 
    # Base Case: Only one element is present in arr[low..high]*/ 
    if low == high: 
        return arr[low] 
   
    # If there are two elements and first is greater then 
    # the first element is maximum */ 
    if high == low + 1 and arr[low] >= arr[high]: 
        return arr[low]; 
   
    # If there are two elements and second is greater then 
    # the second element is maximum */ 
    if high == low + 1 and arr[low] < arr[high]: 
        return arr[high] 
   
    mid = (low + high)//2   #low + (high - low)/2;*/ 
   
    # If we reach a point where arr[mid] is greater than both of 
    # its adjacent elements arr[mid-1] and arr[mid+1], then arr[mid] 
    # is the maximum element*/ 
    if arr[mid] > arr[mid + 1] and arr[mid] > arr[mid - 1]: 
        return arr[mid] 
   
    # If arr[mid] is greater than the next element and smaller than the previous  
    # element then maximum lies on left side of mid */ 
    if arr[mid] > arr[mid + 1] and arr[mid] < arr[mid - 1]: 
        return findMaximum(arr, low, mid-1) 
    else: # when arr[mid] is greater than arr[mid-1] and smaller than arr[mid+1] 
        return findMaximum(arr, mid + 1, high) 
   
# Driver program to check above functions */ 
arr = [1, 3, 50, 10, 9, 7, 6] 
n = len(arr) 
print ("The maximum element is %d"% findMaximum(arr, 0, n-1)) 
  
# This code is contributed by Shreyanshi Arun.
```

## C#

```cs
// C# program to find maximum 
// element 
using System; 
  
class GFG 
{ 
    // function to find the  
    // maximum element 
    static int findMaximum(int []arr, int low, int high) 
    { 
      
    /* Base Case: Only one element is  
        present in arr[low..high]*/
    if (low == high) 
        return arr[low]; 
      
    /* If there are two elements and  
        first is greater then the first  
        element is maximum */
    if ((high == low + 1) && arr[low] >= arr[high]) 
        return arr[low]; 
      
    /* If there are two elements and  
        second is greater then the second  
        element is maximum */
    if ((high == low + 1) && arr[low] < arr[high]) 
        return arr[high]; 
          
    /*low + (high - low)/2;*/
    int mid = (low + high)/2;  
      
    /* If we reach a point where arr[mid]  
        is greater than both of its adjacent  
        elements arr[mid-1] and arr[mid+1],  
        then arr[mid] is the maximum element*/
    if ( arr[mid] > arr[mid + 1] && arr[mid] > arr[mid - 1]) 
        return arr[mid]; 
      
    /* If arr[mid] is greater than the next  
        element and smaller than the previous  
        element then maximum lies on left side  
        of mid */
    if (arr[mid] > arr[mid + 1] && arr[mid] < arr[mid - 1]) 
        return findMaximum(arr, low, mid-1); 
    else
        return findMaximum(arr, mid + 1, high); 
    } 
      
    // main function 
    public static void Main()  
    { 
        int []arr = {1, 3, 50, 10, 9, 7, 6}; 
        int n = arr.Length; 
        Console.Write("The maximum element is "+  
                            findMaximum(arr, 0, n-1)); 
    } 
} 
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to Find the maximum  
// element in an array which is  
// first increasing and then decreasing 
  
function findMaximum($arr, $low, $high) 
{ 
  
    /* Base Case: Only one element  
       is present in arr[low..high]*/
    if ($low == $high) 
        return $arr[$low]; 
      
    /* If there are two elements  
       and first is greater then 
       the first element is maximum */
    if (($high == $low + 1) &&  
        $arr[$low] >= $arr[$high]) 
        return $arr[$low]; 
      
    /* If there are two elements 
       and second is greater then 
       the second element is maximum */
    if (($high == $low + 1) &&  
         $arr[$low] < $arr[$high]) 
        return $arr[$high]; 
      
    /*low + (high - low)/2;*/
    $mid = ($low + $high) / 2;  
      
    /* If we reach a point where 
       arr[mid] is greater than 
       both of its adjacent elements 
       arr[mid-1] and arr[mid+1], 
       then arr[mid] is the maximum 
       element */
    if ( $arr[$mid] > $arr[$mid + 1] && 
         $arr[$mid] > $arr[$mid - 1]) 
        return $arr[$mid]; 
      
    /* If arr[mid] is greater than  
       the next element and smaller  
       than the previous element then 
       maximum lies on left side of mid */
    if ($arr[$mid] > $arr[$mid + 1] &&  
        $arr[$mid] < $arr[$mid - 1]) 
        return findMaximum($arr, $low, $mid - 1); 
      
    // when arr[mid] is greater than  
    // arr[mid-1] and smaller than 
    // arr[mid+1]     
    else 
        return findMaximum($arr,  
                           $mid + 1, $high); 
} 
  
// Driver Code 
$arr = array(1, 3, 50, 10, 9, 7, 6); 
$n = sizeof($arr); 
echo("The maximum element is ");  
echo(findMaximum($arr, 0, $n-1)); 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
The maximum element is 50
```

时间复杂度：`O(logn)`。

此方法仅适用于不同的数字。 例如，它不适用于`{0, 1, 1, 2, 2, 2, 2, 2, 3, 4, 4, 5, 3, 3, 2, 2, 1, 1}`这样的数组。