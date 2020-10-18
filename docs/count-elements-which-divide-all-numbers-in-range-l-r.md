# 计算将`L-R`范围内的所有数字相除的元素

> 原文： [https://www.geeksforgeeks.org/count-elements-which-divide-all-numbers-in-range-l-r/](https://www.geeksforgeeks.org/count-elements-which-divide-all-numbers-in-range-l-r/)

给定`N`个数字和`Q`个查询，每个查询都由`L`和`R`组成。任务是编写一个打印数字计数的程序，该程序将给定范围`L-R`中的所有数字相除。

**示例**：

```
Input : a = {3, 4, 2, 2, 4, 6} 
        Q = 2
        L = 1 R = 4  
        L = 2 R = 6

Output :  0
          2 

Explanation : The range 1-4 has {3, 4, 2, 2} 
which does not have any number that divides all the 
numbers in this range. 
The range 2-6 has {4, 2, 2, 4, 6} which has  2 numbers {2, 2} which divides 
all numbers in the given range. 

Input: a = {1, 2, 3, 5} 
       Q = 2 
       L = 1 R = 4 
       L = 2 R = 4 
Output: 1 
        0      

```

**朴素的方法**：针对每个查询从范围`L-R`进行迭代，并检查索引`i`处的给定元素是否将范围中的所有数字相除。 我们对所有元素进行计数，将所有数字相除。 在最坏情况下，每个查询的复杂度将为`O(n^2)`。

**以下是朴素方法的实现**：

## C++ 

```cpp

// CPP program to Count elements which 
// divides all numbers in range L-R 
#include <bits/stdc++.h> 
using namespace std; 

// function to count element 
// Time complexity O(n^2) worst case 
int answerQuery(int a[], int n,  
                int l, int r) 
{ 
    // answer for query 
    int count = 0; 

    // 0 based index 
    l = l - 1; 

    // iterate for all elements 
    for (int i = l; i < r; i++)  
    { 
        int element = a[i]; 
        int divisors = 0; 

        // check if the element divides 
        // all numbers in range 
        for (int j = l; j < r; j++)  
        { 
            // no of elements 
            if (a[j] % a[i] == 0) 
                divisors++; 
            else
                break; 
        } 

        // if all elements are divisible by a[i] 
        if (divisors == (r - l)) 
            count++; 
    } 

    // answer for every query 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int a[] = { 1, 2, 3, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    int l = 1, r = 4; 
    cout << answerQuery(a, n, l, r) << endl; 

    l = 2, r = 4;     
    cout << answerQuery(a, n, l, r) << endl; 
    return 0; 
} 

```

## Java

```
// Java program to Count elements which 
// divides all numbers in range L-R 
import java.io.*; 
  
class GFG  
{ 
  
// function to count element 
// Time complexity O(n^2) worst case 
static int answerQuery(int a[], int n,  
                       int l, int r) 
{ 
    // answer for query 
    int count = 0; 
  
    // 0 based index 
    l = l - 1; 
  
    // iterate for all elements 
    for (int i = l; i < r; i++)  
    { 
        int element = a[i]; 
        int divisors = 0; 
  
        // check if the element divides 
        // all numbers in range 
        for (int j = l; j < r; j++)  
        { 
            // no of elements 
            if (a[j] % a[i] == 0) 
                divisors++; 
            else
                break; 
        } 
          
        // if all elements are divisible by a[i] 
        if (divisors == (r - l)) 
            count++; 
    } 
  
    // answer for every query 
    return count; 
} 
  
// Driver Code 
public static void main (String[] args)  
{ 
    int a[] = { 1, 2, 3, 5 }; 
    int n = a.length; 
      
    int l = 1, r = 4; 
    System.out.println( answerQuery(a, n, l, r)); 
      
    l = 2; r = 4;  
    System.out.println( answerQuery(a, n, l, r)); 
} 
} 
  
// This code is contributed by anuj_67..
```

## Python3

```
# Python 3 program to Count elements which 
# divides all numbers in range L-R 
  
# function to count element 
# Time complexity O(n^2) worst case 
def answerQuery(a, n, l, r): 
      
    # answer for query 
    count = 0
  
    # 0 based index 
    l = l - 1
  
    # iterate for all elements 
    for i in range(l, r, 1): 
        element = a[i] 
        divisors = 0
  
        # check if the element divides 
        # all numbers in range 
        for j in range(l, r, 1): 
              
            # no of elements 
            if (a[j] % a[i] == 0): 
                divisors += 1
            else: 
                break
          
        # if all elements are divisible 
        # by a[i] 
        if (divisors == (r - l)): 
            count += 1
  
    # answer for every query 
    return count 
  
# Driver Code 
if __name__ =='__main__': 
    a = [1, 2, 3, 5] 
    n = len(a) 
  
    l = 1
    r = 4
    print(answerQuery(a, n, l, r)) 
  
    l = 2
    r = 4
    print(answerQuery(a, n, l, r)) 
  
# This code is contributed by 
# Shashank_Sharma
```

## C#

```
// C# program to Count elements which 
// divides all numbers in range L-R 
using System; 
  
class GFG  
{ 
  
// function to count element 
// Time complexity O(n^2) worst case 
static int answerQuery(int []a, int n,  
                       int l, int r) 
{ 
    // answer for query 
    int count = 0; 
  
    // 0 based index 
    l = l - 1; 
  
    // iterate for all elements 
    for (int i = l; i < r; i++)  
    { 
        //int element = a[i]; 
        int divisors = 0; 
  
        // check if the element divides 
        // all numbers in range 
        for (int j = l; j < r; j++)  
        { 
            // no of elements 
            if (a[j] % a[i] == 0) 
                divisors++; 
            else
                break; 
        } 
          
        // if all elements are divisible by a[i] 
        if (divisors == (r - l)) 
            count++; 
    } 
  
    // answer for every query 
    return count; 
} 
  
// Driver Code 
public static void Main ()  
{ 
    int []a = { 1, 2, 3, 5 }; 
    int n = a.Length; 
      
    int l = 1, r = 4; 
    Console.WriteLine(answerQuery(a, n, l, r)); 
      
    l = 2; r = 4;  
    Console.WriteLine(answerQuery(a, n, l, r)); 
} 
} 
  
// This code is contributed by anuj_67..
```

## PHP

```
<?php 
// PHP program to Count elements which 
// divides all numbers in range L-R 
  
// function to count element 
// Time complexity O(n^2) worst case 
function answerQuery($a, $n, $l, $r) 
{ 
    // answer for query 
    $count = 0; 
  
    // 0 based index 
    $l = $l - 1; 
  
    // iterate for all elements 
    for ($i = $l; $i < $r; $i++)  
    { 
        $element = $a[$i]; 
        $divisors = 0; 
  
        // check if the element divides 
        // all numbers in range 
        for ($j = $l; $j < $r; $j++)  
        { 
            // no of elements 
            if ($a[$j] % $a[$i] == 0) 
                $divisors++; 
            else
                break; 
        } 
          
        // if all elements are divisible by a[i] 
        if ($divisors == ($r - $l)) 
            $count++; 
    } 
  
    // answer for every query 
    return $count; 
} 
  
// Driver Code 
$a = array(1, 2, 3, 5); 
$n = sizeof($a); 
  
$l = 1; $r = 4; 
echo answerQuery($a, $n, $l, $r) . "\n"; 
  
$l = 2; $r = 4;  
echo answerQuery($a, $n, $l, $r) . "\n"; 
  
// This code is contributed 
// by Akanksha Rai
```

输出：

```
0
2
```

时间复杂度：由于树的构造需要`O(n)`且找出 gcd 的需要花费`O(log n)`，所以树的构造的时间复杂度为`O(n log n)`。 在最坏的情况下，每个查询所花费的时间为`O(log n * log n)`，因为内置函数`__gcd`需要`O(log n)`。