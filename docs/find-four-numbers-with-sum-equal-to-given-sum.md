# 找到总和为给定值的四个元素 | 系列 1（`n ^ 3`解）

> 原文： [https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/)

给定一个整数数组，请找到该数组中四个和的总和等于给定值`X`的所有组合。

例如，如果给定的数组为`{10, 2, 3, 4, 5, 9, 7, 8}`且`X = 23`，则您的函数应打印`3 5 7 8`（`3 + 5 + 7 + 8 = 23`）。



**朴素的解决方案**将生成所有可能的四元组，并将每个四元组的和与`X`进行比较。以下代码使用四个嵌套循环实现了此简单方法。

## C++ 

```cpp

// C++ program for naive solution to 
// print all combination of 4 elements 
// in A[] with sum equal to X  
#include <bits/stdc++.h> 
using namespace std; 

/* A naive solution to print all combination  
of 4 elements in A[]with sum equal to X */
void findFourElements(int A[], int n, int X) 
{ 

// Fix the first element and find other three 
for (int i = 0; i < n - 3; i++) 
{ 
    // Fix the second element and find other two 
    for (int j = i + 1; j < n - 2; j++) 
    { 

        // Fix the third element and find the fourth 
        for (int k = j + 1; k < n - 1; k++) 
        { 
            // find the fourth 
            for (int l = k + 1; l < n; l++) 
            if (A[i] + A[j] + A[k] + A[l] == X) 
                cout << A[i] <<", " << A[j]  
                     << ", " << A[k] << ", " << A[l]; 
        }  
    } 
} 
} 

// Driver Code 
int main() 
{ 
    int A[] = {10, 20, 30, 40, 1, 2}; 
    int n = sizeof(A) / sizeof(A[0]); 
    int X = 91; 
    findFourElements (A, n, X); 
    return 0; 
} 

// This code is contributed 
// by Akanksha Rai 

```

## C

```c
#include <stdio.h> 
  
/* A naive solution to print all combination of 4 elements in A[] 
  with sum equal to X */
void findFourElements(int A[], int n, int X) 
{ 
  // Fix the first element and find other three 
  for (int i = 0; i < n-3; i++) 
  { 
    // Fix the second element and find other two 
    for (int j = i+1; j < n-2; j++) 
    { 
      // Fix the third element and find the fourth 
      for (int k = j+1; k < n-1; k++) 
      { 
        // find the fourth 
        for (int l = k+1; l < n; l++) 
           if (A[i] + A[j] + A[k] + A[l] == X) 
              printf("%d, %d, %d, %d", A[i], A[j], A[k], A[l]); 
      } 
    } 
  } 
} 
  
// Driver program to test above function 
int main() 
{ 
    int A[] = {10, 20, 30, 40, 1, 2}; 
    int n = sizeof(A) / sizeof(A[0]); 
    int X = 91; 
    findFourElements (A, n, X); 
    return 0; 
} 
```

## Java

```java
class FindFourElements  
{ 
  
    /* A naive solution to print all combination of 4 elements in A[] 
       with sum equal to X */
    void findFourElements(int A[], int n, int X)  
    { 
        // Fix the first element and find other three 
        for (int i = 0; i < n - 3; i++)  
        { 
            // Fix the second element and find other two 
            for (int j = i + 1; j < n - 2; j++)  
            { 
                // Fix the third element and find the fourth 
                for (int k = j + 1; k < n - 1; k++)  
                { 
                    // find the fourth 
                    for (int l = k + 1; l < n; l++)  
                    { 
                        if (A[i] + A[j] + A[k] + A[l] == X)  
                            System.out.print(A[i]+" "+A[j]+" "+A[k]  
                                                                 +" "+A[l]); 
                    } 
                } 
            } 
        } 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args)  
    { 
        FindFourElements findfour = new FindFourElements(); 
        int A[] = {10, 20, 30, 40, 1, 2}; 
        int n = A.length; 
        int X = 91; 
        findfour.findFourElements(A, n, X); 
    } 
} 
```

## Python3

```py
# A naive solution to print all combination 
# of 4 elements in A[] with sum equal to X  
def findFourElements(A, n, X): 
      
    # Fix the first element and find  
    # other three 
    for i in range(0,n-3): 
          
        # Fix the second element and  
        # find other two 
        for j in range(i+1,n-2): 
              
            # Fix the third element  
            # and find the fourth 
            for k in range(j+1,n-1): 
                  
                # find the fourth 
                for l in range(k+1,n): 
                      
                    if A[i] + A[j] + A[k] + A[l] == X: 
                        print ("%d, %d, %d, %d"
                        %( A[i], A[j], A[k], A[l])) 
  
# Driver program to test above function 
A = [10, 2, 3, 4, 5, 9, 7, 8] 
n = len(A) 
X = 23
findFourElements (A, n, X) 
  
# This code is contributed by shreyanshi_arun 
```

## C#

```cs
// C# program for naive solution to 
// print all combination of 4 elements 
// in A[] with sum equal to X  
using System; 
  
class FindFourElements  
{ 
    void findFourElements(int []A, int n, int X)  
    { 
        // Fix the first element and find other three 
        for (int i = 0; i < n - 3; i++)  
        { 
            // Fix the second element and find other two 
            for (int j = i + 1; j < n - 2; j++)  
            { 
                // Fix the third element and find the fourth 
                for (int k = j + 1; k < n - 1; k++)  
                { 
                    // find the fourth 
                    for (int l = k + 1; l < n; l++)  
                    { 
                        if (A[i] + A[j] + A[k] + A[l] == X)  
                        Console.Write(A[i] + " " + A[j] + 
                                " " + A[k] + " " + A[l]); 
                    } 
                } 
            } 
        } 
    } 
  
    // Driver program to test above functions 
    public static void Main()  
    { 
        FindFourElements findfour = new FindFourElements(); 
        int []A = {10, 20, 30, 40, 1, 2}; 
        int n = A.Length; 
        int X = 91; 
        findfour.findFourElements(A, n, X); 
    } 
} 
  
// This code is contributed by nitin mittal 
```

## PHP
filter_n

```php
<?php 
/* A naive solution to print all combination  
of 4 elements in A[] with sum equal to X */
  
function findFourElements($A, $n, $X) 
{ 
    // Fix the first element and find other 
    // three 
    for ($i = 0; $i < $n-3; $i++) 
    { 
        // Fix the second element and find 
        // other two 
        for ($j = $i+1; $j < $n-2; $j++) 
        { 
            // Fix the third element and  
            // find the fourth 
            for ($k = $j+1; $k < $n-1; $k++) 
            { 
                // find the fourth 
                for ($l = $k+1; $l < $n; $l++) 
                    if ($A[$i] + $A[$j] + 
                        $A[$k] + $A[$l] == $X) 
                          
                        echo $A[$i], ", " , $A[$j], 
                        ", ", $A[$k], ", ", $A[$l]; 
            } 
        } 
    } 
} 
  
// Driver program to test above function 
    $A = array (10, 20, 30, 40, 1, 2); 
    $n = sizeof($A) ; 
    $X = 91; 
    findFourElements ($A, $n, $X); 
      
// This code is contributed by m_kit 
?> 
```

输出：

```
20, 30, 40, 1
```

时间复杂度：`O(n^4)`。

通过使用排序作为预处理步骤，然后使用本文的方法 1 减少循环，可以将时间复杂度提高到`O(n ^ 3)`。