# 每次成功搜索后通过将元素加倍来重复搜索

> 原文： [https://www.geeksforgeeks.org/repeatedly-search-element-doubling-every-successful-search/](https://www.geeksforgeeks.org/repeatedly-search-element-doubling-every-successful-search/)

给定一个数组`a[]`和整数`b`。 查找`b`是否存在于`a[]`中。 如果存在，则将`b`的值加倍并再次搜索。 我们重复这些步骤，直到找不到`b`。 最后，我们返回`b`的值。

例子：

```
Input : a[] = {1, 2, 3}
          b = 1 
Output :4
Initially we start with b = 1\. Since 
it is present in array, it becomes 2.
Now 2 is also present in array b becomes 4 .
Since 4 is not present, we return 4.

Input : a[] = {1 3 5 2 12}
          b = 3 
Output :6

```

问题来源：在 Yatra.com 在线测试中提出



1.  对输入数组进行排序。

2.  继续进行二分搜索并加倍，直到不存在该元素。

以下代码在 STL 中使用[`binary_search()`](https://www.geeksforgeeks.org/binary-search-algorithms-the-c-standard-template-library-stl/)

## C++ 

```cpp

// C++ program to repeatedly search an element by 
// doubling it after every successful search 
#include <bits/stdc++.h> 
using namespace std; 

int findElement(int a[], int n, int b) 
{ 
    // Sort the given array so that binary search 
    // can be applied on it 
    sort(a, a + n); 

    int max = a[n - 1]; // Maximum array element 

    while (b < max) { 

        // search for the element b present or 
        // not in array 
        if (binary_search(a, a + n, b)) 
            b *= 2; 
        else
            return b; 
    } 

    return b; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 3 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int b = 1; 
    cout << findElement(a, n, b); 
    return 0; 
} 

```

## Java

```java
// Java program to repeatedly search an element by 
// doubling it after every successful search 
import java.util.Arrays; 
public class Test4 { 
  
    static int findElement(int a[], int n, int b) 
    { 
        // Sort the given array so that binary search 
        // can be applied on it 
        Arrays.sort(a); 
  
        int max = a[n - 1]; // Maximum array element 
  
        while (b < max) { 
  
            // search for the element b present or 
            // not in array 
            if (Arrays.binarySearch(a, b) > -1) 
                b *= 2; 
            else
                return b; 
        } 
  
        return b; 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int a[] = { 1, 2, 3 }; 
        int n = a.length; 
        int b = 1; 
        System.out.println(findElement(a, n, b)); 
    } 
} 
// This article is contributed by Sumit Ghosh
```

## Python

```py
# Python program to repeatedly search an element by 
# doubling it after every successful search 
  
def binary_search(a, x, lo = 0, hi = None): 
    if hi is None: 
        hi = len(a) 
    while lo < hi: 
        mid = (lo + hi)//2
        midval = a[mid] 
        if midval < x: 
            lo = mid + 1
        elif midval > x:  
            hi = mid 
        else: 
            return mid 
    return -1
  
def findElement(a, n, b): 
     
    # Sort the given array so that binary search 
    # can be applied on it 
    a.sort() 
   
    mx = a[n - 1] # Maximum array element 
   
    while (b < max): 
          
        # search for the element b present or 
        # not in array 
        if (binary_search(a, b, 0, n) != -1): 
            b *= 2
        else: 
            return b 
    return b 
   
# Driver code 
a = [ 1, 2, 3 ] 
n = len(a) 
b = 1
print findElement(a, n, b) 
  
# This code is contributed by Sachin Bisht
```

## C#

```cs
// C# program to repeatedly search an 
// element by doubling it after every 
// successful search 
using System; 
  
public class GFG { 
  
    static int findElement(int[] a, 
                           int n, int b) 
    { 
  
        // Sort the given array so that 
        // binary search can be applied 
        // on it 
        Array.Sort(a); 
  
        // Maximum array element 
        int max = a[n - 1]; 
  
        while (b < max) { 
  
            // search for the element b 
            // present or not in array 
            if (Array.BinarySearch(a, b) > -1) 
                b *= 2; 
            else
                return b; 
        } 
  
        return b; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] a = { 1, 2, 3 }; 
        int n = a.Length; 
        int b = 1; 
        Console.WriteLine(findElement(a, n, b)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// Php program to repeatedly search an element by 
// doubling it after every successful search 
  
function binary_search($a, $x, $lo=0, $hi=NULL) 
{ 
    if ($hi == NULL) 
        $hi = count($a); 
    while ($lo < $hi) { 
        $mid = ($lo + $hi) / 2; 
        $midval = $a[$mid]; 
        if ($midval < $x) 
            $lo = $mid + 1; 
        else if ($midval > $x) 
            $hi = $mid; 
        else
            return $mid; 
    } 
    return -1; 
} 
  
function findElement($a, $n, $b) 
{ 
// Sort the given array so that binary search 
// can be applied on it 
    sort($a); 
  
    $mx = $a[$n - 1]; // Maximum array element 
  
while ($b < max($a)) { 
  
// search for the element b present or 
// not in array 
    if (binary_search($a, $b, 0, $n) != -1) 
        $b *= 2; 
    else
        return $b; 
} 
return $b; 
} 
  
// Driver code 
$a = array(1, 2, 3 ); 
$n = count($a); 
$b = 1; 
echo findElement($a, $n, $b); 
  
// This code is contributed by Srathore 
?>
```

输出：

```
4
```

