# 使得两个元素都不相邻的最大和

> 原文： [https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)

给定一个正数数组，请找到子序列的最大和，并约束该序列中的任何 2 个数字都不应相邻。 所以`3 2 7 10`应该返回 13（3 和 10 之和），或者`3 2 5 10 7`应该返回 15（3、5 和 7 之和）。以最有效的方式回答问题。

例子 ：

```
Input : arr[] = {5, 5, 10, 100, 10, 5}
Output : 110

Input : arr[] = {1, 2, 3}
Output : 4

Input : arr[] = {1, 20, 3}
Output : 20

```



**算法**：

为`arr[]`中的所有元素循环，并维护两个和`incl`和`excl`，其中`incl =`包括前一个元素的最大和，而`exl =`排除前一个元素的最大和。

排除当前元素的最大和为`max(incl, excl)`，包括当前元素的最大和为`excl + current`元素（请注意，仅考虑`excl`是因为元素不能相邻）。

在循环结束时，返回最大值`incl`和`excl`。

**示例**：

```
  arr[] = {5,  5, 10, 40, 50, 35}

  incl = 5 
  excl = 0

  For i = 1 (current element is 5)
  incl =  (excl + arr[i])  = 5
  excl =  max(5, 0) = 5

  For i = 2 (current element is 10)
  incl =  (excl + arr[i]) = 15
  excl =  max(5, 5) = 5

  For i = 3 (current element is 40)
  incl = (excl + arr[i]) = 45
  excl = max(5, 15) = 15

  For i = 4 (current element is 50)
  incl = (excl + arr[i]) = 65
  excl =  max(45, 15) = 45

  For i = 5 (current element is 35)
  incl =  (excl + arr[i]) = 80
  excl =  max(65, 45) = 65

And 35 is the last element. So, answer is max(incl, excl) =  80

```

感谢 [Debanjan](http://groups.google.co.in/group/algogeeks/browse_thread/thread/eb90efd8f8d4a040/6700a1c909841637?lnk=gst&q=Given+an+array+all+of+whose+elements+are+positive+numbers%2C+find+the+maximum+sum+of+a+subsequence+with+the+constraint+that+no+2+numbers+in+the+sequence+should+be+adjacent+in+the+array#6700a1c909841637) 提供了代码。

**实现**：

## C/C++ 

```

#include<stdio.h> 

/*Function to return max sum such that no two elements 
 are adjacent */
int FindMaxSum(int arr[], int n) 
{ 
  int incl = arr[0]; 
  int excl = 0; 
  int excl_new; 
  int i; 

  for (i = 1; i < n; i++) 
  { 
     /* current max excluding i */
     excl_new = (incl > excl)? incl: excl; 

     /* current max including i */
     incl = excl + arr[i]; 
     excl = excl_new; 
  } 

   /* return max of incl and excl */
   return ((incl > excl)? incl : excl); 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr[] = {5, 5, 10, 100, 10, 5}; 
  int n = sizeof(arr) / sizeof(arr[0]); 
  printf("%d n", FindMaxSum(arr, n)); 
  return 0; 
} 

```

## Java

```java
class MaximumSum 
{ 
    /*Function to return max sum such that no two elements 
      are adjacent */
    int FindMaxSum(int arr[], int n) 
    { 
        int incl = arr[0]; 
        int excl = 0; 
        int excl_new; 
        int i; 
  
        for (i = 1; i < n; i++) 
        { 
            /* current max excluding i */
            excl_new = (incl > excl) ? incl : excl; 
  
            /* current max including i */
            incl = excl + arr[i]; 
            excl = excl_new; 
        } 
  
        /* return max of incl and excl */
        return ((incl > excl) ? incl : excl); 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args) 
    { 
        MaximumSum sum = new MaximumSum(); 
        int arr[] = new int[]{5, 5, 10, 100, 10, 5}; 
        System.out.println(sum.FindMaxSum(arr, arr.length)); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal 
```

## Python

```py
# Function to return max sum such that  
# no two elements are adjacent 
def find_max_sum(arr): 
    incl = 0
    excl = 0
     
    for i in arr: 
          
        # Current max excluding i (No ternary in  
        # Python) 
        new_excl = excl if excl>incl else incl 
         
        # Current max including i 
        incl = excl + i 
        excl = new_excl 
      
    # return max of incl and excl 
    return (excl if excl>incl else incl) 
  
# Driver program to test above function 
arr = [5, 5, 10, 100, 10, 5] 
print find_max_sum(arr) 
  
# This code is contributed by Kalai Selvan 
```

## C#

```cs
/* Program to return max sum such that no  
two elements are adjacent */
using System; 
  
class GFG { 
      
    /* Function to return max sum such 
    that no two elements are adjacent */
    static int FindMaxSum(int []arr, int n) 
    { 
        int incl = arr[0]; 
        int excl = 0; 
        int excl_new; 
        int i; 
  
        for (i = 1; i < n; i++) 
        { 
            /* current max excluding i */
            excl_new = (incl > excl) ?  
                            incl : excl; 
  
            /* current max including i */
            incl = excl + arr[i]; 
            excl = excl_new; 
        } 
  
        /* return max of incl and excl */
        return ((incl > excl) ?  
                            incl : excl); 
    } 
  
    // Driver program to test above  
    // functions 
    public static void Main() 
    { 
        int []arr = new int[]{5, 5, 10, 
                              100, 10, 5}; 
                                
        Console.Write( 
             FindMaxSum(arr, arr.Length)); 
    } 
} 
  
// This code has been contributed by 
// nitin mittal 
```

## PHP

```php
<?php 
// PHP code to find Maximum sum  
// such that no two elements  
// are adjacent 
  
/* Function to return max sum 
   such that no two elements 
   are adjacent */
function FindMaxSum($arr, $n) 
{ 
    $incl = $arr[0]; 
    $excl = 0; 
    $excl_new; 
    $i; 
  
for ($i = 1; $i <$n; $i++) 
{ 
      
    // current max excluding i  
    $excl_new = ($incl > $excl)? $incl: $excl; 
  
    // current max including i  
    $incl = $excl + $arr[$i]; 
    $excl = $excl_new; 
} 
  
// return max of incl and excl  
return (($incl > $excl)? $incl : $excl); 
} 
  
// Driver Code 
$arr = array(5, 5, 10, 100, 10, 5); 
$n = sizeof($arr); 
echo FindMaxSum($arr, $n); 
      
// This code is contributed by Ajit 
?> 
```

输出：

```
110
```

时间复杂度：`O(n)`。