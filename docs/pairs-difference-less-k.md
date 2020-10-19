# 差异小于`K`的对

> 原文： [https://www.geeksforgeeks.org/pairs-difference-less-k/](https://www.geeksforgeeks.org/pairs-difference-less-k/)

给定一个由`n`个整数组成的数组，我们需要找到所有差异小于`k`的对。

**示例**：

```
Input : a[] = {1, 10, 4, 2}
        K = 3
Output : 2
We can make only two pairs 
with difference less than 3.
(1, 2) and (4, 2)

Input : a[] = {1, 8, 7}
        K = 7
Output : 2
Pairs with difference less than 7
are (1, 7) and (8, 7)

```



**方法 1（简单）**：运行两个嵌套循环。 外循环逐个选择每个元素`x`。 内部循环考虑`x`之后的所有元素，并检查差异是否在限制范围内。

## C++ 

```cpp

// CPP code to find count of Pairs with  
// difference less than K. 
#include <bits/stdc++.h> 
using namespace std; 

int countPairs(int a[], int n, int k) 
{ 
    int res = 0; 
    for (int i = 0; i < n; i++)  
      for (int j=i+1; j<n; j++) 
         if (abs(a[j] - a[i]) < k)  
            res++; 

    return res; 
} 

// Driver code 
int main() 
{ 
    int a[] =  {1, 10, 4, 2}; 
    int k = 3; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << countPairs(a, n, k) << endl;  
    return 0; 
} 

```

## Java

```
// java code to find count of Pairs with  
// difference less than K. 
import java.io.*; 
  
class GFG { 
    static int countPairs(int a[], int n, int k) 
    { 
        int res = 0; 
        for (int i = 0; i < n; i++)  
        for (int j = i + 1; j < n; j++) 
            if (Math.abs(a[j] - a[i]) < k)  
                res++; 
      
        return res; 
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int a[] = {1, 10, 4, 2}; 
        int k = 3; 
        int n = a.length; 
        System.out.println(countPairs(a, n, k));  
          
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```
# Python3 code to find count of Pairs   
# with difference less than K. 
  
def countPairs(a, n, k): 
    res = 0
    for i in range(n):  
        for j in range(i + 1, n): 
            if (abs(a[j] - a[i]) < k): 
                res += 1
  
    return res 
      
# Driver code 
a = [1, 10, 4, 2] 
k = 3
n = len(a) 
print(countPairs(a, n, k), end = "") 
  
# This code is contributed by Azkia Anam.
```

## C#

```
// C# code to find count of Pairs  
//  with difference less than K. 
using System; 
  
class GFG { 
      
    // Function to count pairs 
    static int countPairs(int []a, int n,  
                          int k) 
    { 
        int res = 0; 
        for (int i = 0; i < n; i++)  
        for (int j = i + 1; j < n; j++) 
            if (Math.Abs(a[j] - a[i]) < k)  
                res++; 
      
        return res; 
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int []a = {1, 10, 4, 2}; 
        int k = 3; 
        int n = a.Length; 
        Console.WriteLine(countPairs(a, n, k));  
          
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// PHP code to find count of Pairs 
// with difference less than K. 
  
function countPairs( $a, $n, $k) 
{ 
    $res = 0; 
    for($i = 0; $i < $n; $i++)  
    for($j = $i + 1; $j < $n; $j++) 
        if (abs($a[$j] - $a[$i]) < $k)  
            $res++; 
  
    return $res; 
} 
  
    // Driver code 
    $a = array(1, 10, 4, 2); 
    $k = 3; 
    $n = count($a); 
    echo countPairs($a, $n, $k);  
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
  2
```

时间复杂度：`O(n ^ 2)`。

辅助空间：`O(1)`。

方法 2（排序）：首先我们对数组进行排序。 然后我们从第一个元素开始，并在差小于`k`的情况下继续考虑对。 如果在发现差异大于或等于`k`时停止循环，则移至下一个元素。

## C++

```
// CPP code to find count of Pairs with  
// difference less than K. 
#include <bits/stdc++.h> 
using namespace std; 
  
int countPairs(int a[], int n, int k) 
{ 
    // to sort the array. 
    sort(a, a + n); 
  
    int res = 0; 
    for (int i = 0; i < n; i++) { 
  
        // Keep incrementing result while 
        // subsequent elements are within 
        // limits. 
        int j = i+1;  
        while (j < n && a[j] - a[i] < k) { 
            res++; 
            j++; 
        } 
    } 
    return res; 
} 
  
// Driver code 
int main() 
{ 
    int a[] =  {1, 10, 4, 2}; 
    int k = 3; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << countPairs(a, n, k) << endl;  
    return 0; 
}
```

## Java

```
// Java code to find count of Pairs with  
// difference less than K. 
import java.io.*; 
import java.util.Arrays; 
  
class GFG 
{ 
    static int countPairs(int a[], int n, int k) 
    { 
        // to sort the array. 
        Arrays.sort(a); 
      
        int res = 0; 
        for (int i = 0; i < n; i++)  
        { 
      
            // Keep incrementing result while 
            // subsequent elements are within 
            // limits. 
            int j = i + 1;  
            while (j < n && a[j] - a[i] < k)  
            { 
                res++; 
                j++; 
            } 
        } 
        return res; 
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int a[] = {1, 10, 4, 2}; 
        int k = 3; 
        int n = a.length; 
        System.out.println(countPairs(a, n, k)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```
# Python code to find count of Pairs   
# with difference less than K. 
  
def countPairs(a, n, k): 
      
    # to sort the array 
    a.sort() 
    res = 0
    for i in range(n):  
          
        # Keep incrementing result while 
        # subsequent elements are within limits. 
        j = i+1
        while (j < n and a[j] - a[i] < k): 
            res += 1
            j += 1
    return res 
  
# Driver code 
a = [1, 10, 4, 2] 
k = 3
n = len(a) 
print(countPairs(a, n, k), end = "") 
  
# This code is contributed by Azkia Anam.
```

## C#

```
// C# code to find count of Pairs  
// with difference less than K. 
using System; 
  
class GFG { 
      
    // Function to count pairs 
    static int countPairs(int []a, int n, 
                          int k) 
    { 
          
        // to sort the array. 
        Array.Sort(a); 
      
        int res = 0; 
        for (int i = 0; i < n; i++)  
        { 
      
            // Keep incrementing result while 
            // subsequent elements are within 
            // limits. 
            int j = i + 1;  
            while (j < n && a[j] - a[i] < k)  
            { 
                res++; 
                j++; 
            } 
        } 
        return res; 
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int []a = {1, 10, 4, 2}; 
        int k = 3; 
        int n = a.Length; 
        Console.WriteLine(countPairs(a, n, k)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// PHP code to find count of  
// Pairs with difference less than K. 
  
function countPairs( $a, $n, $k) 
{ 
    // to sort the array. 
    sort($a); 
  
    $res = 0; 
    for ( $i = 0; $i < $n; $i++)  
    { 
  
        // Keep incrementing result  
        // while subsequent elements  
        // are within limits. 
        $j = $i + 1;  
        while ($j < $n and 
               $a[$j] - $a[$i] < $k)  
        { 
            $res++; 
            $j++; 
        } 
    } 
    return $res; 
} 
  
// Driver code 
$a = array(1, 10, 4, 2); 
$k = 3; 
$n = count($a); 
echo countPairs($a, $n, $k);  
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
  2
```

时间复杂度：`O(res)`，其中`res`是输出中的对数。 请注意，在最坏的情况下，这也需要`O(n ^ 2)`时间，但通常效果更好。