# 将所有零移动到数组末尾

> 原文： [https://www.geeksforgeeks.org/move-zeroes-end-array/](https://www.geeksforgeeks.org/move-zeroes-end-array/)

给定一个随机数数组，将给定数组的所有零都推到该数组的末尾。 例如，如果给定数组为`{1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0}`，则应将其更改为`{1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}`。 所有其他元素的顺序应相同。 预期时间复杂度为`O(n)`，额外空间为`O(1)`。

**示例**：

```
Input :  arr[] = {1, 2, 0, 4, 3, 0, 5, 0};
Output : arr[] = {1, 2, 4, 3, 5, 0, 0};

Input : arr[]  = {1, 2, 0, 0, 0, 3, 6};
Output : arr[] = {1, 2, 3, 6, 0, 0, 0};

```



有很多方法可以解决此问题。 以下是解决此问题的简单有趣的方法。

从左到右遍历给定的数组`arr`。 遍历时，维护数组中非零元素的数量。 让计数为`count`。 对于每个非零元素`arr[i]`，将其放在`arr[count]`处，并递增`count`。 完全遍历之后，所有非零元素都已移至前端，并且`count`被设置为前 0 的索引。现在我们要做的就是运行一个循环，使所有元素从`count`到结束都为零。 的数组。

下面是上述方法的实现。

## C++ 

```cpp

// A C++ program to move all zeroes at the end of array 
#include <iostream> 
using namespace std; 

// Function which pushes all zeros to end of an array. 
void pushZerosToEnd(int arr[], int n) 
{ 
    int count = 0;  // Count of non-zero elements 

    // Traverse the array. If element encountered is non- 
    // zero, then replace the element at index 'count'  
    // with this element 
    for (int i = 0; i < n; i++) 
        if (arr[i] != 0) 
            arr[count++] = arr[i]; // here count is  
                                   // incremented 

    // Now all non-zero elements have been shifted to  
    // front and  'count' is set as index of first 0.  
    // Make all elements 0 from count to end. 
    while (count < n) 
        arr[count++] = 0; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0, 9}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    pushZerosToEnd(arr, n); 
    cout << "Array after pushing all zeros to end of array :\n"; 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

/* Java program to push zeroes to back of array */
import java.io.*; 

class PushZero 
{ 
    // Function which pushes all zeros to end of an array. 
    static void pushZerosToEnd(int arr[], int n) 
    { 
        int count = 0;  // Count of non-zero elements 

        // Traverse the array. If element encountered is 
        // non-zero, then replace the element at index 'count' 
        // with this element 
        for (int i = 0; i < n; i++) 
            if (arr[i] != 0) 
                arr[count++] = arr[i]; // here count is 
                                       // incremented 

        // Now all non-zero elements have been shifted to 
        // front and 'count' is set as index of first 0\. 
        // Make all elements 0 from count to end. 
        while (count < n) 
            arr[count++] = 0; 
    } 

    /*Driver function to check for above functions*/
    public static void main (String[] args) 
    { 
        int arr[] = {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0, 9}; 
        int n = arr.length; 
        pushZerosToEnd(arr, n); 
        System.out.println("Array after pushing zeros to the back: "); 
        for (int i=0; i<n; i++) 
            System.out.print(arr[i]+" "); 
    } 
} 
/* This code is contributed by Devesh Agrawal */

```

## Python3

```py

# Python3 code to move all zeroes 
# at the end of array 

# Function which pushes all 
# zeros to end of an array. 
def pushZerosToEnd(arr, n): 
    count = 0 # Count of non-zero elements 

    # Traverse the array. If element  
    # encountered is non-zero, then 
    # replace the element at index 
    # 'count' with this element 
    for i in range(n): 
        if arr[i] != 0: 

            # here count is incremented 
            arr[count] = arr[i] 
            count+=1

    # Now all non-zero elements have been 
    # shifted to front and 'count' is set 
    # as index of first 0\. Make all  
    # elements 0 from count to end. 
    while count < n: 
        arr[count] = 0
        count += 1

# Driver code 
arr = [1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0, 9] 
n = len(arr) 
pushZerosToEnd(arr, n) 
print("Array after pushing all zeros to end of array:") 
print(arr) 

# This code is contributed by "Abhishek Sharma 44" 

```

## C# 

```cs

/* C# program to push zeroes to back of array */
using System; 

class PushZero 
{ 
    // Function which pushes all zeros  
    // to end of an array. 
    static void pushZerosToEnd(int []arr, int n) 
    { 
        // Count of non-zero elements 
        int count = 0;  

        // Traverse the array. If element encountered is 
        // non-zero, then replace the element  
        // at index â..countâ.. with this element 
        for (int i = 0; i < n; i++) 
        if (arr[i] != 0) 

        // here count is incremented 
        arr[count++] = arr[i];  

        // Now all non-zero elements have been shifted to 
        // front and â..countâ.. is set as index of first 0\. 
        // Make all elements 0 from count to end. 
        while (count < n) 
        arr[count++] = 0; 
    } 

    // Driver function  
    public static void Main () 
    { 
        int []arr = {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0, 9}; 
        int n = arr.Length; 
        pushZerosToEnd(arr, n); 
        Console.WriteLine("Array after pushing all zeros to the back: "); 
        for (int i = 0; i < n; i++) 
        Console.Write(arr[i] +" "); 
    } 
} 
/* This code is contributed by Anant Agrawal */

```

## PHP

```php

<?php  
// A PHP program to move all 
// zeroes at the end of array 

// Function which pushes all  
// zeros to end of an array. 
function pushZerosToEnd(&$arr, $n) 
{ 
    // Count of non-zero elements 
    $count = 0;  

    // Traverse the array. If  
    // element encountered is 
    // non-zero, then replace  
    // the element at index  
    // 'count' with this element 
    for ($i = 0; $i < $n; $i++) 
        if ($arr[$i] != 0) 
            // here count is incremented 
            $arr[$count++] = $arr[$i];  

    // Now all non-zero elements  
    // have been shifted to front 
    // and 'count' is set as index   
    // of first 0\. Make all elements 
    // 0 from count to end. 
    while ($count < $n) 
        $arr[$count++] = 0; 
} 

// Driver Code 
$arr = array(1, 9, 8, 4, 0, 0, 
             2, 7, 0, 6, 0, 9); 
$n = sizeof($arr); 
pushZerosToEnd($arr, $n); 
echo "Array after pushing all " . 
     "zeros to end of array :\n"; 

for ($i = 0; $i < $n; $i++) 
echo $arr[$i] . " "; 

// This code is contributed  
// by ChitraNayal 
?> 

```

**输出**：

```
Array after pushing all zeros to end of array :
1 9 8 4 2 7 6 9 0 0 0 0
```

**时间复杂度**：`O(n)`，其中`n`是输入数组中的元素数。

**辅助空间**：`O(1)`。



