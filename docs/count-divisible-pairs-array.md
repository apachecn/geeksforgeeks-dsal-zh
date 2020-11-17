# 计算数组中的可分割对的数量

> 原文：[https://www.geeksforgeeks.org/count-divisible-pairs-array/](https://www.geeksforgeeks.org/count-divisible-pairs-array/)

给定一个数组，对数组中的对进行计数，以使该对中的一个元素除以另一个。

例子：

```
Input  : arr[] = {1, 2, 3}
Output : 2
The two pairs are (1, 2) and (1, 3)

Input : arr[] = {2, 3, 5, 7}
Output: 0

```

## C++

```cpp

// CPP program to count divisible pairs. 
#include <bits/stdc++.h> 
using namespace std; 

int countDivisibles(int arr[], int n) 
{ 
    int res = 0; 

    // Iterate through all pairs 
    for (int i=0; i<n; i++)  
      for (int j=i+1; j<n; j++)  

         // Increment count if one divides 
         // other 
         if (arr[i] % arr[j] == 0 ||  
             arr[j] % arr[i] == 0)  
               res++; 

    return res; 
} 

int main() 
{ 
    int a[] = {1, 2, 3, 9}; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << countDivisibles(a, n); 
    return 0; 
} 

```

## Java

```java

// Java program to count 
// divisible pairs. 

class GFG { 

// Function returns count 
// of divisible pairs 
static int countDivisibles(int arr[],  
                              int n) 
{ 
    int res = 0; 

    // Iterate through all pairs 
    for (int i = 0; i < n; i++)  
        for (int j = i + 1; j < n; j++)  

        // Increment count if 
        // one divides other 
        if (arr[i] % arr[j] == 0 ||  
            arr[j] % arr[i] == 0)  
            res++; 

    return res; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int a[] = new int[]{1, 2, 3, 9}; 
    int n = a.length; 
    System.out.print(countDivisibles(a, n)); 
} 
} 

// This code is contributed by Smitha. 

```

## Python3

```py

# Python3 program to count  
# divisible pairs.  

def countDivisibles(arr, n) : 

    res = 0

    # Iterate through all pairs  
    for i in range(0, n) : 
        for j in range(i+1, n) : 

            # Increment count if one divides  
            # other  
            if (arr[i] % arr[j] == 0 or
            arr[j] % arr[i] == 0) : 
                res+=1

    return res  

# Driver code  
if __name__=='__main__': 
    a = [1, 2, 3, 9] 
    n = len(a)  
    print(countDivisibles(a, n) ) 

# this code is contributed by  
# Smitha Dinesh Semwal     

```

## C#

```cs

// Java program to count 
// divisible pairs. 
using System; 

class GFG { 

// Function returns count 
// of divisible pairs 
static int countDivisibles(int []arr,  
                              int n) 
{ 
    int res = 0; 

    // Iterate through all pairs 
    for (int i = 0; i < n; i++)  
        for (int j = i + 1; j < n; j++)  

        // Increment count if 
        // one divides other 
        if (arr[i] % arr[j] == 0 ||  
            arr[j] % arr[i] == 0)  
            res++; 

    return res; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int[] a = new int[4] {1, 2, 3, 9}; 
    int n = a.Length; 
    Console.Write(countDivisibles(a, n)); 
} 
} 

// This code is contributed by Smitha. 

```

## PHP

```php

<?php 
// PHP program to count divisible pairs. 
function countDivisibles($arr, $n) 
{ 
    $res = 0; 

    // Iterate through all pairs 
    for ($i = 0; $i < $n; $i++)  
    for ($j = $i + 1; $j < $n; $j++)  

        // Increment count if one divides 
        // other 
        if ($arr[$i] % $arr[$j] == 0 ||  
            $arr[$j] % $arr[$i] == 0)  
            $res++; 

    return $res; 
} 
$a = array(1, 2, 3, 9); 
$n = count($a); 
echo (countDivisibles($a, $n)); 
?> 

```

**输出**：

```
4

```

**有效的解决方案**，适用于小范围的数字。

1.  将数组的所有元素插入哈希表。

2.  查找数组中的最大元素。

3.  对于每个数组元素，在哈希表中搜索它的倍数（最大）。 如果找到，则增加结果。

此处也可以通过对方法稍加修改来处理不同情况，例如负数和重复。



* * *

* * *



