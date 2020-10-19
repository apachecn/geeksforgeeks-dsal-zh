# 找到一个数组元素，使所有元素都可被它整除

> 原文： [https://www.geeksforgeeks.org/number-among-n-numbers-numbers-divisible/](https://www.geeksforgeeks.org/number-among-n-numbers-numbers-divisible/)

给定一个数字数组，请在其中找到一个数字，以使所有数字都可被其整除。 如果不可能，请打印 -1。

例子：

```
Input : arr = {25, 20, 5, 10, 100} 
Output : 5 
Explanation : 5 is an array element
 which divides all numbers.

Input : arr = {9, 3, 6, 2, 15} 
Output : -1 
Explanation : No numbers are divisible
by any array element.

```



**方法 1（自然）**：

通常的方法是获取每个元素并检查是否与所有其他元素相除。 如果所有数字都是可分的，则返回数字。

## C++ 

```cpp

// CPP program to find an array element that  
// divides all numbers in the array using 
// naive approach 
#include <bits/stdc++.h> 
using namespace std; 

// function to find smallest num 
int findSmallest(int a[], int n) 
{ 
    // traverse for all elements 
    for (int i = 0; i < n; i++) { 

        int j; 
        for (j = 0; j < n; j++)  
            if (a[j] % a[i])  
                break; 

        // stores the minimum if 
        // it divides all 
        if (j == n) 
            return a[i]; 
    } 

    return -1; 
} 

// driver code 
int main() 
{ 
    int a[] = { 25, 20, 5, 10, 100 }; 
    int n = sizeof(a) / sizeof(int); 
    cout << findSmallest(a, n); 
    return 0; 
} 

```

## Java

```
// Java program to find an array element 
// that divides all numbers in the array  
// using naive approach 
import java.io.*; 
  
class GFG { 
      
    // function to find smallest num 
    static int findSmallest(int a[], int n) 
    { 
        // traverse for all elements 
        for (int i = 0; i < n; i++)  
        { 
              
            int j; 
            for (j = 0; j < n; j++)  
                if (a[j] % a[i]>=1)  
                    break; 
      
            // stores the minimum if 
            // it divides all 
            if (j == n) 
                return a[i]; 
        } 
      
        return -1; 
    } 
      
    // driver code 
    public static void main(String args[]) 
    { 
        int a[] = { 25, 20, 5, 10, 100 }; 
        int n = a.length; 
        System.out.println(findSmallest(a, n)); 
    } 
} 
  
  
// This code is contributed by Nikita Tiwari.
```

## Python3

```
# Python 3 program to find an array 
# element that divides all numbers 
# in the array using naive approach 
  
# Function to find smallest num 
def findSmallest(a, n) : 
      
    # Traverse for all elements 
    for i in range(0, n ) : 
          
        for j in range(0, n) : 
              
            if ((a[j] % a[i]) >= 1) : 
                break
  
        # Stores the minimum  
        # if it divides all 
        if (j == n - 1) : 
            return a[i] 
                  
    return -1
  
  
# Driver code 
a = [ 25, 20, 5, 10, 100 ] 
n = len(a) 
print(findSmallest(a, n)) 
  
  
# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find an array element 
// that divides all numbers in the array  
// using naive approach 
using System; 
  
class GFG { 
      
    // function to find smallest num 
    static int findSmallest(int []a, int n) 
    { 
        // traverse for all elements 
        for (int i = 0; i < n; i++)  
        { 
              
            int j; 
            for (j = 0; j < n; j++)  
                if (a[j] % a[i] >= 1)  
                    break; 
      
            // stores the minimum if 
            // it divides all 
            if (j == n) 
                return a[i]; 
        } 
      
        return -1; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int []a = { 25, 20, 5, 10, 100 }; 
        int n = a.Length; 
        Console.WriteLine(findSmallest(a, n)); 
    } 
} 
  
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// PHP program to find an array  
// element that divides all  
// numbers in the array using 
// naive approach 
  
// function to find smallest num 
function findSmallest($a, $n) 
{ 
      
    // traverse for all elements 
    for ($i = 0; $i < $n; $i++)  
    { 
        $j; 
        for ($j = 0; $j < $n; $j++)  
            if ($a[$j] % $a[$i])  
                break; 
  
        // stores the minimum if 
        // it divides all 
        if ($j == $n) 
            return $a[$i]; 
    } 
  
    return -1; 
} 
  
    // Driver Code 
    $a = array( 25, 20, 5, 10, 100 ); 
    $n = sizeof($a); 
    echo findSmallest($a, $n); 
  
// This code is contributed by nitin mittal 
?>
```

输出：

```
5
```

时间复杂度：`O(n ^ 2)`

方法 2（有效）：

一种有效的方法是查找所有数字中的最小数字，并检查是否将所有其他数字相除，如果是，则最小数字将为所需数字。

## C++

```
// CPP Program to find the smallest number 
// that divides all numbers in an array 
#include <bits/stdc++.h> 
using namespace std; 
  
// function to find smallest num 
int findSmallest(int a[], int n) 
{  
    // Find the smallest element 
    int smallest = *min_element(a, a+n); 
      
    // Check if all array elements 
    // are divisible by smallest. 
    for (int i = 1; i < n; i++)      
        if (a[i] % smallest)  
            return -1; 
  
    return smallest; 
} 
  
// Driver code 
int main() 
{ 
    int a[] = { 25, 20, 5, 10, 100 }; 
    int n = sizeof(a) / sizeof(int);     
    cout << findSmallest(a, n);     
    return 0; 
}
```

## Java

```
// Java Program to find the  
// smallest number that divides 
// all numbers in an array 
import java.io.*; 
  
class GFG { 
  
    // function to find the smallest element 
    static int min_element(int a[]) 
    { 
        int min = Integer.MAX_VALUE, i; 
        for (i = 0; i < a.length; i++)  
        { 
            if (a[i] < min) 
                min = a[i]; 
        } 
          
        return min; 
    } 
      
    // function to find smallest num 
    static int findSmallest(int a[], int n)  
    { 
        // Find the smallest element 
        int smallest = min_element(a); 
      
        // Check if all array elements 
        // are divisible by smallest. 
        for (int i = 1; i < n; i++) 
        if (a[i] % smallest >= 1) 
            return -1; 
      
        return smallest; 
    } 
      
    // Driver code 
    public static void main(String args[]) 
    { 
        int a[] = {25, 20, 5, 10, 100}; 
        int n = a.length; 
        System.out.println(findSmallest(a, n)); 
    } 
} 
  
// This code is contributed by Nikita Tiwari.
```

## Python3

```
# Python3 Program to find the 
# smallest number that divides 
# all numbers in an array 
  
# Function to find the smallest element 
def min_element(a) : 
      
    m = 10000000
      
    for i in range(0, len(a)) : 
          
        if (a[i] < m) : 
            m = a[i] 
      
    return m 
  
# Function to find smallest num 
def findSmallest(a, n) : 
      
    # Find the smallest element 
    smallest = min_element(a) 
      
    # Check if all array elements 
    # are divisible by smallest. 
    for i in range(1, n) : 
          
        if (a[i] % smallest >= 1) : 
            return -1
  
    return smallest 
  
  
# Driver code 
  
a = [ 25, 20, 5, 10, 100 ] 
n = len(a) 
print(findSmallest(a, n)) 
  
  
# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find the  
// smallest number that divides 
// all numbers in an array 
using System; 
  
class GFG { 
  
    // function to find the smallest element 
    static int min_element(int []a) 
    { 
        int min = int.MaxValue; 
        int i; 
        for (i = 0; i < a.Length; i++)  
        { 
            if (a[i] < min) 
                min = a[i]; 
        } 
          
        return min; 
    } 
      
    // function to find smallest num 
    static int findSmallest(int []a, int n)  
    { 
        // Find the smallest element 
        int smallest = min_element(a); 
      
        // Check if all array elements 
        // are divisible by smallest. 
        for (int i = 1; i < n; i++) 
        if (a[i] % smallest >= 1) 
            return -1; 
      
        return smallest; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int []a = {25, 20, 5, 10, 100}; 
        int n = a.Length; 
        Console.WriteLine(findSmallest(a, n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// PHP Program to find the smallest number 
// that divides all numbers in an array 
  
// function to find smallest num 
function findSmallest($a, $n) 
{ 
      
    // Find the smallest element 
    $smallest = min($a); 
      
    // Check if all array elements 
    // are divisible by smallest. 
    for ($i = 1; $i < $n; $i++)  
        if ($a[$i] % $smallest)  
            return -1; 
  
    return $smallest; 
} 
  
    // Driver Code 
    $a = array(25, 20, 5, 10, 100); 
    $n =count($a); 
    echo findSmallest($a, $n);  
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
5
```

时间复杂度：`O(n)`。