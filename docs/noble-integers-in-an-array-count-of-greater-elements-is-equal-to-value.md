# 数组中的高尚整数（大于等于值的元素数）

> 原文： [https://www.geeksforgeeks.org/noble-integers-in-an-array-count-of-greater-elements-is-equal-to-value/](https://www.geeksforgeeks.org/noble-integers-in-an-array-count-of-greater-elements-is-equal-to-value/)

给定数组`arr[]`，在其中找到一个高尚整数。 如果大于`x`的整数数量等于`x`，则在`arr[]`中将整数`x`称为高尚的。 如果有许多高尚整数，则返回其中的任何一个。 如果没有，则返回 -1。

**示例**：

```
Input  : [7, 3, 16, 10]
Output : 3  
Number of integers greater than 3
is three.

Input  : [-1, -9, -2, -78, 0]
Output : 0
Number of integers greater than 0
is zero.

```



**方法 1（暴力）**：

迭代数组。 对于每个元素`arr[i]`，找到大于`arr[i]`的元素数量。

## CPP

```

// C++ program to find Noble elements 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns a Noble integer if present, 
// else returns -1\. 
int nobleInteger(int arr[], int size) 
{ 
    for (int i = 0; i < size; i++ ) 
    { 
        int count = 0; 
        for (int j = 0; j < size; j++)  
            if (arr[i] < arr[j]) 
                count++; 

        // If count of greater elements 
        // is equal to arr[i] 
        if (count == arr[i]) 
            return arr[i]; 
    } 

    return -1; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {10, 3, 20, 40, 2}; 
    int size = sizeof(arr) / sizeof(arr[0]); 
    int res = nobleInteger(arr, size); 

    if (res != -1) 
        cout<<"The noble integer is "<< res; 
    else
        cout<<"No Noble Integer Found"; 
} 

// This code is contributed by Smitha. 

```

## Java

```
// Java program to find Noble elements 
// in an array. 
import java.util.ArrayList; 
  
class GFG { 
      
    // Returns a Noble integer if present, 
    // else returns -1. 
    public static int nobleInteger(int arr[]) 
    { 
        int size = arr.length; 
        for (int i = 0; i < size; i++ ) 
        { 
            int count = 0; 
            for (int j = 0; j < size; j++) 
                if (arr[i] < arr[j]) 
                    count++; 
  
            // If count of greater elements 
            // is equal to arr[i] 
            if (count == arr[i]) 
                return arr[i]; 
        } 
        return -1; 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int [] arr = {10, 3, 20, 40, 2}; 
        int res = nobleInteger(arr); 
        if (res != -1) 
            System.out.println("The noble "
                     + "integer is "+ res); 
        else
            System.out.println("No Noble "
                        + "Integer Found"); 
    } 
}
```

## Python3

```
# Python3 program to find Noble 
# elements in an array. 
  
# Returns a Noble integer if 
# present, else returns -1. 
def nobleInteger(arr, size): 
  
    for i in range(0, size): 
      
        count = 0
        for j in range(0, size): 
            if (arr[i] < arr[j]): 
                count += 1
        # If count of greater  
        # elements is equal 
        # to arr[i] 
        if (count == arr[i]): 
            return arr[i] 
      
    return -1
  
# Driver code 
arr = [10, 3, 20, 40, 2] 
size = len(arr) 
res = nobleInteger(arr,size) 
if (res != -1):  
    print("The noble integer is ", 
                              res) 
else: 
    print("No Noble Integer Found") 
  
# This code is contributed by 
# Smitha.
```

## C#

```
// C# program to find Noble elements 
// in an array. 
using System; 
  
class GFG { 
      
    // Returns a Noble integer if present, 
    // else returns -1. 
    public static int nobleInteger(int [] arr) 
    { 
        int size = arr.Length; 
        for (int i = 0; i < size; i++ ) 
        { 
            int count = 0; 
            for (int j = 0; j < size; j++) 
                if (arr[i] < arr[j]) 
                    count++; 
  
            // If count of greater elements 
            // is equal to arr[i] 
            if (count == arr[i]) 
                return arr[i]; 
        } 
          
        return -1; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int [] arr = {10, 3, 20, 40, 2}; 
        int res = nobleInteger(arr); 
        if (res != -1) 
            Console.Write("The noble integer"
                              + " is "+ res); 
        else
            Console.Write("No Noble Integer"
                                 + " Found"); 
    } 
} 
  
// This code is contributed by Smitha.
```

## PHP

```
<?php 
// PHP program to find Noble  
// elements in an array. 
  
// Returns a Noble integer  
// if present, else returns -1. 
function nobleInteger( $arr, $size) 
{ 
    for ( $i = 0; $i < $size; $i++ ) 
    { 
        $count = 0; 
        for ( $j = 0; $j < $size; $j++)  
            if ($arr[$i] < $arr[$j]) 
                $count++; 
                  
        // If count of greater elements 
        // is equal to arr[i] 
        if ($count == $arr[$i]) 
            return $arr[$i]; 
    } 
      
    return -1; 
} 
  
// Driver code 
$arr = array(10, 3, 20, 40, 2); 
$size = count($arr); 
$res = nobleInteger($arr, $size); 
  
if ($res != -1) 
    echo "The noble integer is ", $res; 
else
    echo "No Noble Integer Found"; 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
The noble integer is 3
```

方法 2（使用排序）：

以升序对数组`arr[]`进行排序。 此步骤需要`O(nlogn)`。

遍历数组。 将索引`i`的值与索引`i`之后的元素数进行比较。 如果`arr[i]`等于`arr[i]`之后的元素数，则它是一个整数。 检查条件：`A[i] == length-i-1`。 此步骤需要`O(n)`。

注意：数组可能具有重复的元素。 所以，我们应该跳过相同的元素（排序数组中的相邻元素）。

## C++

```
// C++ program to find Noble elements 
// in an array. 
#include<bits/stdc++.h> 
using namespace std; 
  
// Returns a Noble integer if present, 
// else returns -1. 
int nobleInteger(int arr[], int n) 
{ 
    sort(arr, arr + n); 
  
    // Return a Noble element if present 
    // before last. 
    for (int i = 0; i < n - 1; i++) 
    { 
        if (arr[i] == arr[i + 1]) 
            continue; 
  
        // In case of duplicates, we 
        // reach last occurrence here. 
        if (arr[i] == n - i - 1) 
            return arr[i]; 
    } 
    if (arr[n - 1] == 0) 
        return arr[n - 1]; 
    return -1; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = {10, 3, 20, 40, 2}; 
    int res = nobleInteger(arr, 5); 
    if (res != -1) 
        cout << "The noble integer is " << res; 
    else
        cout << "No Noble Integer Found"; 
    return 0; 
} 
  
// This code is contributed by Rajput-Ji
```

## Java

```
// Java program to find Noble elements 
// in an array. 
import java.util.Arrays; 
  
public class Main 
{ 
    // Returns a Noble integer if present, 
    // else returns -1. 
    public static int nobleInteger(int arr[]) 
    { 
        Arrays.sort(arr); 
  
        // Return a Noble element if present 
        // before last. 
        int n = arr.length; 
        for (int i=0; i<n-1; i++) 
        { 
            if (arr[i] == arr[i+1]) 
                continue; 
  
            // In case of duplicates, we 
            // reach last occurrence here. 
            if (arr[i] == n-i-1) 
                return arr[i]; 
        } 
  
        if (arr[n-1] == 0) 
            return arr[n-1]; 
  
        return -1; 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int [] arr = {10, 3, 20, 40, 2}; 
        int res = nobleInteger(arr); 
        if (res != -1) 
            System.out.println("The noble integer is "+ res); 
        else
            System.out.println("No Noble Integer Found"); 
    } 
}
```

## Python

```
# Python3 code to find Noble elements 
# in an array 
  
def nobleInteger(arr): 
      
    arr.sort() 
      
    # Return a Noble element if  
    # present before last 
    n = len(arr) 
      
    for i in range(n - 1): 
          
        if arr[i] == arr[i + 1]: 
            continue
              
        # In case of duplicates we reach 
        # last occurrence here 
        if arr[i] == n - i - 1: 
            return arr[i] 
      
    if arr[n - 1] == 0: 
        return arr[n - 1] 
    return -1
  
# Driver code 
arr = [10, 3, 20, 40, 2] 
  
res = nobleInteger(arr) 
  
if res != -1: 
    print("The noble integer is", res) 
else: 
    print("No Noble Integer Found") 
  
# This code is contributed 
# by Mohit Kumar
```

## C#

```
// C# program to find Noble elements 
// in an array.  
using System; 
  
public class GFG { 
      
    public static int nobleInteger(int[] arr) 
    { 
        Array.Sort(arr); 
  
        // Return a Noble element if present 
        // before last. 
        int n = arr.Length; 
        for (int i = 0; i < n-1; i++) 
        { 
            if (arr[i] == arr[i+1]) 
                continue; 
  
            // In case of duplicates, we 
            // reach last occurrence here. 
            if (arr[i] == n-i-1) 
                return arr[i]; 
        } 
  
        if (arr[n-1] == 0) 
            return arr[n-1]; 
  
        return -1; 
    } 
      
    // Driver code 
    static public void Main () 
    { 
        int [] arr = {10, 3, 20, 40, 2}; 
        int res = nobleInteger(arr); 
        if (res != -1) 
        Console.Write("The noble integer is "
                                      + res); 
        else
            Console.Write("No Noble Integer " 
                                  + "Found"); 
          
    } 
} 
  
// This code is contributed by Shrikant13.
```

## PHP

```
<?php 
// PHP program to find Noble elements 
  
// Returns a Noble integer if present, 
// else returns -1. 
function nobleInteger( $arr) 
    { 
        sort($arr); 
  
        // Return a Noble element if  
        // present before last. 
        $n = count($arr); 
        for ( $i = 0; $i < $n - 1; $i++) 
        { 
            if ($arr[$i] == $arr[$i + 1]) 
                continue; 
  
            // In case of duplicates, we 
            // reach last occurrence here. 
            if ($arr[$i] == $n - $i - 1) 
                return $arr[$i]; 
        } 
  
        if ($arr[$n - 1] == 0) 
            return $arr[$n - 1]; 
  
        return -1; 
    } 
  
    // Driver code 
    $arr = array(10, 3, 20, 40, 2); 
    $res = nobleInteger($arr); 
    if ($res != -1) 
        echo "The noble integer is ", $res; 
    else
        echo "No Noble Integer Found"; 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
The noble integer is 3.
```


