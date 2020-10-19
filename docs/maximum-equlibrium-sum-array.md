# 数组中的最大平衡和

> 原文： [https://www.geeksforgeeks.org/maximum-equlibrium-sum-array/](https://www.geeksforgeeks.org/maximum-equlibrium-sum-array/)

给定一个数组`arr[]`。 在`arr[]`中找到前缀和的最大值，它也是索引`i`的后缀和。

**示例**：

```
Input : arr[] = {-1, 2, 3, 0, 3, 2, -1}
Output : 4
Prefix sum of arr[0..3] = 
            Suffix sum of arr[3..6]

Input : arr[] = {-2, 5, 3, 1, 2, 6, -4, 2}
Output : 7
Prefix sum of arr[0..3] = 
              Suffix sum of arr[3..7]

```



**简单解决方案**一步一步地检查每个元素的给定条件（前缀和等于后缀和），然后返回满足给定条件的元素的最大值。

## C++ 

```cpp

// CPP program to find  
// maximum equilibrium sum. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find  
// maximum equilibrium sum. 
int findMaxSum(int arr[], int n) 
{ 
    int res = INT_MIN; 
    for (int i = 0; i < n; i++) 
    { 
    int prefix_sum = arr[i]; 
    for (int j = 0; j < i; j++) 
        prefix_sum += arr[j]; 

    int suffix_sum = arr[i]; 
    for (int j = n - 1; j > i; j--) 
        suffix_sum += arr[j]; 

    if (prefix_sum == suffix_sum) 
        res = max(res, prefix_sum); 
    } 
    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {-2, 5, 3, 1,  
                  2, 6, -4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findMaxSum(arr, n); 
    return 0; 
} 

```

## Java

```
// java program to find maximum
// equilibrium sum.
import java.io.*;
 
class GFG {
     
    // Function to find maximum 
    // equilibrium sum.
    static int findMaxSum(int []arr, int n)
    {
        int res = Integer.MIN_VALUE;
         
        for (int i = 0; i < n; i++)
        {
            int prefix_sum = arr[i];
             
            for (int j = 0; j < i; j++)
                prefix_sum += arr[j];
         
            int suffix_sum = arr[i];
             
            for (int j = n - 1; j > i; j--)
                suffix_sum += arr[j];
         
            if (prefix_sum == suffix_sum)
                res = Math.max(res, prefix_sum);
        }
         
        return res;
    }
     
    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {-2, 5, 3, 1, 2, 6, -4, 2 };
        int n = arr.length;
        System.out.println(findMaxSum(arr, n));
    }
}
 
// This code is contributed by anuj_67.
```

## Python3

```
# Python 3 program to find maximum 
# equilibrium sum.
import sys
 
# Function to find maximum equilibrium sum.
def findMaxSum(arr, n):
    res = -sys.maxsize - 1
    for i in range(n):
        prefix_sum = arr[i]
        for j in range(i):
            prefix_sum += arr[j]
 
        suffix_sum = arr[i]
        j = n - 1
        while(j > i):
            suffix_sum += arr[j]
            j -= 1
        if (prefix_sum == suffix_sum):
            res = max(res, prefix_sum)
 
    return res
 
# Driver Code
if __name__ == '__main__':
    arr = [-2, 5, 3, 1, 2, 6, -4, 2]
    n = len(arr)
    print(findMaxSum(arr, n))
 
# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find maximum
// equilibrium sum.
using System;
 
class GFG {
     
    // Function to find maximum 
    // equilibrium sum.
    static int findMaxSum(int []arr, int n)
    {
        int res = int.MinValue;
         
        for (int i = 0; i < n; i++)
        {
            int prefix_sum = arr[i];
             
            for (int j = 0; j < i; j++)
                prefix_sum += arr[j];
         
            int suffix_sum = arr[i];
             
            for (int j = n - 1; j > i; j--)
                suffix_sum += arr[j];
         
            if (prefix_sum == suffix_sum)
                res = Math.Max(res, prefix_sum);
        }
         
        return res;
    }
     
    // Driver Code
    public static void Main ()
    {
        int []arr = {-2, 5, 3, 1, 2, 6, -4, 2 };
        int n = arr.Length;
        Console.WriteLine(findMaxSum(arr, n));
    }
}
 
// This code is contributed by anuj_67.
```

## PHP

```
<?php
// PHP program to find
// maximum equilibrium sum.
 
// Function to find 
// maximum equilibrium sum.
function findMaxSum( $arr, $n)
{
    $res = PHP_INT_MIN;
    for ( $i = 0; $i < $n; $i++)
    {
    $prefix_sum = $arr[$i];
    for ( $j = 0; $j < $i; $j++)
        $prefix_sum += $arr[$j];
 
    $suffix_sum = $arr[$i];
    for ( $j = $n - 1; $j > $i; $j--)
        $suffix_sum += $arr[$j];
 
    if ($prefix_sum == $suffix_sum)
        $res = max($res, $prefix_sum);
    }
    return $res;
}
 
// Driver Code
$arr = array(-2, 5, 3, 1,
              2, 6, -4, 2 );
$n = count($arr);
echo findMaxSum($arr, $n);
 
// This code is contributed by anuj_67.
?>
```

输出：

```
7
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。

进一步优化：

通过首先计算总和，然后使用它来查找当前的前缀和后缀和，我们可以避免使用多余的空间。

## C++

```
// CPP program to find
// maximum equilibrium sum.
#include <bits/stdc++.h>
using namespace std;
 
// Function to find 
// maximum equilibrium sum.
int findMaxSum(int arr[], int n)
{
    int sum = accumulate(arr, arr + n, 0);
    int prefix_sum = 0, res = INT_MIN;
    for (int i = 0; i < n; i++)
    {
    prefix_sum += arr[i]; 
    if (prefix_sum == sum)
        res = max(res, prefix_sum); 
    sum -= arr[i];
    }
    return res;
}
 
// Driver Code
int main()
{
    int arr[] = { -2, 5, 3, 1, 
                   2, 6, -4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMaxSum(arr, n);
    return 0;
}
```

## Java

```
// Java program to find maximum equilibrium
// sum.
import java.lang.Math.*;
import java.util.stream.*;
 
class GFG {
     
    // Function to find maximum equilibrium
    // sum.
    static int findMaxSum(int arr[], int n)
    {
        int sum = IntStream.of(arr).sum();
        int prefix_sum = 0,
        res = Integer.MIN_VALUE;
         
        for (int i = 0; i < n; i++)
        {
            prefix_sum += arr[i]; 
             
            if (prefix_sum == sum)
                res = Math.max(res, prefix_sum); 
            sum -= arr[i];
        }
         
        return res;
    }
     
    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { -2, 5, 3, 1, 
                    2, 6, -4, 2 };
        int n = arr.length;
        System.out.print(findMaxSum(arr, n));
    }
}
 
// This code is contributed by Smitha.
```

## Python3

```
# Python3 program to find
# maximum equilibrium sum.
import sys
 
# Function to find 
# maximum equilibrium sum. 
def findMaxSum(arr,n):
     
    ss = sum(arr)
    prefix_sum = 0
    res = -sys.maxsize
     
    for i in range(n):
        prefix_sum += arr[i]
         
        if prefix_sum == ss:
            res = max(res, prefix_sum); 
             
        ss -= arr[i];
         
    return res
  
# Driver code   
if __name__=="__main__":
     
    arr = [ -2, 5, 3, 1, 
             2, 6, -4, 2 ]
    n = len(arr)
     
    print(findMaxSum(arr, n))
 
# This code is contributed by rutvik_56
```

## C#

```
// C# program to find maximum equilibrium sum.
using System.Linq;
using System;
 
class GFG {
     
    static int Add(int x, int y) { 
        return x + y; 
    } 
     
    // Function to find maximum equilibrium
    // sum.
    static int findMaxSum(int []arr, int n)
    {
        int sum = arr.Aggregate(func:Add);
        int prefix_sum = 0,
        res = int.MinValue;
         
        for (int i = 0; i < n; i++)
        {
            prefix_sum += arr[i]; 
             
            if (prefix_sum == sum)
                res = Math.Max(res, prefix_sum); 
            sum -= arr[i];
        }
         
        return res;
    }
     
    // Driver Code
    public static void Main()
    {
        int []arr = { -2, 5, 3, 1, 
                    2, 6, -4, 2 };
        int n = arr.Length;
        Console.Write(findMaxSum(arr, n));
    }
}
 
// This code is contributed by Smitha.
```

输出：

```
7
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。