# 查找数组中的最小和第二个最小元素

> 原文： [https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

编写高效的 C 程序以查找数组中的最小和第二个最小元素。

![](img/111eac0cedd7eba13b40b5ba82b67845.png)

**示例**：

```
Input:  arr[] = {12, 13, 1, 10, 34, 1}
Output: The smallest element is 1 and 
        second Smallest element is 10

```



**简单解决方案**是按递增顺序对数组进行排序。 排序数组中的前两个元素将是两个最小的元素。 该解决方案的时间复杂度为`O(N log N)`。

**更好的解决方案**是扫描数组两次。 在第一次遍历中找到最小元素。 将此元素设为`x`。 在第二遍历中，找到大于`x`的最小元素。 该解决方案的时间复杂度为`O(n)`。

上面的解决方案需要两次遍历输入数组。

**有效解决方案**可以在一次遍历中找到最少两个元素。 下面是完整的算法。

**算法**：

```
1) Initialize both first and second smallest as INT_MAX
   *first* = *second* = INT_MAX
2) Loop through all the elements.
   a) If the current element is smaller than *first*, then update *first* 
       and *second*. 
   b) Else if the current element is smaller than *second* then update 
    *second*
```

**实现**：

## C++ 

```cpp

// C++ program to find smallest and  
// second smallest elements  
#include <bits/stdc++.h> 
using namespace std; /* For INT_MAX */

void print2Smallest(int arr[], int arr_size)  
{  
    int i, first, second;  

    /* There should be atleast two elements */
    if (arr_size < 2)  
    {  
        cout<<" Invalid Input ";  
        return;  
    }  

    first = second = INT_MAX;  
    for (i = 0; i < arr_size ; i ++)  
    {  
        /* If current element is smaller than first  
        then update both first and second */
        if (arr[i] < first)  
        {  
            second = first;  
            first = arr[i];  
        }  

        /* If arr[i] is in between first and second  
        then update second */
        else if (arr[i] < second && arr[i] != first)  
            second = arr[i];  
    }  
    if (second == INT_MAX)  
        cout << "There is no second smallest element\n";  
    else
        cout << "The smallest element is " << first << " and second "
            "Smallest element is " << second << endl;  
}  

/* Driver code */
int main()  
{  
    int arr[] = {12, 13, 1, 10, 34, 1};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    print2Smallest(arr, n);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c
// C program to find smallest and second smallest elements 
#include <stdio.h> 
#include <limits.h> /* For INT_MAX */ 
  
void print2Smallest(int arr[], int arr_size) 
{ 
    int i, first, second; 
  
    /* There should be atleast two elements */
    if (arr_size < 2) 
    { 
        printf(" Invalid Input "); 
        return; 
    } 
  
    first = second = INT_MAX; 
    for (i = 0; i < arr_size ; i ++) 
    { 
        /* If current element is smaller than first  
           then update both first and second */
        if (arr[i] < first) 
        { 
            second = first; 
            first = arr[i]; 
        } 
  
        /* If arr[i] is in between first and second  
           then update second  */
        else if (arr[i] < second && arr[i] != first) 
            second = arr[i]; 
    } 
    if (second == INT_MAX) 
        printf("There is no second smallest element\n"); 
    else
        printf("The smallest element is %d and second "
               "Smallest element is %d\n", first, second); 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr[] = {12, 13, 1, 10, 34, 1}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    print2Smallest(arr, n); 
    return 0; 
} 
```

## Java

```java
// Java program to find smallest and second smallest elements 
import java.io.*; 
  
class SecondSmallest 
{ 
    /* Function to print first smallest and second smallest 
      elements */
    static void print2Smallest(int arr[]) 
    { 
        int first, second, arr_size = arr.length; 
  
        /* There should be atleast two elements */
        if (arr_size < 2) 
        { 
            System.out.println(" Invalid Input "); 
            return; 
        } 
  
        first = second = Integer.MAX_VALUE; 
        for (int i = 0; i < arr_size ; i ++) 
        { 
            /* If current element is smaller than first 
              then update both first and second */
            if (arr[i] < first) 
            { 
                second = first; 
                first = arr[i]; 
            } 
  
            /* If arr[i] is in between first and second 
               then update second  */
            else if (arr[i] < second && arr[i] != first) 
                second = arr[i]; 
        } 
        if (second == Integer.MAX_VALUE) 
            System.out.println("There is no second" + 
                               "smallest element"); 
        else
            System.out.println("The smallest element is " + 
                               first + " and second Smallest" + 
                               " element is " + second); 
    } 
  
    /* Driver program to test above functions */
    public static void main (String[] args) 
    { 
        int arr[] = {12, 13, 1, 10, 34, 1}; 
        print2Smallest(arr); 
    } 
} 
/*This code is contributed by Devesh Agrawal*/
```

## Python

```py
# Python program to find smallest and second smallest elements 
import sys 
  
def print2Smallest(arr): 
  
    # There should be atleast two elements 
    arr_size = len(arr) 
    if arr_size < 2: 
        print "Invalid Input"
        return
  
    first = second = sys.maxint 
    for i in range(0, arr_size): 
  
        # If current element is smaller than first then 
        # update both first and second 
        if arr[i] < first: 
            second = first 
            first = arr[i] 
  
        # If arr[i] is in between first and second then 
        # update second 
        elif (arr[i] < second and arr[i] != first): 
            second = arr[i]; 
  
    if (second == sys.maxint): 
        print "No second smallest element"
    else: 
        print 'The smallest element is',first,'and' \ 
              ' second smallest element is',second 
  
# Driver function to test above function 
arr = [12, 13, 1, 10, 34, 1] 
print2Smallest(arr) 
  
# This code is contributed by Devesh Agrawal 
```

## C#

```cs
// C# program to find smallest 
// and second smallest elements 
using System; 
  
class GFG 
{ 
      
    /* Function to print first smallest  
     and second smallest elements */
    static void print2Smallest(int []arr) 
    { 
        int first, second, arr_size = arr.Length; 
  
        /* There should be atleast two elements */
        if (arr_size < 2) 
        { 
            Console.Write(" Invalid Input "); 
            return; 
        } 
  
        first = second = int.MaxValue; 
          
        for (int i = 0; i < arr_size ; i ++) 
        { 
            /* If current element is smaller than first 
            then update both first and second */
            if (arr[i] < first) 
            { 
                second = first; 
                first = arr[i]; 
            } 
  
            /* If arr[i] is in between first and second 
            then update second */
            else if (arr[i] < second && arr[i] != first) 
                second = arr[i]; 
        } 
        if (second == int.MaxValue) 
            Console.Write("There is no second" + 
                            "smallest element"); 
        else
            Console.Write("The smallest element is " + 
                            first + " and second Smallest" + 
                            " element is " + second); 
    } 
  
    /* Driver program to test above functions */
    public static void Main() 
    { 
        int []arr = {12, 13, 1, 10, 34, 1}; 
        print2Smallest(arr); 
    }  
} 
  
// This code is contributed by Sam007 
```

## PHP

```php
<?php 
// PHP  program to find smallest and 
// second smallest elements 
  
function print2Smallest($arr, $arr_size) 
{ 
    $INT_MAX = 2147483647; 
      
    /* There should be atleast  
       two elements */
    if ($arr_size < 2) 
    { 
        echo(" Invalid Input "); 
        return; 
    } 
  
    $first = $second = $INT_MAX; 
    for ($i = 0; $i < $arr_size ; $i ++) 
    { 
          
        /* If current element is 
           smaller than first then 
           update both first and 
           second */
        if ($arr[$i] < $first) 
        { 
            $second = $first; 
            $first = $arr[$i]; 
        } 
  
        /* If arr[i] is in between 
           first and second then  
           update second */
        else if ($arr[$i] < $second &&  
                 $arr[$i] != $first) 
            $second = $arr[$i]; 
    } 
    if ($second == $INT_MAX) 
        echo("There is no second smallest element\n"); 
    else
        echo "The smallest element is ",$first
             ," and second Smallest element is "
                                     , $second; 
} 
  
// Driver Code 
$arr = array(12, 13, 1, 10, 34, 1); 
$n = count($arr); 
print2Smallest($arr, $n) 
  
// This code is contributed by Smitha 
?> 
```

输出：

```
The smallest element is 1 and second Smallest element is 10
```

可以使用相同的方法在数组中查找最大和第二大元素。

时间复杂度：`O(n)`。