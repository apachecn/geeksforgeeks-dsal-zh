# 给定一个经过排序和旋转的数组，查找是否存在具有给定总和的偶对

> 原文： [https://www.geeksforgeeks.org/given-a-sorted-and-rotated-array-find-if-there-is-a-pair-with-a-given-sum/](https://www.geeksforgeeks.org/given-a-sorted-and-rotated-array-find-if-there-is-a-pair-with-a-given-sum/)

给定一个已排序的数组，然后围绕未知点旋转。 查找数组是否具有给定总和为`x`的对。 可以假定数组中的所有元素都是不同的。

**示例**：

```
Input: arr[] = {11, 15, 6, 8, 9, 10}, x = 16
Output: true
There is a pair (6, 10) with sum 16

Input: arr[] = {11, 15, 26, 38, 9, 10}, x = 35
Output: true
There is a pair (26, 9) with sum 35

Input: arr[] = {11, 15, 26, 38, 9, 10}, x = 45
Output: false
There is no pair with sum 45.

```



我们已经讨论了用于排序数组的[`O(n)`解（请参见方法 1 的步骤 2、3 和 4）](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)。 我们也可以将此解决方案扩展到旋转数组。 这个想法是首先找到数组中最大的元素，它也是枢轴点，紧随其后的元素是最小的元素。 一旦我们有了最大和最小元素的索引，就可以在中间算法（如方法 1 中的[这里](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)讨论的）中使用类似的 Meet 来查找是否存在一对。 唯一的新变化是使用模块化算法以循环方式递增和递减索引。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to find a pair with a given sum in a sorted and 
// rotated array 
#include<iostream> 
using namespace std; 

// This function returns true if arr[0..n-1] has a pair 
// with sum equals to x. 
bool pairInSortedRotated(int arr[], int n, int x) 
{ 
    // Find the pivot element 
    int i; 
    for (i=0; i<n-1; i++) 
        if (arr[i] > arr[i+1]) 
            break; 
    int l = (i+1)%n;  // l is now index of smallest element 
    int r = i;        // r is now index of largest element 

    // Keep moving either l or r till they meet 
    while (l != r) 
    { 
         // If we find a pair with sum x, we return true 
         if (arr[l] + arr[r] == x) 
              return true; 

         // If current pair sum is less, move to the higher sum 
         if (arr[l] + arr[r] < x) 
              l = (l + 1)%n; 
         else  // Move to the lower sum side 
              r = (n + r - 1)%n; 
    } 
    return false; 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {11, 15, 6, 8, 9, 10}; 
    int sum = 16; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    if (pairInSortedRotated(arr, n, sum)) 
        cout << "Array has two elements with sum 16"; 
    else
        cout << "Array doesn't have two elements with sum 16 "; 

    return 0; 
} 

```

## Java

```java
// Java program to find a pair with a given  
// sum in a sorted and rotated array 
class PairInSortedRotated 
{ 
    // This function returns true if arr[0..n-1]  
    // has a pair with sum equals to x. 
    static boolean pairInSortedRotated(int arr[],  
                                    int n, int x) 
    { 
        // Find the pivot element 
        int i; 
        for (i = 0; i < n - 1; i++) 
            if (arr[i] > arr[i+1]) 
                break; 
                  
        int l = (i + 1) % n; // l is now index of                                           
                            // smallest element 
                           
        int r = i;       // r is now index of largest  
                         //element 
       
        // Keep moving either l or r till they meet 
        while (l != r) 
        { 
             // If we find a pair with sum x, we 
             // return true 
             if (arr[l] + arr[r] == x) 
                  return true; 
       
             // If current pair sum is less, move  
             // to the higher sum 
             if (arr[l] + arr[r] < x) 
                  l = (l + 1) % n; 
                    
             else  // Move to the lower sum side 
                  r = (n + r - 1) % n; 
        } 
        return false; 
    } 
  
    /* Driver program to test above function */
    public static void main (String[] args) 
    { 
        int arr[] = {11, 15, 6, 8, 9, 10}; 
        int sum = 16; 
        int n = arr.length; 
       
        if (pairInSortedRotated(arr, n, sum)) 
            System.out.print("Array has two elements" + 
                             " with sum 16"); 
        else
            System.out.print("Array doesn't have two" +  
                             " elements with sum 16 "); 
    } 
} 
/*This code is contributed by Prakriti Gupta*/
```

## Python3

```py
# Python3 program to find a  
# pair with a given sum in 
# a sorted and rotated array 
  
  
# This function returns True  
# if arr[0..n-1] has a pair 
# with sum equals to x. 
def pairInSortedRotated( arr, n, x ): 
      
    # Find the pivot element 
    for i in range(0, n - 1): 
        if (arr[i] > arr[i + 1]): 
            break; 
              
    # l is now index of smallest element         
    l = (i + 1) % n 
    # r is now index of largest element 
    r = i      
  
    # Keep moving either l  
    # or r till they meet 
    while (l != r): 
          
        # If we find a pair with  
        # sum x, we return True 
        if (arr[l] + arr[r] == x): 
            return True; 
              
        # If current pair sum is less, 
        # move to the higher sum 
        if (arr[l] + arr[r] < x): 
            l = (l + 1) % n; 
        else: 
              
            # Move to the lower sum side 
            r = (n + r - 1) % n; 
      
    return False; 
  
  
# Driver program to test above function  
arr = [11, 15, 6, 8, 9, 10] 
sum = 16
n = len(arr) 
  
if (pairInSortedRotated(arr, n, sum)): 
    print ("Array has two elements with sum 16") 
else: 
    print ("Array doesn't have two elements with sum 16 ") 
  
      
# This article contributed by saloni1297 
```

## C#

```cs
// C# program to find a pair with a given  
// sum in a sorted and rotated array 
using System; 
  
class PairInSortedRotated 
{ 
    // This function returns true if arr[0..n-1]  
    // has a pair with sum equals to x. 
    static bool pairInSortedRotated(int []arr,  
                                    int n, int x) 
    { 
        // Find the pivot element 
        int i; 
        for (i = 0; i < n - 1; i++) 
            if (arr[i] > arr[i + 1]) 
                break; 
                  
        // l is now index of smallest element         
        int l = (i + 1) % n;  
          
        // r is now index of largest element                 
        int r = i;  
      
        // Keep moving either l or r till they meet 
        while (l != r) 
        { 
            // If we find a pair with sum x, we 
            // return true 
            if (arr[l] + arr[r] == x) 
                return true; 
      
            // If current pair sum is less,   
            // move to the higher sum 
            if (arr[l] + arr[r] < x) 
                l = (l + 1) % n; 
              
            // Move to the lower sum side     
            else 
                r = (n + r - 1) % n; 
        } 
        return false; 
    } 
  
    // Driver Code 
    public static void Main () 
    { 
        int []arr = {11, 15, 6, 8, 9, 10}; 
        int sum = 16; 
        int n = arr.Length; 
      
        if (pairInSortedRotated(arr, n, sum)) 
            Console.WriteLine("Array has two elements" + 
                                       " with sum 16"); 
        else
        Console.WriteLine("Array doesn't have two" +  
                            " elements with sum 16 "); 
    } 
} 
  
// This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP program to find a pair 
// with a given sum in a 
// sorted and rotated array 
  
// This function returns true 
// if arr[0..n-1] has a pair  
// with sum equals to x. 
  
function pairInSortedRotated($arr, $n, $x) 
{ 
    // Find the pivot element 
    $i; 
    for ($i = 0; $i < $n - 1; $i++) 
        if ($arr[$i] > $arr[$i + 1]) 
            break; 
          
    // l is now index of  
    // smallest element 
    $l = ($i + 1) % $n;  
      
    // r is now index of 
    // largest element 
    $r = $i; 
  
    // Keep moving either l  
    // or r till they meet 
    while ($l != $r) 
    { 
        // If we find a pair with 
        // sum x, we return true 
        if ($arr[$l] + $arr[$r] == $x) 
            return true; 
  
        // If current pair sum is  
        // less, move to the higher sum 
        if ($arr[$l] + $arr[$r] < $x) 
            $l = ($l + 1) % $n; 
              
        // Move to the lower sum side 
        else 
            $r = ($n + $r - 1) % $n; 
    } 
    return false; 
} 
  
// Driver Code 
$arr = array(11, 15, 6, 8, 9, 10); 
$sum = 16; 
$n = sizeof($arr); 
  
if (pairInSortedRotated($arr, $n, $sum)) 
    echo "Array has two elements ".  
                     "with sum 16"; 
else
    echo "Array doesn't have two ".  
           "elements with sum 16 "; 
  
// This code is contributed by aj_36 
?> 
```

输出：

```
Array has two elements with sum 16
```

上述解决方案的时间复杂度为`O(n)`。使用此处讨论的二分搜索方法，可以将查找枢轴的步骤优化为`O(Logn)`。

如何计算所有具有和`x`的对？

逐步算法是：

+   查找已排序和旋转数组的枢轴元素。枢轴元素是数组中最大的元素。最小的元素将与其相邻。
+   使用两个指针（例如，左和右），左指针指向最小元素，右指针指向最大元素。
+   找到两个指针所指向的元素的总和。
+   如果总和等于`x`，则增加计数。如果总和小于`x`，则要增加总和，请以旋转方式将左指针移至下一个位置。
+   如果总和大于`x`，则要减少总和，请以旋转方式将右指针递减以将其移动到下一个位置。
+   重复步骤3和4，直到左指针不等于右指针或直到左指针不等于右指针 –1。
+   打印最终计数。

下面是上述算法的实现：

## C++

```cpp
// C++ program to find number of pairs with  
// a given sum in a sorted and rotated array. 
#include<bits/stdc++.h> 
using namespace std; 
  
// This function returns count of number of pairs 
// with sum equals to x. 
int pairsInSortedRotated(int arr[], int n, int x) 
{ 
    // Find the pivot element. Pivot element 
    // is largest element of array. 
    int i; 
    for (i = 0; i < n-1; i++) 
        if (arr[i] > arr[i+1]) 
            break; 
      
    // l is index of smallest element. 
    int l = (i + 1) % n;  
      
    // r is index of largest element. 
    int r = i; 
      
    // Variable to store count of number 
    // of pairs. 
    int cnt = 0; 
  
    // Find sum of pair formed by arr[l] and 
    // and arr[r] and update l, r and cnt  
    // accordingly. 
    while (l != r) 
    { 
        // If we find a pair with sum x, then  
        // increment cnt, move l and r to  
        // next element. 
        if (arr[l] + arr[r] == x){ 
            cnt++; 
              
            // This condition is required to  
            // be checked, otherwise l and r 
            // will cross each other and loop 
            // will never terminate. 
            if(l == (r - 1 + n) % n){ 
                return cnt; 
            } 
              
            l = (l + 1) % n; 
            r = (r - 1 + n) % n; 
        } 
  
        // If current pair sum is less, move to  
        // the higher sum side. 
        else if (arr[l] + arr[r] < x) 
            l = (l + 1) % n; 
          
        // If current pair sum is greater, move  
        // to the lower sum side. 
        else 
            r = (n + r - 1)%n; 
    } 
      
    return cnt; 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr[] = {11, 15, 6, 7, 9, 10}; 
    int sum = 16; 
    int n = sizeof(arr)/sizeof(arr[0]); 
  
    cout << pairsInSortedRotated(arr, n, sum); 
      
    return 0; 
}  
```

## Java

```java
// Java program to find  
// number of pairs with  
// a given sum in a sorted  
// and rotated array. 
import java.io.*; 
  
class GFG 
{ 
      
// This function returns 
// count of number of pairs 
// with sum equals to x. 
static int pairsInSortedRotated(int arr[],  
                                int n, int x) 
{ 
    // Find the pivot element.  
    // Pivot element is largest  
    // element of array. 
    int i; 
    for (i = 0; i < n - 1; i++) 
        if (arr[i] > arr[i + 1]) 
            break; 
      
    // l is index of 
    // smallest element. 
    int l = (i + 1) % n;  
      
    // r is index of  
    // largest element. 
    int r = i; 
      
    // Variable to store 
    // count of number 
    // of pairs. 
    int cnt = 0; 
  
    // Find sum of pair  
    // formed by arr[l]  
    // and arr[r] and  
    // update l, r and  
    // cnt accordingly. 
    while (l != r) 
    { 
        // If we find a pair with  
        // sum x, then increment  
        // cnt, move l and r to  
        // next element. 
        if (arr[l] + arr[r] == x) 
        { 
            cnt++; 
              
            // This condition is required  
            // to be checked, otherwise  
            // l and r will cross each  
            // other and loop will never  
            // terminate. 
            if(l == (r - 1 + n) % n) 
            { 
                return cnt; 
            } 
              
            l = (l + 1) % n; 
            r = (r - 1 + n) % n; 
        } 
  
        // If current pair sum  
        // is less, move to  
        // the higher sum side. 
        else if (arr[l] + arr[r] < x) 
            l = (l + 1) % n; 
          
        // If current pair sum  
        // is greater, move  
        // to the lower sum side. 
        else
            r = (n + r - 1) % n; 
    } 
      
    return cnt; 
} 
  
// Driver Code 
public static void main (String[] args)  
{ 
    int arr[] = {11, 15, 6, 7, 9, 10}; 
    int sum = 16; 
    int n = arr.length; 
  
    System.out.println( 
            pairsInSortedRotated(arr, n, sum)); 
} 
} 
  
// This code is contributed by ajit 
```

## Python 3

```py
# Python program to find  
# number of pairs with  
# a given sum in a sorted  
# and rotated array. 
  
# This function returns 
# count of number of pairs 
# with sum equals to x. 
def pairsInSortedRotated(arr, n, x): 
      
    # Find the pivot element.  
    # Pivot element is largest  
    # element of array. 
    for i in range(n): 
        if arr[i] > arr[i + 1]: 
            break
      
    # l is index of 
    # smallest element. 
    l = (i + 1) % n  
      
    # r is index of  
    # largest element. 
    r = i 
      
    # Variable to store  
    # count of number 
    # of pairs. 
    cnt = 0
  
    # Find sum of pair  
    # formed by arr[l]  
    # and arr[r] and  
    # update l, r and  
    # cnt accordingly. 
    while (l != r): 
          
        # If we find a pair  
        # with sum x, then  
        # increment cnt, move  
        # l and r to next element. 
        if arr[l] + arr[r] == x: 
            cnt += 1
              
            # This condition is  
            # required to be checked,  
            # otherwise l and r will  
            # cross each other and  
            # loop will never terminate. 
            if l == (r - 1 + n) % n: 
                return cnt 
              
            l = (l + 1) % n 
            r = (r - 1 + n) % n 
          
        # If current pair sum  
        # is less, move to  
        # the higher sum side. 
        elif arr[l] + arr[r] < x: 
            l = (l + 1) % n 
          
        # If current pair sum  
        # is greater, move to  
        # the lower sum side. 
        else: 
            r = (n + r - 1) % n 
      
    return cnt 
  
# Driver Code 
arr = [11, 15, 6, 7, 9, 10] 
s = 16
  
print(pairsInSortedRotated(arr, 6, s)) 
  
# This code is contributed  
# by ChitraNayal 
```

## C#

```cs
// C# program to find  
// number of pairs with  
// a given sum in a sorted  
// and rotated array. 
using System; 
  
class GFG 
{ 
      
// This function returns 
// count of number of pairs 
// with sum equals to x. 
static int pairsInSortedRotated(int []arr,  
                                int n, int x) 
{ 
    // Find the pivot element.  
    // Pivot element is largest  
    // element of array. 
    int i; 
    for (i = 0; i < n - 1; i++) 
        if (arr[i] > arr[i + 1]) 
            break; 
      
    // l is index of 
    // smallest element. 
    int l = (i + 1) % n;  
      
    // r is index of  
    // largest element. 
    int r = i; 
      
    // Variable to store 
    // count of number 
    // of pairs. 
    int cnt = 0; 
  
    // Find sum of pair  
    // formed by arr[l]  
    // and arr[r] and  
    // update l, r and  
    // cnt accordingly. 
    while (l != r) 
    { 
        // If we find a pair with  
        // sum x, then increment  
        // cnt, move l and r to  
        // next element. 
        if (arr[l] + arr[r] == x) 
        { 
            cnt++; 
              
            // This condition is required  
            // to be checked, otherwise  
            // l and r will cross each  
            // other and loop will never  
            // terminate. 
            if(l == (r - 1 + n) % n) 
            { 
                return cnt; 
            } 
              
            l = (l + 1) % n; 
            r = (r - 1 + n) % n; 
        } 
  
        // If current pair sum  
        // is less, move to  
        // the higher sum side. 
        else if (arr[l] + arr[r] < x) 
            l = (l + 1) % n; 
          
        // If current pair sum  
        // is greater, move  
        // to the lower sum side. 
        else
            r = (n + r - 1) % n; 
    } 
      
    return cnt; 
} 
  
// Driver Code 
static public void Main () 
{ 
    int []arr = {11, 15, 6, 7, 9, 10}; 
    int sum = 16; 
    int n = arr.Length; 
      
    Console.WriteLine( 
            pairsInSortedRotated(arr, n, sum)); 
} 
} 
  
// This code is contributed by akt_mit 
```

## PHP

```php
<?php 
// PHP program to find number  
// of pairs with a given sum  
// in a sorted and rotated array. 
  
// This function returns count  
// of number of pairs with sum 
// equals to x. 
function pairsInSortedRotated($arr,  
                              $n, $x) 
{ 
    // Find the pivot element. 
    // Pivot element is largest  
    // element of array. 
    $i; 
    for ($i = 0; $i < $n - 1; $i++) 
        if ($arr[$i] > $arr[$i + 1]) 
            break; 
      
    // l is index of 
    // smallest element. 
    $l = ($i + 1) % $n;  
      
    // r is index of  
    // largest element. 
    $r = $i; 
      
    // Variable to store  
    // count of number 
    // of pairs. 
    $cnt = 0; 
  
    // Find sum of pair formed  
    // by arr[l] and arr[r] and 
    // update l, r and cnt  
    // accordingly. 
    while ($l != $r) 
    { 
        // If we find a pair with  
        // sum x, then increment 
        // cnt, move l and r to  
        // next element. 
        if ($arr[$l] + $arr[$r] == $x) 
        { 
            $cnt++; 
              
            // This condition is required  
            // to be checked, otherwise l  
            // and r will cross each other  
            // and loop will never terminate. 
            if($l == ($r - 1 + $n) % $n) 
            { 
                return $cnt; 
            } 
              
            $l = ($l + 1) % $n; 
            $r = ($r - 1 + $n) % $n; 
        } 
  
        // If current pair sum  
        // is less, move to  
        // the higher sum side. 
        else if ($arr[$l] + $arr[$r] < $x) 
            $l = ($l + 1) % $n; 
          
        // If current pair sum  
        // is greater, move to 
        // the lower sum side. 
        else
            $r = ($n + $r - 1) % $n; 
    } 
      
    return $cnt; 
} 
  
// Driver Code 
$arr = array(11, 15, 6,  
              7, 9, 10); 
$sum = 16; 
$n = sizeof($arr) / sizeof($arr[0]); 
  
echo pairsInSortedRotated($arr,      
                          $n, $sum); 
  
// This code is contributed by ajit 
?> 
```

输出：

```
2
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。