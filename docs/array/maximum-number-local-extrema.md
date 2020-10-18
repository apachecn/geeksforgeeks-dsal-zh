# 数组中局部极值的数量

> 原文： [https://www.geeksforgeeks.org/maximum-number-local-extrema/](https://www.geeksforgeeks.org/maximum-number-local-extrema/)

您将获得一个包含`n`个元素的数组。 极值是大于其两个邻居或小于其两个邻居的元素。 您必须计算给定数组中局部极值的数量。

**注意**：第一个和最后一个元素不是极值。

**示例**：

```
Input : a[] = {1, 5, 2, 5}
Output : 2

Input : a[] = {1, 2, 3}
Output : 0

```



**方法**：为了计算极值，我们必须检查一个元素是最大值还是最小值，即该元素是大于其两个邻居还是小于两个邻居。 为此，只需在数组上进行迭代，然后对每个元素检查其成为极值的可能性。

**注意**： `a[0]`和`a[n-1]`分别只有一个邻居，它们既不是最小值也不是最大值。

## C++ 

```cpp

// CPP to find number 
// of extrema 
#include <bits/stdc++.h> 
using namespace std; 

// function to find  
// local extremum 
int extrema(int a[], int n) 
{ 
    int count = 0; 

    // start loop from position 1 
    // till n-1 
    for (int i = 1; i < n - 1; i++) 
    { 

        // only one condition 
        // will be true at a   
        // time either a[i]  
        // will be greater than 
        // neighbours or less  
        // than neighbours 

        // check if a[i] is greater 
        // than both its neighbours 
        // then add 1 to x 
        count += (a[i] > a[i - 1] && a[i] > a[i + 1]); 

        // check if a[i] is  
        // less than both its  
        // neighbours, then  
        // add 1 to x 
        count += (a[i] < a[i - 1] && a[i] < a[i + 1]); 
    } 

    return count; 
} 

// driver program 
int main() 
{ 
    int a[] = { 1, 0, 2, 1 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << extrema(a, n); 
    return 0; 
} 

```

## Java

```java

// Java to find  
// number of extrema 
import java.io.*; 

class GFG { 

    // function to find  
    // local extremum 
    static int extrema(int a[], int n) 
    { 
        int count = 0; 

        // start loop from  
        // position 1 till n-1 
        for (int i = 1; i < n - 1; i++)  
        { 

            // only one condition 
            // will be true at a   
            // time either a[i]  
            // will be greater than 
            // neighbours or less  
            // than neighbours 

            // check if a[i] is greater 
            // than both its neighbours 
            // then add 1 to x 
            if(a[i] > a[i - 1] && a[i] > a[i + 1]) 
                count += 1; 

            // check if a[i] is  
            // less than both its  
            // neighbours, then  
            // add 1 to x 
            if(a[i] < a[i - 1] && a[i] < a[i + 1]) 
                count += 1; 
        } 

        return count; 
    } 

    // driver program 
    public static void main(String args[]) 
                            throws IOException 
    { 
        int a[] = { 1, 0, 2, 1 }; 
        int n = a.length; 
        System.out.println(extrema(a, n)); 
    } 
} 

/* This code is contributed by Nikita Tiwari.*/

```

## Python3

```py

# Python 3 to find 
# number of extrema 

# function to find 
# local extremum 
def extrema(a, n): 

    count = 0
    # start loop from 
    # position 1 till n-1 
    for i in range(1, n - 1) : 
        # only one condition  
        # will be true  
        # at a time either 
        # a[i] will be greater  
        # than neighbours or  
        # less than neighbours 

        # check if a[i] if 
        # greater than both its  
        # neighbours, then add  
        # 1 to x 
        count += (a[i] > a[i - 1] and a[i] > a[i + 1]); 

        # check if a[i] if 
        # less than both its  
        # neighbours, then  
        # add 1 to x 
        count += (a[i] < a[i - 1] and a[i] < a[i + 1]); 

    return count 

# driver program 
a = [1, 0, 2, 1 ] 
n = len(a) 
print(extrema(a, n)) 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# to find  
// number of extrema 
using System; 

class GFG { 

    // function to find  
    // local extremum 
    static int extrema(int []a, int n) 
    { 
        int count = 0; 

        // start loop from  
        // position 1 till n-1 
        for (int i = 1; i < n - 1; i++)  
        { 

            // only one condition 
            // will be true at a  
            // time either a[i]  
            // will be greater than 
            // neighbours or less  
            // than neighbours 

            // check if a[i] is greater 
            // than both its neighbours 
            // then add 1 to x 
            if(a[i] > a[i - 1] && a[i] > a[i + 1]) 
                count += 1; 

            // check if a[i] is  
            // less than both its  
            // neighbours, then  
            // add 1 to x 
            if(a[i] < a[i - 1] && a[i] < a[i + 1]) 
                count += 1; 
        } 

        return count; 
    } 

    // Driver program 
    public static void Main() 

    { 
        int []a = { 1, 0, 2, 1 }; 
        int n = a.Length; 
    Console.WriteLine(extrema(a, n)); 
    } 
} 

/* This code is contributed by vt_m.*/

```

## PHP

```php

<?php 
// PHP to find number 
// of extrema 

// function to find  
// local extremum 
function extrema($a, $n) 
{ 
    $count = 0; 

    // start loop from position 1 
    // till n-1 
    for ($i = 1; $i < $n - 1; $i++) 
    { 

        // only one condition 
        // will be true at a  
        // time either a[i]  
        // will be greater than 
        // neighbours or less  
        // than neighbours 

        // check if a[i] is greater 
        // than both its neighbours 
        // then add 1 to x 
        $count += ($a[$i] > $a[$i - 1] and 
                   $a[$i] > $a[$i + 1]); 

        // check if a[i] is  
        // less than both its  
        // neighbours, then  
        // add 1 to x 
        $count += ($a[$i] < $a[$i - 1] and 
                   $a[$i] < $a[$i + 1]); 
    } 

    return $count; 
} 

// Driver Code 
$a = array( 1, 0, 2, 1 ); 
$n = count($a); 
echo extrema($a, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
2

```



* * *

* * *



