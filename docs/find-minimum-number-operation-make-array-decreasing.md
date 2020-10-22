# 使数组递减的最小减法运算数

> 原文： [https://www.geeksforgeeks.org/find-minimum-number-operation-make-array-decreasing/](https://www.geeksforgeeks.org/find-minimum-number-operation-make-array-decreasing/)

您将得到一个由数字`arr[0], arr[1], …, arr[N – 1]`和一个正整数`K`组成的序列。在每个运算中，都可以从数组的任何元素中减去`K`。 您需要找到使给定数组减少的最小操作数。

如果每个`i`（`0 <= i < N-1`）满足`arr[i] >= arr[i+1]`，则将数组`arr[0], arr[1], ....., arr[N-1]`称为递减。

> 输入：`N = 4`，`K = 5`，`arr[] = {1, 1, 2, 3}`
> 
> 输出：3
> 
> 说明：
> 
> 由于`arr[1] == arr[0]`，因此`arr[1]`不需要减法。 对于`arr[2]`，由于`arr[2] > arr[1]`（`2 > 1`），所以我们必须用`k`减去`arr[2]`，并且`arr[2]`的一个减法值是 -3 该值小于`arr[1]`的值，因此减法数仅需 1，现在`arr[2]`的值已更新了 -3。
> 
> 对于`arr[3]`同样，因为`arr[3] > arr[2]`（`3 > -3`），所以为此，我们必须两次将`arr[3]`减去`k`来得出`arr[3]`小于`arr[2]`，所需的减法数为 2，而`arr[3]`的更新值为 -7。 现在，通过在每个步骤上加上操作数来计算减法/操作的总数，即`0 + 1 + 2 = 3`。
> 
> 输入：`N = 5`，`K = 2`，`arr[] = {5, 4, 3, 2, 1}`
> 
> 输出：0


**方法**：

```
1\. Traverse each element of array from 1 to n-1.
2\. Check if (arr[i] > arr[i-1]) then
    Find noOfSubtraction; 
     noOfSubtraction = 

   If ( (arr[i] - arr[i-1]) % k == 0 )
     then noOfSubtraction++

   Modify arr[i]; 
     arr[i] = 
```

以下是上述方法的实现：

## CPP

```

// CPP program to make an array decreasing 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count minimum no of operation 
int min_noOf_operation(int arr[], int n, int k) 
{ 
    int noOfSubtraction; 
    int res = 0; 
    for (int i = 1; i < n; i++) { 
        noOfSubtraction = 0; 

        if (arr[i] > arr[i - 1]) { 

            // Count how many times we have to subtract. 
            noOfSubtraction = (arr[i] - arr[i - 1]) / k; 

            // Check an additional subtraction is  
            // required or not. 
            if ((arr[i] - arr[i - 1]) % k != 0) 
                noOfSubtraction++; 

            // Modify the value of arr[i]. 
            arr[i] = arr[i] - k * noOfSubtraction; 
        } 

        // Count total no of operation/subtraction . 
        res = res + noOfSubtraction; 
    } 

    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 1, 1, 2, 3 }; 
    int N = sizeof(arr) / sizeof(arr[0]); 
    int k = 5; 
    cout << min_noOf_operation(arr, N, k) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to make an 
// array decreasing 
import java.util.*; 
import java.lang.*; 
  
public class GfG{ 
      
    // Function to count minimum no of operation 
    public static int min_noOf_operation(int arr[],  
                                      int n, int k) 
    { 
        int noOfSubtraction; 
        int res = 0; 
          
        for (int i = 1; i < n; i++) { 
            noOfSubtraction = 0; 
  
            if (arr[i] > arr[i - 1]) { 
      
                // Count how many times  
                // we have to subtract. 
                noOfSubtraction = (arr[i] - arr[i - 1]) / k; 
  
                // Check an additional subtraction  
                // is required or not. 
                if ((arr[i] - arr[i - 1]) % k != 0) 
                    noOfSubtraction++; 
  
                // Modify the value of arr[i] 
                arr[i] = arr[i] - k * noOfSubtraction; 
            } 
  
            // Count total no of subtraction 
            res = res + noOfSubtraction; 
        } 
  
        return res; 
    } 
      
    // driver function 
    public static void main(String argc[]){ 
        int arr = { 1, 1, 2, 3 }; 
        int N = 4; 
        int k = 5; 
        System.out.println(min_noOf_operation(arr, 
                                           N, k));  
    } 
      
} 
  
/* This code is contributed by Sagar Shukla */
```

## Python3

```py
# Python program to make an array decreasing 
  
# Function to count minimum no of operation 
def min_noOf_operation(arr, n, k): 
  
    res = 0
    for i in range(1,n): 
        noOfSubtraction = 0
  
        if (arr[i] > arr[i - 1]): 
  
            # Count how many times we have to subtract. 
            noOfSubtraction = (arr[i] - arr[i - 1]) / k; 
  
            # Check an additional subtraction is  
            # required or not. 
            if ((arr[i] - arr[i - 1]) % k != 0): 
                noOfSubtraction+=1
  
            # Modify the value of arr[i]. 
            arr[i] = arr[i] - k * noOfSubtraction 
          
  
        # Count total no of operation/subtraction . 
        res = res + noOfSubtraction 
      
  
    return int(res) 
  
  
# Driver Code 
arr = [ 1, 1, 2, 3 ] 
N = len(arr) 
k = 5
print(min_noOf_operation(arr, N, k)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal
```

## C#

```cs
// C# program to make an 
// array decreasing 
using System; 
  
public class GfG{ 
      
    // Function to count minimum no of operation 
    public static int min_noOf_operation(int []arr,  
                                       int n, int k) 
    { 
        int noOfSubtraction; 
        int res = 0; 
          
        for (int i = 1; i < n; i++) { 
            noOfSubtraction = 0; 
  
            if (arr[i] > arr[i - 1]) { 
      
                // Count how many times  
                // we have to subtract. 
                noOfSubtraction = (arr[i] - arr[i - 1]) / k; 
  
                // Check an additional subtraction  
                // is required or not. 
                if ((arr[i] - arr[i - 1]) % k != 0) 
                    noOfSubtraction++; 
  
                // Modify the value of arr[i] 
                arr[i] = arr[i] - k * noOfSubtraction; 
            } 
  
            // Count total no of subtraction 
            res = res + noOfSubtraction; 
        } 
  
        return res; 
    } 
      
    // driver function 
    public static void Main() 
    { 
        int []arr = { 1, 1, 2, 3 }; 
        int N = 4; 
        int k = 5; 
        Console.WriteLine(min_noOf_operation(arr, 
                                        N, k));  
    } 
      
} 
  
// This code is contributed by vt_m
```

## PHP

```php
<?php 
// PHP program to make an array decreasing 
  
// Function to count minimum no of operation 
function min_noOf_operation($arr, $n, $k) 
{ 
      
    $noOfSubtraction; 
    $res = 0; 
    for($i = 1; $i < $n; $i++)  
    { 
        $noOfSubtraction = 0; 
  
        if ($arr[$i] > $arr[$i - 1])  
        { 
  
            // Count how many times we 
            // have to subtract. 
            $noOfSubtraction = ($arr[$i] -  
                      $arr[$i - 1]) / $k; 
  
            // Check an additional subtraction  
            // is required or not. 
            if (($arr[$i] - $arr[$i - 1])  
                               % $k != 0) 
                $noOfSubtraction++; 
  
            // Modify the value of arr[i]. 
            $arr[$i] = $arr[$i] - $k *  
                      $noOfSubtraction; 
        } 
  
        // Count total no of  
        // operation/subtraction . 
        $res = $res + $noOfSubtraction; 
    } 
  
    return floor($res); 
} 
  
    // Driver Code 
    $arr = array(1, 1, 2, 3); 
    $N = count($arr); 
    $k = 5; 
    echo min_noOf_operation($arr, $N, $k) ; 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
 3
```

时间复杂度：`O(N)`。