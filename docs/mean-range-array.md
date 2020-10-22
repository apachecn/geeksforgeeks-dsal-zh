# 数组范围的平均值

> 原文： [https://www.geeksforgeeks.org/mean-range-array/](https://www.geeksforgeeks.org/mean-range-array/)

给定`n`个整数数组。 给出`q`个查询。 编写一个程序，在新行中为每个查询打印从`l`到`r`范围内的均值的下限值。

**示例**：

```
Input : arr[] = {1, 2, 3, 4, 5}
        q = 3
        0 2
        1 3
        0 4
Output : 2
         3
         3
Here for 0 to 2 (1 + 2 + 3) / 3 = 2

Input : arr[] = {6, 7, 8, 10}
        q = 2
        0 3
        1 2
Output : 7
         7

```



**朴素的方法**：我们可以为每个查询`l`到`r`运行循环，并找到范围内元素的总和和数量。 此后，我们可以为每个查询打印均值下限。

## C++ 

```cpp

// CPP program to find floor value 
// of mean in range l to r 
#include <bits/stdc++.h> 
using namespace std; 

// To find mean of range in l to r 
int findMean(int arr[], int l, int r) 
{ 
    // Both sum and count are 
    // initialize to 0 
    int sum = 0, count = 0; 

    // To calculate sum and number 
    // of elements in range l to r 
    for (int i = l; i <= r; i++) { 
        sum += arr[i]; 
        count++; 
    } 

    // Calculate floor value of mean 
    int mean = floor(sum / count); 

    // Returns mean of array 
    // in range l to r 
    return mean; 
} 

// Driver program to test findMean() 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    cout << findMean(arr, 0, 2) << endl; 
    cout << findMean(arr, 1, 3) << endl; 
    cout << findMean(arr, 0, 4) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to find floor value 
// of mean in range l to r 
public class Main { 
  
    // To find mean of range in l to r 
    static int findMean(int arr[], int l, int r) 
    { 
        // Both sum and count are 
        // initialize to 0 
        int sum = 0, count = 0; 
  
        // To calculate sum and number 
        // of elements in range l to r 
        for (int i = l; i <= r; i++) { 
            sum += arr[i]; 
            count++; 
        } 
  
        // Calculate floor value of mean 
        int mean = (int)Math.floor(sum / count); 
  
        // Returns mean of array 
        // in range l to r 
        return mean; 
    } 
  
    // Driver program to test findMean() 
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 2, 3, 4, 5 }; 
        System.out.println(findMean(arr, 0, 2)); 
        System.out.println(findMean(arr, 1, 3)); 
        System.out.println(findMean(arr, 0, 4)); 
    } 
}
```

## Python3

```py
# Python 3 program to find floor value 
# of mean in range l to r 
import math 
  
# To find mean of range in l to r 
def findMean(arr, l, r): 
      
    # Both sum and count are 
    # initialize to 0 
    sum, count = 0, 0
      
    # To calculate sum and number 
    # of elements in range l to r 
    for i in range(l, r + 1): 
        sum += arr[i] 
        count += 1
  
    # Calculate floor value of mean 
    mean = math.floor(sum / count) 
  
    # Returns mean of array 
    # in range l to r 
    return mean 
  
# Driver Code 
arr = [ 1, 2, 3, 4, 5 ] 
      
print(findMean(arr, 0, 2)) 
print(findMean(arr, 1, 3)) 
print(findMean(arr, 0, 4)) 
  
# This code is contributed  
# by PrinciRaj1992
```

## C#

```cs
//C# program to find floor value 
// of mean in range l to r 
using System; 
  
public class GFG { 
   
    // To find mean of range in l to r 
    static int findMean(int []arr, int l, int r) 
    { 
        // Both sum and count are 
        // initialize to 0 
        int sum = 0, count = 0; 
   
        // To calculate sum and number 
        // of elements in range l to r 
        for (int i = l; i <= r; i++) { 
            sum += arr[i]; 
            count++; 
        } 
   
        // Calculate floor value of mean 
        int mean = (int)Math.Floor((double)sum / count); 
   
        // Returns mean of array 
        // in range l to r 
        return mean; 
    } 
   
    // Driver program to test findMean() 
    public static void Main() 
    { 
        int []arr = { 1, 2, 3, 4, 5 }; 
        Console.WriteLine(findMean(arr, 0, 2)); 
        Console.WriteLine(findMean(arr, 1, 3)); 
        Console.WriteLine(findMean(arr, 0, 4)); 
    } 
} 
  
/*This code is contributed by PrinciRaj1992*/
```

## PHP

```php
<?php 
// PHP program to find floor  
// value of mean in range l to r 
  
// To find mean of  
// range in l to r 
function findMean($arr, $l, $r) 
{ 
    // Both sum and count  
    // are initialize to 0 
    $sum = 0; 
    $count = 0; 
  
    // To calculate sum and  
    // number of elements in 
    // range l to r 
    for ($i = $l; $i <= $r; $i++)  
    { 
        $sum += $arr[$i]; 
        $count++; 
    } 
  
    // Calculate floor  
    // value of mean 
    $mean = floor($sum / $count); 
  
    // Returns mean of array 
    // in range l to r 
    return $mean; 
} 
  
// Driver Code 
$arr = array(1, 2, 3, 4, 5); 
echo findMean($arr, 0, 2), "\n"; 
echo findMean($arr, 1, 3), "\n"; 
echo findMean($arr, 0, 4), "\n"; 
  
// This code is contributed by ajit 
?>
```

输出：

```
2
3
3
```

时间复杂度：`O(n)`。

高效的方法：我们可以使用前缀和来求和。 `prefixSum[i]`表示前`i`个元素的总和。 因此，范围从`l`到`r`的数字总和将是`prefixSum[r] – prefixSum[l-1]`。 从`l`到`r`范围内的元素数将为`r – l + 1`。因此，我们现在可以在`O(1)`中打印从`l`到`r`范围的均值。

## C++

```cpp
// CPP program to find floor value 
// of mean in range l to r 
#include <bits/stdc++.h> 
#define MAX 1000005 
using namespace std; 
  
int prefixSum[MAX]; 
  
// To calculate prefixSum of array 
void calculatePrefixSum(int arr[], int n) 
{ 
    // Calculate prefix sum of array 
    prefixSum[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
        prefixSum[i] = prefixSum[i - 1] + arr[i]; 
} 
  
// To return floor of mean 
// in range l to r 
int findMean(int l, int r) 
{ 
    if (l == 0) 
      return floor(prefixSum[r]/(r+1)); 
  
    // Sum of elements in range l to 
    // r is prefixSum[r] - prefixSum[l-1] 
    // Number of elements in range 
    // l to r is r - l + 1 
    return floor((prefixSum[r] -  
          prefixSum[l - 1]) / (r - l + 1)); 
} 
  
// Driver program to test above functions 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    calculatePrefixSum(arr, n); 
    cout << findMean(0, 2) << endl; 
    cout << findMean(1, 3) << endl; 
    cout << findMean(0, 4) << endl; 
    return 0; 
}
```

## Java

```java
// Java program to find floor value 
// of mean in range l to r 
public class Main { 
public static final int MAX = 1000005; 
    static int prefixSum[] = new int[MAX]; 
  
    // To calculate prefixSum of array 
    static void calculatePrefixSum(int arr[], int n) 
    { 
        // Calculate prefix sum of array 
        prefixSum[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            prefixSum[i] = prefixSum[i - 1] + arr[i]; 
    } 
  
    // To return floor of mean 
    // in range l to r 
    static int findMean(int l, int r) 
    { 
        if (l == 0) 
           return (int)Math.floor(prefixSum[r] / (r + 1)); 
          
        // Sum of elements in range l to 
        // r is prefixSum[r] - prefixSum[l-1] 
        // Number of elements in range 
        // l to r is r - l + 1 
        return (int)Math.floor((prefixSum[r] - 
                prefixSum[l - 1]) / (r - l + 1)); 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 2, 3, 4, 5 }; 
        int n = arr.length; 
        calculatePrefixSum(arr, n); 
        System.out.println(findMean(1, 2)); 
        System.out.println(findMean(1, 3)); 
        System.out.println(findMean(1, 4)); 
    } 
}
```

## Python3

```py
# Python3 program to find floor value 
# of mean in range l to r 
import math as mt 
  
MAX = 1000005
prefixSum = [0 for i in range(MAX)] 
  
# To calculate prefixSum of array 
def calculatePrefixSum(arr, n): 
  
    # Calculate prefix sum of array 
    prefixSum[0] = arr[0] 
  
    for i in range(1,n): 
        prefixSum[i] = prefixSum[i - 1] + arr[i] 
  
# To return floor of mean 
# in range l to r 
def findMean(l, r): 
  
    if (l == 0): 
        return mt.floor(prefixSum[r] / (r + 1)) 
  
    # Sum of elements in range l to 
    # r is prefixSum[r] - prefixSum[l-1] 
    # Number of elements in range 
    # l to r is r - l + 1 
    return (mt.floor((prefixSum[r] - 
                      prefixSum[l - 1]) /
                          (r - l + 1))) 
  
# Driver Code 
arr = [1, 2, 3, 4, 5] 
  
n = len(arr) 
  
calculatePrefixSum(arr, n) 
print(findMean(0, 2)) 
print(findMean(1, 3)) 
print(findMean(0, 4)) 
  
# This code is contributed by Mohit Kumar
```

## C#

```cs
// C# program to find floor value 
// of mean in range l to r 
using System; 
                      
public class GFG { 
public static readonly int MAX = 1000005; 
    static int []prefixSum = new int[MAX]; 
   
    // To calculate prefixSum of array 
    static void calculatePrefixSum(int []arr, int n) 
    { 
        // Calculate prefix sum of array 
        prefixSum[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            prefixSum[i] = prefixSum[i - 1] + arr[i]; 
    } 
   
    // To return floor of mean 
    // in range l to r 
    static int findMean(int l, int r) 
    { 
        if (l == 0) 
           return (int)Math.Floor((double)(prefixSum[r] / (r + 1))); 
           
        // Sum of elements in range l to 
        // r is prefixSum[r] - prefixSum[l-1] 
        // Number of elements in range 
        // l to r is r - l + 1 
        return (int)Math.Floor((double)(prefixSum[r] - 
                prefixSum[l - 1]) / (r - l + 1)); 
    } 
   
    // Driver program to test above functions 
    public static void Main() 
    { 
        int []arr = { 1, 2, 3, 4, 5 }; 
        int n = arr.Length; 
        calculatePrefixSum(arr, n); 
        Console.WriteLine(findMean(1, 2)); 
        Console.WriteLine(findMean(1, 3)); 
        Console.WriteLine(findMean(1, 4)); 
    } 
} 
  
//This code is contributed by PrinciRaj1992
```

输出：

```
2
3
3
```

