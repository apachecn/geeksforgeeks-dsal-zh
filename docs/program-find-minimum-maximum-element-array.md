# 程序来查找数组的最小（或最大）元素

> 原文： [https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

给定一个数组，编写函数以查找其中的最小和最大元素。

## C++ 

```cpp

// CPP program to find minimum (or maximum) element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int getMin(int arr[], int n) 
{ 
    int res = arr[0]; 
    for (int i = 1; i < n; i++) 
        res = min(res, arr[i]); 
    return res; 
} 

int getMax(int arr[], int n) 
{ 
    int res = arr[0]; 
    for (int i = 1; i < n; i++) 
        res = max(res, arr[i]); 
    return res; 
} 

int main() 
{ 
    int arr[] = { 12, 1234, 45, 67, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum element of array: " << getMin(arr, n) << "\n"; 
    cout << "Maximum element of array: " << getMax(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find minimum (or maximum) 
// element in an array.
import java.io.*;
 
class GFG {
     
    static int getMin(int arr[], int n)
    {
        int res = arr[0];
         
        for (int i = 1; i < n; i++)
            res = Math.min(res, arr[i]);
        return res;
    }
     
    static int getMax(int arr[], int n)
    {
        int res = arr[0];
         
        for (int i = 1; i < n; i++)
            res = Math.max(res, arr[i]);
        return res;
    }
 
    // Driver code
    public static void main (String[] args) 
    {
        int arr[] = { 12, 1234, 45, 67, 1 };
        int n = arr.length;
        System.out.println( "Minimum element"
           + " of array: " + getMin(arr, n));
        System.out.println( "Maximum element"
           + " of array: " + getMax(arr, n));
    }
}
 
// This code is contributed by anuj_67.
```

## Python3

```py
# Python3 program to find minimum
# (or maximum) element in an array
 
# Minimum Function
def getMin(arr, n):
    res = arr[0]
    for i in range(1,n):
        res = min(res, arr[i])
    return res
 
# Maximum Function
def getMax(arr, n):
    res = arr[0]
    for i in range(1,n):
        res = max(res, arr[i])
    return res
 
# Driver Program
arr = [12, 1234, 45, 67, 1]
n = len(arr)
print ("Minimum element of array:", getMin(arr, n))
print ("Maximum element of array:", getMax(arr, n))
 
# This code is contributed 
# by Shreyanshi Arun.
```

## C#

```cs
// C# program to find 
// minimum (or maximum) 
// element in an array.
using System;
 
class GFG 
{
    static int getMin(int []arr,
                      int n)
    {
        int res = arr[0];
         
        for (int i = 1; i < n; i++)
            res = Math.Min(res, arr[i]);
        return res;
    }
     
    static int getMax(int []arr, 
                      int n)
    {
        int res = arr[0];
         
        for (int i = 1; i < n; i++)
            res = Math.Max(res, arr[i]);
        return res;
    }
 
    // Driver code
    public static void Main () 
    {
        int []arr = {12, 1234, 45, 67, 1};
        int n = arr.Length;
        Console.Write("Minimum element" + 
                          " of array: " + 
                         getMin(arr, n) + "\n" );
        Console.Write("Maximum element" + 
                          " of array: " + 
                         getMax(arr, n));
    }
}
 
// This code is contributed by Smita.
```

## PHP

```php
<?php
// PHP program to find minimum 
// (or maximum) element in an
// array.
 
function getMin($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = min($res, $arr[$i]);
    return $res;
}
 
function getMax($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = max($res, $arr[$i]);
    return $res;
}
 
    // Driver Code
    $arr = array(12, 1234, 45, 67, 1);
    $n = sizeof($arr);
    echo "Minimum element of array: "
           , getMin($arr, $n), "\n";
    echo "Maximum element of array: "
                  ,getMax($arr, $n);
 
// This code is contributed by ajit
?>
```

输出：

```
Minimum element of array: 1
Maximum element of array: 1234
```

时间复杂度：`O(n)`。

递归方案：

## C++

```cpp
// CPP program to find 
// minimum (or maximum) element
// in an array.
#include <bits/stdc++.h>
using namespace std;
 
int getMin(int arr[], int n)
{
    // If there is single element, return it.
    // Else return minimum of first element and
    // minimum of remaining array.
    return (n == 1) ? arr[0] : min(arr[0], 
                         getMin(arr + 1, n - 1));
}
 
int getMax(int arr[], int n)
{
    // If there is single element, return it.
    // Else return maximum of first element and
    // maximum of remaining array.
    return (n == 1) ? arr[0] : max(arr[0], 
                          getMax(arr + 1, n - 1));
}
 
int main()
{
    int arr[] = { 12, 1234, 45, 67, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum element of array: " << 
                            getMin(arr, n) << "\n";
    cout << "Maximum element of array: " << 
                                   getMax(arr, n);
    return 0;
}
```

## Java

```java
// Java program to find minimum 
// (or maximum) element
// in an array.
class GFG 
{
 
static int getMin(int arr[], int i, int n)
{
    // If there is single element, return it.
    // Else return minimum of first element and
    // minimum of remaining array.
    return (n == 1) ? arr[i] : Math.min(arr[i], 
                        getMin(arr,i + 1 , n - 1));
}
 
static int getMax(int arr[], int i, int n)
{
    // If there is single element, return it.
    // Else return maximum of first element and
    // maximum of remaining array.
    return (n == 1) ? arr[i] : Math.max(arr[i], 
                         getMax(arr ,i + 1, n - 1));
}
 
// Driver code
public static void main(String[] args) 
{
    int arr[] = { 12, 1234, 45, 67, 1 };
    int n = arr.length;
    System.out.print("Minimum element of array: " + 
                        getMin(arr, 0, n) + "\n");
    System.out.println("Maximum element of array: " + 
                        getMax(arr, 0, n));
    }
}
 
/* This code contributed by PrinciRaj1992 */
```

## Python3

```py
# Python3 program to find minimum 
# (or maximum) element in an array.
def getMin(arr, n):
    if(n==1):
        return arr[0]
    # If there is single element, return it. 
    # Else return minimum of first element 
    # and minimum of remaining array. 
    else:
        return min(getMin(arr[1:], n-1), arr[0])
def getMax(arr, n): 
    if(n==1):
        return arr[0]
    # If there is single element, return it. 
    # Else return maximum of first element 
    # and maximum of remaining array. 
    else:
        return max(getMax(arr[1:], n-1), arr[0])
 
# Driver code
arr = [12, 1234, 45, 67, 1]
n = len(arr)
print("Minimum element of array: ", 
                   getMin(arr, n));
print("Maximum element of array: ",
                   getMax(arr, n));
 
# This code is contributed by 
# Mohit Kumar 29
```

## C#

```cs
// C# program to find minimum 
// (or maximum) element 
// in an array.
using System; 
 
class GFG 
{ 
 
static int getMin(int []arr, int i, int n) 
{ 
    // If there is single element, return it. 
    // Else return minimum of first element and 
    // minimum of remaining array. 
    return (n == 1) ? arr[i] : Math.Min(arr[i], 
                    getMin(arr,i + 1 , n - 1)); 
} 
 
static int getMax(int []arr, int i, int n) 
{ 
    // If there is single element, return it. 
    // Else return maximum of first element and 
    // maximum of remaining array. 
    return (n == 1) ? arr[i] : Math.Max(arr[i], 
                    getMax(arr ,i + 1, n - 1)); 
} 
 
// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = { 12, 1234, 45, 67, 1 }; 
    int n = arr.Length; 
    Console.WriteLine("Minimum element of array: " +
                                getMin(arr, 0, n)); 
    Console.WriteLine("Maximum element of array: " + 
                                getMax(arr, 0, n)); 
} 
} 
 
// This code is contribute by Mohit
```

输出：

```
Min of array: 1
Max of array: 1234
```

使用库函数：

我们可以使用[`min_element()`](https://www.geeksforgeeks.org/stdmin_element-in-cpp/)和[`max_element()`](https://www.geeksforgeeks.org/stdmax_element-in-cpp/)来找到数组的最小值和最大值。

## C++

```cpp
// CPP program to find minimum (or maximum) element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 
 
int getMin(int arr[], int n) 
{ 
    return *min_element(arr, arr + n); 
} 
 
int getMax(int arr[], int n) 
{ 
    return *max_element(arr, arr + n); 
} 
 
int main() 
{ 
    int arr[] = { 12, 1234, 45, 67, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum element of array: " << getMin(arr, n) << "\n"; 
    cout << "Maximum element of array: " << getMax(arr, n); 
    return 0; 
}
```

## Java

```java
import java.util.Arrays;
 
// Java program to find minimum (or maximum) element 
// in an array. 
import java.util.Arrays;
 
class GFG {
 
    static int getMin(int arr[], int n) {
        return Arrays.stream(arr).min().getAsInt();
    }
 
    static int getMax(int arr[], int n) {
        return Arrays.stream(arr).max().getAsInt();
    }
 
// Driver code 
    public static void main(String[] args) {
        int arr[] = {12, 1234, 45, 67, 1};
        int n = arr.length;
        System.out.println("Minimum element of array: " + getMin(arr, n));
        System.out.println("Maximum element of array: " + getMax(arr, n));
    }
}
/*This Java code is contributed by 29AjayKumar*/
```

## Python3

```py
# Python3 program to find minimum 
# (or maximum) element 
# in an array. 
def getMin(arr,n):
    return min(arr)
 
def getMax(arr,n):
    return max(arr)
 
# Driver Code
if __name__=='__main__':
    arr = [12,1234,45,67,1]
    n = len(arr)
    print("Minimum element of array: "
          ,getMin(arr, n))
    print("Maximum element of array: "
          ,getMax(arr, n))
 
# This code is contributed by 
# Shrikant13
```

## C#

```cs
// C# program to find minimum 
// (or maximum) element in an array. 
using System;
using System.Linq;
class GFG
{ 
static int getMin(int []arr, int n) 
{
    return arr.Min();
}
 
static int getMax(int []arr, int n)
{
    return arr.Max();
}
 
// Driver code 
public static void Main(String[] args) 
{
    int []arr = {12, 1234, 45, 67, 1};
    int n = arr.Length;
    Console.WriteLine("Minimum element of array: " + 
                                    getMin(arr, n));
    Console.WriteLine("Maximum element of array: " + 
                                    getMax(arr, n));
}
}
 
// This code is contributed by 29AjayKumar
```

## PHP

```php
<?php 
// PHP program to find minimum (or maximum) 
// element in an array. 
 
function getMin(&$arr, $n) 
{ 
    return min($arr); 
} 
 
function getMax(&$arr, $n) 
{ 
    return max($arr); 
} 
 
// Driver Code
$arr = array(12, 1234, 45, 67, 1 ); 
$n = sizeof($arr); 
echo "Minimum element of array: " . 
           getMin($arr, $n) . "\n"; 
echo "Maximum element of array: " .
                  getMax($arr, $n); 
 
// This code is contributed 
// by ChitraNayal
?>
```

输出：

```
Minimum element of array: 1
Maximum element of array: 1234
```


