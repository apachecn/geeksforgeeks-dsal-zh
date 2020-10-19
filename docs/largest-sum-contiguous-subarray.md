# 最大总和连续子数组

> 原文： [https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

编写一个有效的程序，以在具有最大和的一维数字数组中找到连续子数组的和。

![kadane-algorithm](img/b18443fe347f743a54fda310276891fb.png)



**Kadane 的算法**：

```
Initialize:
    max_so_far = 0
    max_ending_here = 0

Loop for each element of the array
  (a) max_ending_here = max_ending_here + a[i]
  (b) if(max_ending_here < 0)
            max_ending_here = 0
  (c) if(max_so_far < max_ending_here)
            max_so_far = max_ending_here
return max_so_far

```

**说明**：

Kadane 算法的简单思路是查找数组的所有正连续段（为此使用`max_ending_here`）。 并跟踪所有正分段中的最大和连续分段（为此使用`max_so_far`）。 每次我们获得正和时，请将其与`max_so_far`进行比较，如果大于`max_so_far`，则更新`max_so_far`。

```
    Lets take the example:
    {-2, -3, 4, -1, -2, 1, 5, -3}

    max_so_far = max_ending_here = 0

    for i=0,  a[0] =  -2
    max_ending_here = max_ending_here + (-2)
    Set max_ending_here = 0 because max_ending_here < 0

    for i=1,  a[1] =  -3
    max_ending_here = max_ending_here + (-3)
    Set max_ending_here = 0 because max_ending_here < 0

    for i=2,  a[2] =  4
    max_ending_here = max_ending_here + (4)
    max_ending_here = 4
    max_so_far is updated to 4 because max_ending_here greater 
    than max_so_far which was 0 till now

    for i=3,  a[3] =  -1
    max_ending_here = max_ending_here + (-1)
    max_ending_here = 3

    for i=4,  a[4] =  -2
    max_ending_here = max_ending_here + (-2)
    max_ending_here = 1

    for i=5,  a[5] =  1
    max_ending_here = max_ending_here + (1)
    max_ending_here = 2

    for i=6,  a[6] =  5
    max_ending_here = max_ending_here + (5)
    max_ending_here = 7
    max_so_far is updated to 7 because max_ending_here is 
    greater than max_so_far

    for i=7,  a[7] =  -3
    max_ending_here = max_ending_here + (-3)
    max_ending_here = 4

```

**程序**：

## C++ 

```cpp

// C++ program to print largest contiguous array sum 
#include<iostream> 
#include<climits> 
using namespace std; 

int maxSubArraySum(int a[], int size) 
{ 
    int max_so_far = INT_MIN, max_ending_here = 0; 

    for (int i = 0; i < size; i++) 
    { 
        max_ending_here = max_ending_here + a[i]; 
        if (max_so_far < max_ending_here) 
            max_so_far = max_ending_here; 

        if (max_ending_here < 0) 
            max_ending_here = 0; 
    } 
    return max_so_far; 
} 

/*Driver program to test maxSubArraySum*/
int main() 
{ 
    int a[] = {-2, -3, 4, -1, -2, 1, 5, -3}; 
    int n = sizeof(a)/sizeof(a[0]); 
    int max_sum = maxSubArraySum(a, n); 
    cout << "Maximum contiguous sum is " << max_sum; 
    return 0; 
} 

```

## Java

```
import java.io.*; 
// Java program to print largest contiguous array sum 
import java.util.*; 
  
class Kadane 
{ 
    public static void main (String[] args) 
    { 
        int [] a = {-2, -3, 4, -1, -2, 1, 5, -3}; 
        System.out.println("Maximum contiguous sum is " + 
                                       maxSubArraySum(a)); 
    } 
  
    static int maxSubArraySum(int a[]) 
    { 
        int size = a.length; 
        int max_so_far = Integer.MIN_VALUE, max_ending_here = 0; 
  
        for (int i = 0; i < size; i++) 
        { 
            max_ending_here = max_ending_here + a[i]; 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
            if (max_ending_here < 0) 
                max_ending_here = 0; 
        } 
        return max_so_far; 
    } 
}
```

## Python

```
# Python program to find maximum contiguous subarray 
   
# Function to find the maximum contiguous subarray 
from sys import maxint 
def maxSubArraySum(a,size): 
       
    max_so_far = -maxint - 1
    max_ending_here = 0
       
    for i in range(0, size): 
        max_ending_here = max_ending_here + a[i] 
        if (max_so_far < max_ending_here): 
            max_so_far = max_ending_here 
  
        if max_ending_here < 0: 
            max_ending_here = 0   
    return max_so_far 
   
# Driver function to check the above function  
a = [-13, -3, -25, -20, -3, -16, -23, -12, -5, -22, -15, -4, -7] 
print "Maximum contiguous sum is", maxSubArraySum(a,len(a)) 
   
#This code is contributed by _Devesh Agrawal_
```

## C#

```
// C# program to print largest  
// contiguous array sum 
using System; 
  
class GFG 
{ 
    static int maxSubArraySum(int []a) 
    { 
        int size = a.Length; 
        int max_so_far = int.MinValue,  
            max_ending_here = 0; 
  
        for (int i = 0; i < size; i++) 
        { 
            max_ending_here = max_ending_here + a[i]; 
              
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
              
            if (max_ending_here < 0) 
                max_ending_here = 0; 
        } 
          
        return max_so_far; 
    } 
      
    // Driver code  
    public static void Main () 
    { 
        int [] a = {-2, -3, 4, -1, -2, 1, 5, -3}; 
        Console.Write("Maximum contiguous sum is " + 
                                maxSubArraySum(a)); 
    } 
  
} 
  
// This code is contributed by Sam007_
```

## PHP

```
<?php 
// PHP program to print largest 
// contiguous array sum 
  
function maxSubArraySum($a, $size) 
{ 
    $max_so_far = PHP_INT_MIN;  
    $max_ending_here = 0; 
  
    for ($i = 0; $i < $size; $i++) 
    { 
        $max_ending_here = $max_ending_here + $a[$i]; 
        if ($max_so_far < $max_ending_here) 
            $max_so_far = $max_ending_here; 
  
        if ($max_ending_here < 0) 
            $max_ending_here = 0; 
    } 
    return $max_so_far; 
} 
  
// Driver code 
$a = array(-2, -3, 4, -1, 
           -2, 1, 5, -3); 
$n = count($a); 
$max_sum = maxSubArraySum($a, $n); 
echo "Maximum contiguous sum is " ,  
                          $max_sum; 
  
// This code is contributed by anuj_67. 
?>
```

输出：


```
Maximum contiguous sum is 7
```

如果我们将`max_so_far`与`max_ending_here`进行比较，则仅当`max_ending_here`大于 0 时，才能进一步优化上述程序。

## C++

```
int maxSubArraySum(int a[], int size) 
{ 
   int max_so_far = 0, max_ending_here = 0; 
   for (int i = 0; i < size; i++) 
   { 
       max_ending_here = max_ending_here + a[i]; 
       if (max_ending_here < 0) 
           max_ending_here = 0; 
  
       /* Do not compare for all elements. Compare only    
          when  max_ending_here > 0 */
       else if (max_so_far < max_ending_here) 
           max_so_far = max_ending_here; 
   } 
   return max_so_far; 
}
```

## Java

```
static int maxSubArraySum(int a[],int size)  
{  
      
    int max_so_far = 0, max_ending_here = 0;  
  
    for (int i = 0; i < size; i++)  
    {  
        max_ending_here = max_ending_here + a[i]; 
        if (max_ending_here < 0)  
            max_ending_here = 0;  
          
        /* Do not compare for all 
           elements. Compare only  
           when max_ending_here > 0 */
        else if (max_so_far < max_ending_here)  
            max_so_far = max_ending_here;  
          
    }  
    return max_so_far;  
}  
  
// This code is contributed by ANKITRAI1
```

## Python

```
def maxSubArraySum(a,size): 
      
    max_so_far = 0
    max_ending_here = 0
      
    for i in range(0, size): 
        max_ending_here = max_ending_here + a[i] 
        if max_ending_here < 0: 
            max_ending_here = 0
          
        # Do not compare for all elements. Compare only    
        # when  max_ending_here > 0 
        elif (max_so_far < max_ending_here): 
            max_so_far = max_ending_here 
              
    return max_so_far
```

## C#

```
static int maxSubArraySum(int[] a, 
                          int size)  
{  
int max_so_far = 0,  
    max_ending_here = 0;  
  
for (int i = 0; i < size; i++)  
{  
    max_ending_here = max_ending_here + a[i]; 
    if (max_ending_here < 0)  
        max_ending_here = 0;  
      
    /* Do not compare for all 
    elements. Compare only  
    when max_ending_here > 0 */
    else if (max_so_far < max_ending_here)  
        max_so_far = max_ending_here;  
}  
return max_so_far;  
}  
  
// This code is contributed 
// by ChitraNayal
```

## PHP

```
<?php  
function maxSubArraySum(&$a, $size) 
{ 
$max_so_far = 0; 
$max_ending_here = 0; 
for ($i = 0; $i < $size; $i++) 
{ 
    $max_ending_here = $max_ending_here + $a[$i]; 
    if ($max_ending_here < 0) 
        $max_ending_here = 0; 
  
    /* Do not compare for all elements.  
       Compare only when max_ending_here > 0 */
    else if ($max_so_far < $max_ending_here) 
        $max_so_far = $max_ending_here; 
} 
return $max_so_far; 
  
// This code is contributed 
// by ChitraNayal 
?>
```

輸出：

```
Maximum contiguous sum is 7
```

为了打印具有最大和的子数组，只要获得最大和，我们就维护索引。

## C++

```
int maxSubArraySum(int a[], int size) 
{ 
   int max_so_far = 0, max_ending_here = 0; 
   for (int i = 0; i < size; i++) 
   { 
       max_ending_here = max_ending_here + a[i]; 
       if (max_ending_here < 0) 
           max_ending_here = 0; 
  
       /* Do not compare for all elements. Compare only    
          when  max_ending_here > 0 */
       else if (max_so_far < max_ending_here) 
           max_so_far = max_ending_here; 
   } 
   return max_so_far; 
}
```

## Java

```
static int maxSubArraySum(int a[],int size)  
{  
      
    int max_so_far = 0, max_ending_here = 0;  
  
    for (int i = 0; i < size; i++)  
    {  
        max_ending_here = max_ending_here + a[i]; 
        if (max_ending_here < 0)  
            max_ending_here = 0;  
          
        /* Do not compare for all 
           elements. Compare only  
           when max_ending_here > 0 */
        else if (max_so_far < max_ending_here)  
            max_so_far = max_ending_here;  
          
    }  
    return max_so_far;  
}  
  
// This code is contributed by ANKITRAI1
```

## Python

```
def maxSubArraySum(a,size): 
      
    max_so_far = 0
    max_ending_here = 0
      
    for i in range(0, size): 
        max_ending_here = max_ending_here + a[i] 
        if max_ending_here < 0: 
            max_ending_here = 0
          
        # Do not compare for all elements. Compare only    
        # when  max_ending_here > 0 
        elif (max_so_far < max_ending_here): 
            max_so_far = max_ending_here 
              
    return max_so_far
```

## C#

```
static int maxSubArraySum(int[] a, 
                          int size)  
{  
int max_so_far = 0,  
    max_ending_here = 0;  
  
for (int i = 0; i < size; i++)  
{  
    max_ending_here = max_ending_here + a[i]; 
    if (max_ending_here < 0)  
        max_ending_here = 0;  
      
    /* Do not compare for all 
    elements. Compare only  
    when max_ending_here > 0 */
    else if (max_so_far < max_ending_here)  
        max_so_far = max_ending_here;  
}  
return max_so_far;  
}  
  
// This code is contributed 
// by ChitraNayal
```

## PHP

```
<?php  
function maxSubArraySum(&$a, $size) 
{ 
$max_so_far = 0; 
$max_ending_here = 0; 
for ($i = 0; $i < $size; $i++) 
{ 
    $max_ending_here = $max_ending_here + $a[$i]; 
    if ($max_ending_here < 0) 
        $max_ending_here = 0; 
  
    /* Do not compare for all elements.  
       Compare only when max_ending_here > 0 */
    else if ($max_so_far < $max_ending_here) 
        $max_so_far = $max_ending_here; 
} 
return $max_so_far; 
  
// This code is contributed 
// by ChitraNayal 
?>
```

输出：

```
Maximum contiguous sum is 7
Starting index 2
Ending index 6
```

现在尝试以下问题：

给定一个整数数组（可能其中一些元素为负），编写一个 C 程序，通过将`n == ARRAY_SIZE`的`n`个连续整数乘以数组，找出最大乘积。 同时打印最大乘积子数组的起点。

参考：

<http://en.wikipedia.org/wiki/Kadane%27s_Algorithm>