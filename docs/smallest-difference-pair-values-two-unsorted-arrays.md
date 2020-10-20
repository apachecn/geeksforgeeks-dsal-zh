# 两个未排序数组之间的最小差值对

> 原文： [https://www.geeksforgeeks.org/smallest-difference-pair-values-two-unsorted-arrays/](https://www.geeksforgeeks.org/smallest-difference-pair-values-two-unsorted-arrays/)

给定两个整数数组，请计算差异最小（非负）的一对值（每个数组中的一个值）。 退还差额。

**示例**：

```
Input : A[] = {l, 3, 15, 11, 2}
        B[] = {23, 127, 235, 19, 8} 
Output : 3  
That is, the pair (11, 8) 

Input : A[] = {l0, 5, 40}
        B[] = {50, 90, 80} 
Output : 10
That is, the pair (40, 50)

```



一种简单的**解决方案**是使用两个具有时间复杂度`O(n^2)`的循环进行暴力破解。

**更好的解决方案**是对数组进行排序。 对数组进行排序后，我们可以使用下文中讨论的方法通过遍历数组来找到最小差异。

[从两个排序的数组中查找最接近的对](https://www.geeksforgeeks.org/given-two-sorted-arrays-number-x-find-pair-whose-sum-closest-x/)

考虑以下两个数组：

```
A = {1, 2, 11, 15}
B = {4, 12, 19, 23, 127, 235}
```

1.  假设一个指针`a`指向`A`的开头，一个指针`b`指向`B`的开头。`a`和`bis`之间的当前差值 3.将其存储为最小值。

2. 我们如何（可能）缩小这种差异？ 好吧，`bis`处的值大于`a`处的值，因此移动`b`只会使差值更大。 因此，我们要移动一个。

3. 现在`a`指向 2，`b`（静止）指向 4。该差为 2，因此我们应更新`min`。 移动`a`，因为它较小。

4. 现在`a`指向 11，`b`指向 4。移动`b`。

5. 现在，`a`指向 11，`b`指向 12。将`min`更新为 1。移动`b`。 等等。

以下是该想法的实现。

## C++ 

```cpp

// C++ Code to find Smallest  
// Difference between two Arrays 
#include <bits/stdc++.h> 
using namespace std; 

// function to calculate Small  
// result between two arrays 
int findSmallestDifference(int A[], int B[], 
                           int m, int n) 
{ 
    // Sort both arrays using 
    // sort function 
    sort(A, A + m); 
    sort(B, B + n); 

    int a = 0, b = 0; 

    // Initialize result as max value 
    int result = INT_MAX; 

    // Scan Both Arrays upto  
    // sizeof of the Arrays 
    while (a < m && b < n) 
    { 
        if (abs(A[a] - B[b]) < result) 
            result = abs(A[a] - B[b]); 

        // Move Smaller Value 
        if (A[a] < B[b]) 
            a++; 

        else
            b++; 
    } 

    // return final sma result 
    return result;  
} 

// Driver Code 
int main() 
{ 
    // Input given array A 
    int A[] = {1, 2, 11, 5}; 

    // Input given array B 
    int B[] = {4, 12, 19, 23, 127, 235}; 

    // Calculate size of Both arrays 
    int m = sizeof(A) / sizeof(A[0]); 
    int n = sizeof(B) / sizeof(B[0]); 

    // Call function to print  
    // smallest result 
    cout << findSmallestDifference(A, B, m, n); 

    return 0; 
} 

```

## Java

```
// Java Code to find Smallest  
// Difference between two Arrays 
import java.util.*; 
  
class GFG  
{ 
      
    // function to calculate Small  
    // result between two arrays 
    static int findSmallestDifference(int A[], int B[], 
                                      int m, int n) 
    { 
        // Sort both arrays  
        // using sort function 
        Arrays.sort(A); 
        Arrays.sort(B); 
      
        int a = 0, b = 0; 
      
        // Initialize result as max value 
        int result = Integer.MAX_VALUE; 
      
        // Scan Both Arrays upto  
        // sizeof of the Arrays 
        while (a < m && b < n) 
        { 
            if (Math.abs(A[a] - B[b]) < result) 
                result = Math.abs(A[a] - B[b]); 
      
            // Move Smaller Value 
            if (A[a] < B[b]) 
                a++; 
      
            else
                b++; 
        } 
          
        // return final sma result 
        return result;  
    } 
      
    // Driver Code 
    public static void main(String[] args)  
    { 
        // Input given array A 
        int A[] = {1, 2, 11, 5}; 
      
        // Input given array B 
        int B[] = {4, 12, 19, 23, 127, 235}; 
      
      
        // Calculate size of Both arrays 
        int m = A.length; 
        int n = B.length; 
      
        // Call function to  
        // print smallest result 
        System.out.println(findSmallestDifference 
                                   (A, B, m, n)); 
          
    } 
} 
// This code is contributed 
// by Arnav Kr. Mandal.
```

## Python3

```
# Python 3 Code to find 
# Smallest Difference between 
# two Arrays 
import sys 
  
# function to calculate 
# Small result between 
# two arrays 
def findSmallestDifference(A, B, m, n): 
  
    # Sort both arrays  
    # using sort function 
    A.sort() 
    B.sort() 
  
    a = 0
    b = 0
  
    # Initialize result as max value 
    result = sys.maxsize 
  
    # Scan Both Arrays upto 
    # sizeof of the Arrays 
    while (a < m and b < n): 
      
        if (abs(A[a] - B[b]) < result): 
            result = abs(A[a] - B[b]) 
  
        # Move Smaller Value 
        if (A[a] < B[b]): 
            a += 1
  
        else: 
            b += 1
    # return final sma result 
    return result  
  
# Driver Code 
  
# Input given array A 
A = [1, 2, 11, 5] 
  
# Input given array B 
B = [4, 12, 19, 23, 127, 235] 
  
# Calculate size of Both arrays 
m = len(A) 
n = len(B) 
  
# Call function to  
# print smallest result 
print(findSmallestDifference(A, B, m, n)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal
```

## C#

```
// C# Code to find Smallest  
// Difference between two Arrays 
using System; 
  
class GFG  
{ 
      
    // function to calculate Small  
    // result between two arrays 
    static int findSmallestDifference(int []A, int []B, 
                                      int m, int n) 
    { 
          
        // Sort both arrays using 
        // sort function 
        Array.Sort(A); 
        Array.Sort(B); 
      
        int a = 0, b = 0; 
      
        // Initialize result as max value 
        int result = int.MaxValue; 
      
        // Scan Both Arrays upto  
        // sizeof of the Arrays 
        while (a < m && b < n) 
        { 
            if (Math.Abs(A[a] - B[b]) < result) 
                result = Math.Abs(A[a] - B[b]); 
      
            // Move Smaller Value 
            if (A[a] < B[b]) 
                a++; 
      
            else
                b++; 
        } 
          
        // return final sma result 
        return result;  
    } 
      
    // Driver Code 
    public static void Main()  
    { 
          
        // Input given array A 
        int []A = {1, 2, 11, 5}; 
      
        // Input given array B 
        int []B = {4, 12, 19, 23, 127, 235}; 
      
      
        // Calculate size of Both arrays 
        int m = A.Length; 
        int n = B.Length; 
      
        // Call function to  
        // print smallest result 
        Console.Write(findSmallestDifference 
                              (A, B, m, n)); 
          
    } 
} 
  
// This code is contributed 
// by nitin mittal.
```

## PHP

```
<?php 
// PHP Code to find Smallest  
// Difference between two Arrays 
  
  
// function to calculate Small 
// result between two arrays 
function findSmallestDifference($A, $B, 
                                $m, $n) 
{ 
    // Sort both arrays  
    // using sort function 
    sort($A);  
    sort($A, $m); 
    sort($B);  
    sort($B, $n); 
  
    $a = 0; $b = 0; 
    $INT_MAX = 1; 
  
    // Initialize result  
    // as max value 
    $result = $INT_MAX; 
  
    // Scan Both Arrays upto 
    // sizeof of the Arrays 
    while ($a < $m && $b < $n) 
    { 
        if (abs($A[$a] - $B[$b]) < $result) 
            $result = abs($A[$a] - $B[$b]); 
  
        // Move Smaller Value 
        if ($A[$a] < $B[$b]) 
            $a++; 
  
        else
            $b++; 
    } 
  
    // return final sma result 
    return $result;  
} 
  
// Driver Code 
{ 
    // Input given array A 
    $A = array(1, 2, 11, 5); 
  
    // Input given array B 
    $B = array(4, 12, 19, 23, 127, 235); 
  
  
    // Calculate size of Both arrays 
    $m = sizeof($A) / sizeof($A[0]); 
    $n = sizeof($B) / sizeof($B[0]); 
  
    // Call function to print 
    // smallest result 
    echo findSmallestDifference($A, $B, $m, $n); 
  
    return 0; 
} 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
1
```

该算法需要`O(m log m + n log n)`时间进行排序，并花费`O(m + n)`时间来找到最小差异。 因此，总体运行时间为`O(m log m + n log n)`。

