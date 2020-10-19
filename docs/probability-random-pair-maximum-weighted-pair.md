# 随机对为最大加权对的概率

> 原文： [https://www.geeksforgeeks.org/probability-random-pair-maximum-weighted-pair/](https://www.geeksforgeeks.org/probability-random-pair-maximum-weighted-pair/)

给定两个数组`A`和`B`，从数组`A`中选择一个元素，数组`B`中另一个元素，从中选取一个随机对。输出该对被最大加权的概率。

**示例**：

```
Input : A[] = 1 2 3
        B[] = 1 3 3
Output : 0.222
Explanation : Possible pairs are : {1, 1}, 
{1, 3}, {1, 3}, {2, 1}, {2, 3}, {2, 3},
{3, 1}, {3, 3}, {3, 3} i.e. 9.
The pair with maximum weight is {3, 3} with
frequency 2\. So, the probability of random 
pair being maximum is 2/9 = 0.2222.

```



**暴力法**：以`N ^ 2`的时间复杂度生成所有可能的对，并计算最大加权对。

**更好的方法**：对两个数组都进行排序，并对`A`和`B`中的最后一个（最大）元素进行计数。最大加权对的数量将是`(count1 * count2) / sizeof(A) * sizeof(B)`。

**最佳方法**：最佳方法将是遍历两个数组并计算最大元素。 最大加权对的数量将是两个计数的乘积。 概率将是`(count1 * count2) / sizeof(A) * sizeof(B)`。

下面是实现：

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// Function to return probability 
double probability(int a[], int b[], int size1,  
                                     int size2) 
{ 
    // Count occurrences of maximum element  
    // in A[] 
    int max1 = INT_MIN,  count1 = 0; 
    for (int i = 0; i < size1; i++) { 
        if (a[i] > max1) { 
            max1 = a[i]; 
            count1 = 1; 
        } 
        else if (a[i] == max1) { 
            count1++; 
        } 
    } 

    // Count occurrences of maximum element  
    // in B[] 
    int max2 = INT_MIN, count2 = 0; 
    for (int i = 0; i < size2; i++) { 
        if (b[i] > max2) { 
            max2 = b[i]; 
            count2 = 1; 
        } 
        else if (b[i] == max2) { 
            count2++; 
        } 
    } 

    // Returning probability 
    return (double)(count1 * count2) /  
                  (size1 * size2); 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 3 }; 
    int b[] = { 1, 3, 3 }; 

    int size1 = sizeof(a) / sizeof(a[0]); 
    int size2 = sizeof(b) / sizeof(b[0]); 

    cout << probability(a, b, size1, size2); 
    return 0; 
} 

```

## Java

```
// Java program to find Probability  
// of a random pair being the maximum 
// weighted pair 
import java.io.*; 
  
class GFG { 
      
    // Function to return probability 
    static double probability(int a[], int b[],  
                            int size1,int size2) 
    { 
        // Count occurrences of maximum  
        // element in A[] 
        int max1 = Integer.MIN_VALUE,  count1 = 0; 
        for (int i = 0; i < size1; i++) { 
            if (a[i] > max1) { 
                max1 = a[i]; 
                count1 = 1; 
            } 
            else if (a[i] == max1) { 
                count1++; 
            } 
        } 
       
        // Count occurrences of maximum  
        // element in B[] 
        int max2 = Integer.MIN_VALUE, count2 = 0; 
        for (int i = 0; i < size2; i++) { 
            if (b[i] > max2) { 
                max2 = b[i]; 
                count2 = 1; 
            } 
            else if (b[i] == max2) { 
                count2++; 
            } 
        } 
       
        // Returning probability 
        return (double)(count1 * count2) / (size1 * size2); 
    } 
       
    // Driver code 
    public static void main(String args[]) 
    { 
        int a[] = { 1, 2, 3 }; 
        int b[] = { 1, 3, 3 }; 
       
        int size1 = a.length; 
        int size2 = b.length; 
       
        System.out.println(probability(a, b,  
                            size1, size2)); 
    } 
} 
  
/*This code is contributed by Nikita Tiwari.*/
```

## Python3

```
import sys 
  
# Function to return probability  
def probability(a, b, size1, size2): 
  
    # Count occurrences of maximum 
    # element in A[]  
    max1 = -(sys.maxsize - 1) 
    count1 = 0
    for i in range(size1): 
        if a[i] > max1: 
            count1 = 1
        elif a[i] == max1: 
            count1 += 1
  
    # Count occurrences of maximum  
    # element in B[]  
    max2 = -(sys.maxsize - 1) 
    count2 = 0
    for i in range(size2): 
        if b[i] > max2: 
            max2 = b[i] 
            count2 = 1
        elif b[i] == max2: 
            count2 += 1
  
    # Returning probability  
    return round((count1 * count2) / 
                 (size1 * size2), 6) 
  
# Driver code 
a = [1, 2, 3] 
b = [1, 3, 3] 
size1 = len(a) 
size2 = len(b) 
print(probability(a, b, size1, size2)) 
  
# This code is contributed  
# by Shrikant13
```

## C#

```
// C# program to find Probability of a random  
// pair being the maximum weighted pair 
using System; 
  
class GFG { 
      
    // Function to return probability 
    static float probability(int []a, int []b,  
                          int size1,int size2) 
    { 
          
        // Count occurrences of maximum  
        // element in A[] 
        int max1 = int.MinValue, count1 = 0; 
          
        for (int i = 0; i < size1; i++) { 
            if (a[i] > max1) { 
                max1 = a[i]; 
                count1 = 1; 
            } 
            else if (a[i] == max1) { 
                count1++; 
            } 
        } 
      
        // Count occurrences of maximum  
        // element in B[] 
        int max2 = int.MinValue, count2 = 0; 
          
        for (int i = 0; i < size2; i++) { 
            if (b[i] > max2) { 
                max2 = b[i]; 
                count2 = 1; 
            } 
            else if (b[i] == max2) { 
                count2++; 
            } 
        } 
      
        // Returning probability 
        return (float)(count1 * count2) /  
                            (size1 * size2); 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int []a = { 1, 2, 3 }; 
        int []b = { 1, 3, 3 }; 
      
        int size1 = a.Length; 
        int size2 = b.Length; 
      
        Console.WriteLine(probability(a, b,  
                            size1, size2)); 
    } 
} 
  
/* This code is contributed by vt_m.*/
```

## PHP

```
<?php 
// PHP program for Probability of  
// a random pair being the maximum  
// weighted pair 
  
// Function to return probability 
function probability($a, $b,  
             $size1, $size2) 
{ 
      
    // Count occurrences of maximum 
    // element in A[] 
    $max1 = PHP_INT_MIN; $count1 = 0; 
    for ($i = 0; $i < $size1; $i++) 
    { 
        if ($a[$i] > $max1) 
        { 
            $max1 = $a[$i]; 
            $count1 = 1; 
        } 
        else if ($a[$i] == $max1) 
        { 
            $count1++; 
        } 
    } 
  
    // Count occurrences of maximum  
    // element in B[] 
    $max2 = PHP_INT_MIN; $count2 = 0; 
    for ($i = 0; $i < $size2; $i++)  
    { 
        if ($b[$i] > $max2)  
        { 
            $max2 = $b[$i]; 
            $count2 = 1; 
        } 
        else if ($b[$i] == $max2)  
        { 
            $count2++; 
        } 
    } 
  
    // Returning probability 
    return (double)($count1 * $count2) /  
                     ($size1 * $size2); 
} 
  
    // Driver code 
    $a = array(1, 2, 3); 
    $b = array(1, 3, 3); 
    $size1 = sizeof($a); 
    $size2 = sizeof($b); 
    echo probability($a, $b,  
            $size1, $size2); 
      
// This code is contributed by ajit 
?>
```

输出：

```
0.222222
```

